# Fonctionnalités des fixtures

## Objectif
Savoir ce qu'on peut faire nativement.

## Modularité
Les fixtures sont découpées en unités logiques : `currency`, `locale`, `channel`, `product`, `tax_category`, etc.
Cela permet de ne charger QUE ce dont on a besoin pour un test spécifique.

## Example Factories
Sylius sépare la logique de "définition" (Fixture) de la logique de "création" (Factory).
Les `ExampleFactory` utilisent `OptionsResolver` pour valider les données YAML et fournir des valeurs par défaut (faker).

Exemple : Si je ne fournis pas le nom du produit, `ProductExampleFactory` en génère un aléatoire ("Black T-Shirt").

## Suites
On peut définir plusieurs "suites" :
*   `default` : Jeu complet pour le dev.
*   `performance` : 10,000 produits pour tester la charge.
*   `ui_test` : Données minimales et prévisibles pour Behat/Cypress.

Commande : `bin/console sylius:fixtures:load --suite=performance`.

