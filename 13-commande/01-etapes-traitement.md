# Détails sur les étapes du traitement d'une commande

## Objectif
Que se passe-t-il après le clic sur "Payer" ?

## Le OrderProcessor (Rappel)
Le processeur tourne à chaque modification du panier. Une fois la commande validée (`checkout_completed`), le processeur ne tourne plus automatiquement pour garantir l'immutabilité des prix.

## Cycle de Vie Post-Checkout

1.  **Validation (Create)** : La commande passe de l'état `cart` à `new`.
    *   Stock décrémenté (onHold).
    *   Email de confirmation envoyé.
2.  **Paiement** :
    *   L'utilisateur est redirigé vers la gateway.
    *   Au retour (IPN/Webhook), le paiement passe à `completed`.
    *   La commande passe à l'état de paiement `paid`.
3.  **Préparation (Fulfillment)** :
    *   L'admin voit la commande "Payée".
    *   Il prépare le colis.
4.  **Expédition (Shipping)** :
    *   L'admin clique sur "Ship".
    *   La commande passe à l'état de livraison `shipped`.
    *   Le stock physique est décrémenté (onHand).
5.  **Terminée** :
    *   Si Paiement = Paid ET Livraison = Shipped, la commande passe à `fulfilled` (selon config).

## Immutabilité
Une fois la commande passée, on ne doit plus modifier les prix unitaires ou les promotions. Les données sont figées dans les entités `OrderItem` et `Adjustment`.

