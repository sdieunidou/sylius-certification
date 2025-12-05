# Optimisations des grilles

## Objectif
Éviter les problèmes de performance (N+1 queries) dans les listes.

## Repository Method
Au lieu de laisser la grille faire un `findAll()`, on définit une méthode de repository optimisée.

```yaml
sylius_grid:
    grids:
        app_admin_product:
            driver:
                options:
                    class: App\Entity\Product
                    repository:
                        method: createListQueryBuilder
                        arguments: ["expr:service('sylius.context.channel').getChannel()"]
```

Dans le Repository :
```php
public function createListQueryBuilder(ChannelInterface $channel): QueryBuilder
{
    return $this->createQueryBuilder('p')
        ->addSelect('translation')
        ->leftJoin('p.translations', 'translation')
        ->andWhere(':channel MEMBER OF p.channels')
        ->setParameter('channel', $channel);
}
```
Le `addSelect` et `leftJoin` sont cruciaux pour charger les données liées en une seule requête ("Eager Loading").

## Pagination
Configurer `limits` pour ne pas charger trop d'éléments par défaut.
```yaml
limits: [10, 25, 50]
```

