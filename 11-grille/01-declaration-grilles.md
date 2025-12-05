# Comment les grilles peuvent être déclarées

## Objectif
Créer des listes de données filtrables et triables dans l'admin.

## Documentation Officielle
*   [Grid Bundle Documentation](https://docs.sylius.com/en/latest/components_and_bundles/bundles/SyliusGridBundle/index.html)

## Format de déclaration
Les grilles sont configurées en YAML (recommandé) ou PHP.
Fichier : `config/packages/sylius_grid.yaml`.

## Structure de base

```yaml
sylius_grid:
    grids:
        app_admin_supplier:
            driver:
                name: doctrine/orm
                options:
                    class: App\Entity\Supplier
            sorting:
                name: asc
            fields:
                name:
                    type: string
                    label: app.ui.name
            actions:
                main:
                    create:
                        type: create
                item:
                    update:
                        type: update
                    delete:
                        type: delete
            filters:
                search:
                    type: string
                    options:
                        fields: [name, email]
```

## Héritage
On peut étendre une grille existante pour ne pas tout réécrire.
Exemple : Ajouter une colonne à la grille des produits.
```yaml
sylius_grid:
    grids:
        sylius_admin_product:
            fields:
                my_new_field:
                    type: string
                    position: 1
```

