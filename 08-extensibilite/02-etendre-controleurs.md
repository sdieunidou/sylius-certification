# Étendre les contrôleurs Sylius

## Objectif
Modifier le comportement HTTP.

## Approche ResourceController
Sylius utilise `SyliusResourceBundle` qui génère des contrôleurs dynamiques basés sur la config.
La plupart des routes pointent vers `sylius.controller.product:indexAction` (par exemple).

## Méthode 1 : Surcharge de configuration (Routing)
Si vous voulez juste changer le template ou ajouter un critère de tri.
Dans `routes.yaml` :

```yaml
sylius_shop_product_index:
    path: /products/
    methods: [GET]
    defaults:
        _controller: sylius.controller.product:indexAction
        _sylius:
            template: "@SyliusShop/Product/index.html.twig"
            repository:
                method: createQueryBuilderByChannelAndTaxon
                arguments: [expr:service('sylius.context.channel').getChannel(), $taxon]
            paginate: 9
```
Modifiez simplement cette config.

## Méthode 2 : Décoration ou Surcharge de Classe
Si vous devez changer la logique PHP (ex: appel API externe avant affichage).

1.  Créer `App\Controller\ProductController` qui étend `Sylius\Bundle\ResourceBundle\Controller\ResourceController`.
2.  Surcharger la méthode (ex: `showAction`).
3.  Enregistrer la classe dans `sylius_product.yaml` -> `classes: controller: App\Controller\ProductController`.

## Méthode 3 : Route Personnalisée
Souvent le plus simple pour une nouvelle fonctionnalité.
Créez un contrôleur Symfony standard et définissez votre propre route, en utilisant les services Sylius (Repositories, Factories) injectés.

