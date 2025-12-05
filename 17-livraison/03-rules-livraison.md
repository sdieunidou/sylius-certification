# Rule checkers de livraison

## Objectif
Restreindre l'affichage des méthodes.

## Rules Natives
1.  **Order Total** : ex: Disponible seulement si panier > 50€.
2.  **Order Weight** : ex: Disponible seulement si poids < 30kg.

## Extension
Comme pour les promotions, on peut créer des `RuleChecker` personnalisés.
Tag : `sylius.shipping_method_rule_checker`.

Exemple : "Disponible seulement le week-end".

