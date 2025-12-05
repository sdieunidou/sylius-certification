# Détails sur les associations de produits

## Objectif
Cross-selling et Up-selling.

## Documentation Officielle
*   [Product Associations](https://docs.sylius.com/en/latest/book/products/associations.html)

## AssociationType
On définit d'abord des types d'association :
*   "Produits similaires" (`similar`)
*   "Accessoires" (`accessories`)
*   "Alternative" (`alternatives`)

## ProductAssociation
Lie un produit A à une liste de produits B, C, D sous un type donné.

*   **Owner** : Produit A.
*   **Type** : Accessoires.
*   **Associated Products** : Collection [B, C, D].

## Utilisation
Dans le template produit :
```twig
{% set accessories = product.getAssociations('accessories') %}
{% for association in accessories %}
    {% for associatedProduct in association.associatedProducts %}
        ...
    {% endfor %}
{% endfor %}
```

