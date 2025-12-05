# Services disponibles et fonctionnalités par défaut

## Objectif
Utiliser l'écosystème Resource.

## Factory
*   `createNew()` : Retourne une nouvelle instance.

## Repository
Étend par défaut `EntityRepository`.
*   `add($resource)`
*   `remove($resource)`
*   `createPaginator(array $criteria, array $sorting)` : Spécifique Sylius pour la pagination.

## Controller (ResourceController)
Fournit les actions standard :
*   `showAction`, `indexAction`
*   `createAction`, `updateAction`, `deleteAction`
*   `applyStateMachineTransitionAction`

Ces actions gèrent la Request, le Form, la validation, le Flash message, la redirection et l'Event Dispatching.

## Manager
C'est un alias de l'EntityManager Doctrine (ou DocumentManager).

