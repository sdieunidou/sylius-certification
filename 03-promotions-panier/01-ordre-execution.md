# Ordre d'exécution et résultats du calcul des promotions

## Objectif
Comprendre quand et comment les promotions de panier sont appliquées pour garantir des totaux corrects.

## Le OrderProcessor

Le calcul des promotions fait partie du cycle de traitement de la commande (`OrderProcessing`).
Service clé : `Sylius\Component\Core\OrderProcessing\OrderProcessor`.

Ce processeur exécute plusieurs tâches en séquence :
1.  **OrderPricesRecalculator** : Recalcule les prix unitaires des items (base price).
2.  **OrderInventoryProcessor** : Vérifie les stocks.
3.  **ShippingChargesProcessor** : Calcule les frais de port.
4.  **OrderPromotionProcessor** : C'est ici que les promotions s'appliquent.
5.  **OrderTaxesProcessor** : Les taxes s'appliquent en dernier (généralement sur le prix remisé).

## Logique d'application des promotions (`PromotionProcessor`)

1.  **Nettoyage** : Toutes les promotions ("adjustments") précédemment appliquées sont supprimées de la commande pour éviter les doublons.
2.  **Sélection** : Le `PromotionRepository` récupère toutes les promotions **actives** pour le canal courant et la date courante.
3.  **Priorité** : Les promotions sont triées par `priority` (descendant). La priorité la plus haute passe en premier.
4.  **Éligibilité (Rules)** : Pour chaque promotion, le `RuleChecker` vérifie si la commande remplit les conditions (ex: Total > 100€).
5.  **Application (Actions)** : Si éligible, l' `ActionExecutor` applique la réduction (ex: -10%).
6.  **Exclusivité** :
    *   Si une promotion est marquée `exclusive`, et qu'elle est appliquée, **le processus s'arrête**. Aucune autre promotion (même valide) ne sera testée ensuite.
    *   L'ordre de priorité est donc crucial pour les promotions exclusives.

## Résultats

Le résultat est la création d'objets `Adjustment` liés à la Commande (`Order`) ou aux Lignes (`OrderItem`).
Type d'ajustement : `AdjustmentInterface::ORDER_PROMOTION_ADJUSTMENT` ou `ORDER_ITEM_PROMOTION_ADJUSTMENT`.

Ces ajustements modifient le `total` à payer.

## Exemple de conflit

*   Promo A (Priorité 10, Exclusive) : -20%
*   Promo B (Priorité 5) : -5€

Si la commande est éligible aux deux :
Seule la Promo A s'applique car elle est exclusive et prioritaire. La Promo B est ignorée.
Si Promo A n'était pas exclusive, le client aurait -20% PUIS -5€.

