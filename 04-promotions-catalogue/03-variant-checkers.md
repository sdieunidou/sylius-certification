# "Variant checkers" disponibles et extension

## Objectif
Comprendre comment Sylius sélectionne les variantes éligibles (Scopes).

## Scopes Natifs (Scope Providers)

Sylius détermine quelles variantes sont visées par la promotion via des `ScopeProvider` ou `VariantChecker`.
Les types natifs sont :

1.  `for_variants` : Liste explicite de codes de variantes.
2.  `for_products` : Liste de produits (toutes leurs variantes sont impactées).
3.  `for_taxons` : Liste de taxons (tous les produits de cette catégorie sont impactés).

## Créer un Scope Personnalisé

Exemple : "Tous les produits dont l'attribut 'Matière' est 'Coton'".

### 1. Créer le Provider
Il doit retourner une requête ou une liste de variantes.

Implémenter `InForProductScopeVariantCheckerInterface` (ou similaire selon l'architecture v2 qui utilise souvent des `QueryBuilder`).

Dans Sylius v2, le système repose beaucoup sur la sélection par lot.
Il faut implémenter un `ScopeEffectivenessCheckerInterface` (pour vérifier si une promo s'applique à une variante donnée) et un Provider pour lister les variantes lors du calcul global.

### 2. Enregistrement
Tag : `sylius.catalog_promotion.scope_provider`.

```yaml
services:
    app.catalog_promotion_scope.material:
        class: App\Promotion\Scope\MaterialScope
        tags:
            - { name: sylius.catalog_promotion.scope_provider, type: for_material, label: "Material" }
```

### 3. FormType
Pour choisir la matière "Coton" dans l'admin.

