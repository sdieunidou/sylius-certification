# Gestion des stocks (inventory) durant le processus de commande

## Objectif
Comprendre comment et quand Sylius réserve ou décrémente le stock des produits.

## Documentation Officielle
*   [Inventory Guide](https://docs.sylius.com/en/latest/book/products/inventory.html)

## Concepts Clés

*   **On Hand** : Quantité physique en stock.
*   **On Hold** : Quantité réservée (dans des paniers validés mais pas encore expédiés/payés).
*   **Tracked** : Si `false`, le stock n'est pas géré pour cette variante (toujours disponible).

## Le Processus Standard

Par défaut, Sylius ne réserve **PAS** le stock lors de l'ajout au panier (pour éviter de bloquer du stock sur des paniers abandonnés).

### 1. Vérification de disponibilité (Availability Checking)
*   Se fait à l'ajout au panier (`AddToCart`).
*   Se fait à chaque étape du checkout pour s'assurer que le produit est toujours là.
*   Service : `AvailabilityCheckerInterface`.
    *   `isStockSufficient(variant, quantity)`

### 2. Réservation (Holding) - Transition `complete`
*   C'est au moment où l'utilisateur clique sur "Commander" (Transition `complete` du checkout).
*   L'écouteur `InventoryOrderStateListener` réagit.
*   Action : Augmente `onHold` pour chaque variante commandée.
*   Le stock physique (`onHand`) ne bouge pas encore.

### 3. Validation / Expédition - Transition `ship`
*   Lorsque le gestionnaire expédie la commande (Machine à état `sylius_shipment`, transition `ship`).
*   Action :
    *   Décrémente `onHand`.
    *   Décrémente `onHold`.
    *   Le stock sort définitivement de l'entrepôt.

## Configuration de la réservation

Il est possible de modifier ce comportement via la configuration de la machine à états si on souhaite réserver le stock plus tôt (ex: au moment du paiement).

## Gestion des ruptures (Backorders)

Si le stock est insuffisant mais que la variante autorise les "backorders" (commandes hors stock) :
*   `AvailabilityChecker` renvoie `true`.
*   Le stock `onHand` peut devenir négatif (ou géré séparément selon l'implémentation).

## InventoryOperator

Service central (`sylius.inventory.operator`) qui expose les méthodes :
*   `hold(variant, quantity)`
*   `release(variant, quantity)` (en cas d'annulation de commande)

