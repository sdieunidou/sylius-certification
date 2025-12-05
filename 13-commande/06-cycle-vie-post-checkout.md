# Cycle de vie de la commande après le checkout

## Objectif
Gestion post-achat (SAV).

## Annulation (Cancel)
*   Possible tant que non expédiée (généralement).
*   Libère le stock (`onHold` -> 0).
*   Annule le paiement (Void) ou rembourse (Refund) si déjà capturé.

## Remboursement (Refund)
*   Géré via le plugin `RefundPlugin` (maintenant standard/recommandé avec Sylius).
*   Crée des `CreditMemo` (Avoirs).
*   Gère le remboursement partiel (ex: 1 item sur 3).

## Fulfillment (Expédition)
*   Peut être partiel (`partially_shipped`) si on envoie en plusieurs colis.
*   Sylius gère nativement les `Shipments` multiples.

