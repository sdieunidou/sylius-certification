# Gestion et traitement des images

## Objectif
Gérer les médias produits.

## ProductImage
Étend `ImageInterface`.
*   **File** : Le fichier uploadé (Virtual).
*   **Path** : Le chemin stocké en BDD.
*   **Type** : Catégorie d'image (`main`, `thumbnail`, `banner`).

## Variantes
Une image peut être liée :
*   Soit au Produit entier (pour toutes les variantes).
*   Soit à des Variantes spécifiques (ex: Photo du T-Shirt Rouge liée à la variante Rouge).

## LiipImagineBundle
Sylius utilise `LiipImagineBundle` pour le redimensionnement à la volée et le cache des thumbnails.
Les filtres (`sylius_shop_product_thumbnail`, etc.) sont définis dans `config/packages/liip_imagine.yaml`.

## Stockage
Géré par `Flysystem` (via Gaufrette historiquement, ou Flysystem direct en v2).
Permet de stocker sur S3, Local, Azure facilement.

