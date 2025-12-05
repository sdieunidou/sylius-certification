# Actions possibles sur le panier dans Sylius

## Objectif
Lister et expliquer les manipulations possibles sur l'objet `Order` lorsqu'il est dans l'état `cart`.

## Le Panier est une Commande
Dans Sylius, **Panier = Commande** (`Order`) avec l'état `cart`. Il n'y a pas d'entité "Panier" séparée en base de données.

## Actions Principales

### 1. Ajouter un article (Add to Cart)
*   **Service** : `sylius.order_item_quantity_modifier`
*   **Processus** :
    1.  Création d'un `OrderItem`.
    2.  Lien avec le `ProductVariant`.
    3.  Définition de la quantité.
    4.  Ajout à la `Order`.
*   **Contraintes** : Vérifie si le produit est activé et disponible.

### 2. Modifier la quantité (Modify Quantity)
*   **Action** : Changer la quantité d'un `OrderItem` existant.
*   **Quantité 0** : Si la quantité tombe à 0, l'item est supprimé du panier.
*   **Recalcul** : Déclenche le `OrderProcessor` pour mettre à jour les totaux et promotions.

### 3. Supprimer un article (Remove Item)
*   Supprime physiquement l'entité `OrderItem` de la collection `items` de la commande.

### 4. Appliquer un Code Promo (Coupon)
*   **Champ** : `promotionCoupon` sur l'entité `Order`.
*   **Action** : L'utilisateur soumet un code.
*   **Traitement** : Le système vérifie la validité du coupon. Si valide, il est attaché à la commande. Les promotions éligibles sont recalculées.

### 5. Vider le panier (Clear Cart)
*   Action de suppression de tous les items ou abandon de la commande (création d'un nouveau panier frais).

## Gestionnaires de Panier (Cart Context)

Comment Sylius sait quel est le panier actuel ?

*   **CartContextInterface** : Service qui retrouve le panier courant.
*   **CartProvider** : Logique de récupération (Session, Token JWT, Base de données).
*   **Storage** : En session par défaut pour les invités, lié au `Customer` pour les connectés.

### Fusion des paniers (Cart Merge)
Lorsqu'un utilisateur invité se connecte :
1.  Sylius détecte s'il avait un panier en session.
2.  Il détecte s'il a un panier existant non-terminé en base.
3.  Les items du panier session sont déplacés vers le panier utilisateur (ou vice-versa selon config).

## Code : Ajouter au panier programmatiquement

```php
/** @var OrderModifierInterface $orderModifier */
$orderModifier = $container->get('sylius.order_modifier');
/** @var OrderItemFactoryInterface $itemFactory */
$itemFactory = $container->get('sylius.factory.order_item');

$item = $itemFactory->createNew();
$item->setVariant($variant);
$orderModifier->addToOrder($cart, $item);

$cartManager->persist($cart);
$cartManager->flush();
```

