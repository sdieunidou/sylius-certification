# États de la commande

## Objectif
Maîtriser les 3 axes d'état d'une commande.

Une commande Sylius a **trois** machines à états indépendantes mais liées.

1.  **Order State** (`state`) : État global.
    *   `cart`, `new`, `cancelled`, `fulfilled`.
2.  **Payment State** (`paymentState`) : État financier.
    *   `cart`, `awaiting_payment`, `paid`, `partially_paid`, `cancelled`, `refunded`.
3.  **Shipping State** (`shippingState`) : État logistique.
    *   `cart`, `ready`, `shipped`, `partially_shipped`, `cancelled`.

## Le State Resolver (`OrderStateResolver`)
C'est un service qui observe les états Payment et Shipping pour mettre à jour l'état Global.
*   Si Payment = `paid` et Shipping = `shipped` -> Order = `fulfilled` (si configuré ainsi).

