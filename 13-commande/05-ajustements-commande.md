# Comportement et détails sur les ajustements de commande

## Objectif
Comprendre comment Sylius stocke les taxes, promos et frais.

## Adjustment
Entité : `Sylius\Component\Core\Model\Adjustment`.

Tout montant qui s'ajoute ou se soustrait du prix des produits est un `Adjustment`.
*   `type` : Clé string (ex: `tax`, `shipping`, `order_promotion`).
*   `amount` : Entier (+ ou -).
*   `neutral` : Booléen. Si `true`, l'ajustement est informatif et n'impacte pas le total à payer (rare, ex: taxe incluse affichée séparément).
*   `locked` : Si `true`, le processeur ne recalculera pas cet ajustement (utile pour figer des frais).

## Récupération
`$order->getAdjustments('tax')` retourne la collection des taxes.
`$order->getAdjustmentsTotal('tax')` retourne la somme.

