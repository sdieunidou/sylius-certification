# Commandes Sylius et leur utilisation

## Objectif
Connaître les commandes console spécifiques à Sylius pour l'administration et la maintenance.

## Installation et Initialisation

*   `bin/console sylius:install` : Lance l'assistant d'installation complet (check requirements, database, shop data, assets).
    *   `sylius:install:check-requirements`
    *   `sylius:install:database`
    *   `sylius:install:sample-data` : Charge des fixtures de démo.
    *   `sylius:install:assets` : Installe les assets (Gulp/Webpack build requis avant souvent).

## Fixtures

*   `bin/console sylius:fixtures:load` : Charge les fixtures définies dans `sylius_fixtures.yaml`.
    *   Options : `--group=group_name` (pour charger un sous-ensemble), `--no-interaction`.

## Utilisateurs Admin

*   `bin/console sylius:user:promote` : Donne le rôle `ROLE_ADMINISTRATION_ACCESS` à un utilisateur.
*   `bin/console sylius:user:demote` : Retire les droits admin.
*   `bin/console sylius:user:create` : Crée un utilisateur (Shop ou Admin selon les args).

## Canaux

*   `bin/console sylius:channel:list` : Liste les canaux configurés.

## Promotions & Catalogue

*   `bin/console sylius:process-catalog-promotions` : Force le recalcul des promotions catalogue (indispensable si le worker Messenger ne tourne pas).
*   `bin/console sylius:cancel-order` : Annule les commandes non payées après un délai (utile en CRON).
*   `bin/console sylius:remove-expired-carts` : Nettoie les paniers abandonnés (CRON).

## Thèmes (Si SyliusThemeBundle utilisé)

*   `bin/console sylius:theme:list` : Liste les thèmes détectés.
*   `bin/console sylius:theme:assets:install` : Installe les assets des thèmes (lien symbolique ou copie).

## Développement

*   `bin/console debug:container sylius` : Liste tous les services Sylius.
*   `bin/console debug:event-dispatcher sylius` : Liste tous les événements Sylius.

## Points de Certification
*   Savoir que `sylius:install` est une méta-commande qui en lance d'autres.
*   Connaître les commandes de nettoyage (paniers, commandes expirées) qui doivent tourner en tâche planifiée.
*   Le rôle crucial de `sylius:process-catalog-promotions` pour l'intégrité des prix.

