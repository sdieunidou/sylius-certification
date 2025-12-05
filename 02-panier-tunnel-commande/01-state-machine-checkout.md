# Détails sur la machine à états (state machine) du checkout

## Objectif
Comprendre comment le workflow de commande est piloté par la machine à états `sylius_order_checkout`.

## Concepts Clés

Sylius utilise `winzou/state-machine-bundle` pour gérer les transitions de la commande. Il y a deux machines à états principales pour une commande :
1.  `sylius_order` : Le cycle de vie global (New -> Cancelled/Fulfilled).
2.  `sylius_order_checkout` : Le focus de cette fiche, qui gère spécifiquement le tunnel d'achat (Panier -> Commande validée).

### États du Checkout (`sylius_order_checkout`)

Les états sont définis dans `SyliusOrderBundle`.

*   `cart` : État initial. Le client modifie son panier.
*   `addressed` : L'adresse a été fournie et validée.
*   `shipping_selected` : La méthode de livraison a été choisie (si nécessaire).
*   `shipping_skipped` : Si aucune livraison n'est requise (ex: produits digitaux).
*   `payment_selected` : La méthode de paiement a été choisie.
*   `payment_skipped` : Si le total est de 0.
*   `completed` : La commande est passée (le client a cliqué sur "Payer/Commander").

## Transitions et Callbacks

C'est ici que la magie opère. Chaque transition déclenche des callbacks (logique métier).

| Transition | De | Vers | Actions Clés (Callbacks) |
| :--- | :--- | :--- | :--- |
| `address` | `cart` | `addressed` | Recalcul du panier (taxes, shipping costs provisoires). |
| `select_shipping` | `addressed` | `shipping_selected` | Application des frais de port réels. |
| `select_payment` | `shipping_selected` | `payment_selected` | Création de l'état de paiement initial (`new`). |
| `complete` | `payment_selected` | `completed` | **Crucial** : Valide la commande, décrémente le stock (selon config), assigne le numéro de commande, envoie l'email de confirmation. |

## Configuration

Le fichier de configuration se trouve généralement dans `config/packages/sylius_order.yaml` (ou surchargé dans `_sylius.yaml`).

```yaml
winzou_state_machine:
    sylius_order_checkout:
        callbacks:
            after:
                sylius_process_cart:
                    on: ["address", "select_shipping", "select_payment"]
                    do: ["@sylius.order_processing.order_processor", "process"]
                sylius_create_order:
                    on: ["complete"]
                    do: ["@sm.callback.cascade_transition", "apply"]
                    args: ["object", "event", "'create'", "'sylius_order'"]
```

## Extensibilité

Pour ajouter une étape (ex: "Vérification Identité") :
1.  Ajouter un nouvel état dans la configuration YAML.
2.  Définir les transitions vers et depuis cet état.
3.  Surcharger le `CheckoutResolver` ou le contrôleur de checkout pour diriger l'utilisateur vers la bonne page si l'état n'est pas atteint.

## Points de certification
*   La transition `complete` sur `sylius_order_checkout` déclenche automatiquement la transition `create` sur la machine `sylius_order`.
*   C'est la machine à état qui garantit qu'on ne peut pas payer sans avoir choisi une adresse.

