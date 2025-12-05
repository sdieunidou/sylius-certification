# Filtres de grille disponibles et extension

## Objectif
Permettre la recherche et le filtrage.

## Filtres Natifs
*   `string` : Recherche textuelle (LIKE %).
*   `boolean` : Oui/Non.
*   `date` : Date range.
*   `entity` : Select box d'une entité liée.
*   `money` : Montant (Greater than, Less than).
*   `select` : Liste de choix statiques.

## Créer un Filtre Personnalisé

Exemple : Filtrer par "Produits ayant au moins X images".

1.  **Classe PHP** : Implémenter `FilterInterface`.
    ```php
    public function apply(DataSourceInterface $dataSource, string $name, $data, array $options): void
    {
        // $dataSource est un wrapper autour du QueryBuilder
        $dataSource->restrict($dataSource->getExpressionBuilder()->greaterThan('imagesCount', $data));
    }
    ```
2.  **Service** : Tag `sylius.grid_filter`.
3.  **Template** : Si le formulaire de filtre a besoin d'un UI spécial.

## Configuration

```yaml
filters:
    has_images:
        type: min_images_count
        label: Minimum Images
```

