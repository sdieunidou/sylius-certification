# Détails et prérequis pour chaque étape du processus de commande

## Objectif
Connaître le fonctionnement détaillé des étapes standard du checkout Sylius et leurs validateurs.

## Le Checkout Resolver

Sylius utilise un `CheckoutResolver` (`sylius.resolver.checkout`) pour déterminer si un utilisateur peut accéder à une étape donnée. Si les prérequis ne sont pas remplis (ex: accéder au paiement sans adresse), il redirige vers la première étape incomplète.

## 1. Addressing (Adressage)
*   **URL** : `/checkout/address`
*   **Prérequis** : Le panier ne doit pas être vide.
*   **Données saisies** : Adresse de facturation (`billingAddress`), Adresse de livraison (`shippingAddress`).
*   **Logique spéciale** : Si l'utilisateur coche "Même adresse pour la livraison", l'adresse de facturation est dupliquée.
*   **Validation** : Validation standard des entités Address + vérification des zones (si configuré).

## 2. Shipping (Livraison)
*   **URL** : `/checkout/select-shipping`
*   **Prérequis** : État `addressed`. Le panier doit contenir des articles expédiables (`isShippingRequired()`).
*   **Données saisies** : Une méthode de livraison par "Shipment" (Expédition).
*   **Cas multi-expédition** : Si le panier contient des articles stockés dans des endroits différents ou avec des modalités différentes, Sylius peut générer plusieurs objets `Shipment`. L'utilisateur doit choisir une méthode pour *chaque* expédition.
*   **Validation** : La méthode choisie doit être disponible pour la zone de l'adresse de livraison.

## 3. Payment (Paiement)
*   **URL** : `/checkout/select-payment`
*   **Prérequis** : État `shipping_selected` (ou `shipping_skipped`).
*   **Données saisies** : Une méthode de paiement.
*   **Logique spéciale** :
    *   Si le total est 0 (gratuit), cette étape peut être sautée (`payment_skipped`).
    *   Création de l'objet `Payment` associé à la commande.

## 4. Summary (Récapitulatif) & Complete
*   **URL** : `/checkout/summary` (souvent combiné avec l'action finale).
*   **Prérequis** : État `payment_selected`.
*   **Action** : L'utilisateur confirme. Cela déclenche la transition `complete`.
*   **Post-traitement** : Redirection vers la page de paiement externe (PayPal, Stripe) OU page de remerciement si paiement hors-ligne (Chèque).

## Interaction Frontend (ShopBundle)
Sylius utilise des formulaires Symfony classiques pour chaque étape.
*   `AddressType`
*   `SelectShippingType`
*   `SelectPaymentType`

## API Platform (Headless)
En API, la logique est identique mais gérée via des opérations `PATCH` ou des commandes Messenger spécifiques sur la ressource `Order`.
Les violations de contraintes (ex: essayer de payer sans shipping) renvoient des erreurs 400/422 basées sur la machine à états.

