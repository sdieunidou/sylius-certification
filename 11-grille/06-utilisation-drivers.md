# Utilisation des grilles et drivers

## Objectif
Comprendre comment la grille récupère les données.

## Documentation Officielle
*   [Grid Drivers](https://docs.sylius.com/en/latest/components_and_bundles/bundles/SyliusGridBundle/index.html#drivers)

## Drivers
Le driver fait le lien entre la définition de la grille et la source de données.

1.  **Doctrine ORM** (`doctrine/orm`) : Le standard. Construit une requête SQL/DQL.
2.  **Vector** (Expérimental/Community) : Pour des sources Array.

## Fonctionnement
1.  Le `GridProvider` lit la config YAML.
2.  Le `GridViewFactory` crée la vue.
3.  Le `DataSource` (via le Driver) exécute la requête en appliquant :
    *   Le tri (`Sorting`).
    *   Les filtres (`Filtering`).
    *   La pagination.
4.  Le rendu se fait via Twig (`@SyliusUi/Grid/index.html.twig`).

## Point de Certification
Savoir que la grille est agnostique de la persistance (théoriquement), mais que 99% des cas utilisent Doctrine ORM.
Savoir que les filtres modifient la requête `DataSource` avant exécution.

