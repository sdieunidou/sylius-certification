# Dépendances actuelles de Sylius

## Objectif
Connaître la stack technologique (v2).

## Core
*   **PHP** : 8.1+ (voire 8.2 selon la version mineure).
*   **Symfony** : 6.4 ou 7.x (Full stack).
*   **Doctrine ORM** : 2.15+ (Persistence).

## Frontend (Shop/Admin Legacy)
*   **Twig** : Moteur de template.
*   **Bootstrap 5** (Admin) / **Semantic UI** (Shop Legacy - attention, Semantic UI est en cours de remplacement/dépréciation dans certaines parties mais reste très présent).
*   **Webpack Encore** : Build assets.
*   **Stimulus / Turbo** : Pour l'interactivité moderne dans l'admin v2.

## API
*   **API Platform** : 3.x.

## Tests
*   **PHPUnit** : Tests unitaires.
*   **Behat** : BDD (Behavior Driven Development) - Cœur de la stratégie de test Sylius.
*   **PHPSpec** : SpecBDD (Tests unitaires descriptifs).

## Outils
*   **Winzou State Machine** : Gestion des workflows.
*   **Pagerfanta** : Pagination.
*   **Payum** : Abstraction de paiement (sera potentiellement remplacé par une nouvelle couche dans le futur, mais présent en v2).

