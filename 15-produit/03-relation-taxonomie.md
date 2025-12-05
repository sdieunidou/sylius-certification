# Détails sur le produit et sa relation avec la taxonomie

## Objectif
Organiser le catalogue.

## Taxons
Sylius utilise un système d'arbre unique : `Taxonomy` (obsolète/unifié dans le concept) -> `Taxon`.
En pratique v2 : On manipule des **Taxons**.

*   Arborescence : Un taxon a un `parent` et des `children`.
*   Codes : `CATEGORY`, `T_SHIRTS`, `MEN_T_SHIRTS`.
*   Slug : `category/t-shirts/men`.

## ProductTaxon
La relation est **Many-to-Many** mais via une entité de jointure explicite `ProductTaxon`.
Cela permet de définir un **ordre** (position) du produit *dans* cette catégorie spécifique.

*   Un produit peut être dans "Nouveautés" (Position 1) et "T-Shirts" (Position 50).
*   **Main Taxon** : Champ spécial sur le produit pour définir sa "catégorie principale" (utile pour le fil d'ariane / breadcrumb).

## Menu
Le menu principal de Sylius est généralement généré à partir d'un Taxon racine (souvent code `MENU` ou `CATEGORY`).

