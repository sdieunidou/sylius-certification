# Rôle de chacune des étapes du traitement

## Objectif
Comprendre la sémantique des processeurs.

## Processeurs par défaut (OrderProcessing)

Ces processeurs agissent sur le **Panier** (avant validation).

1.  `OrderPricesRecalculator` : Prend le prix de base du ChannelPricing.
2.  `OrderInventoryProcessor` : Vérifie la disponibilité (ne bloque pas de stock, juste check).
3.  `OrderItemQuantityModifier` : Gère les règles de quantité min/max/step (si implémenté).
4.  `OrderTaxesProcessor` : Calcule la TVA.
5.  `OrderPromotionProcessor` : Applique les promos.
6.  `ShippingChargesProcessor` : Calcule les frais de port basés sur la méthode sélectionnée.

## Ordre d'exécution
Défini par la `priority` des tags de service `sylius.order_processor`.
Il est crucial que `Promotion` passe AVANT `Taxes` (si la taxe s'applique sur le prix réduit) ou APRÈS (si la taxe est sur le prix plein). Par défaut : Promo puis Taxe.

