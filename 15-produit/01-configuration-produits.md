# Détails sur la configuration des produits

## Objectif
Structure de l'entité Produit.

## Product vs ProductVariant
C'est la distinction fondamentale de Sylius.

*   **Product** : Le concept abstrait / conteneur.
    *   Nom, Description, Slug (Traduisibles).
    *   Associations, Taxons, Attributs.
    *   Options (ce qui fait varier le produit).
*   **ProductVariant** : L'objet physique vendable (SKU).
    *   Prix, Stock.
    *   Code unique.
    *   Valeurs d'options (ex: Rouge, XL).

## Produit Simple vs Configurable
*   **Simple** : Sylius crée automatiquement **une** variante "par défaut" invisible en arrière-plan. L'utilisateur a l'impression de manipuler un produit simple.
*   **Configurable** : Le produit a des options (Taille, Couleur) et plusieurs variantes.

## Base de données
*   `sylius_product`
*   `sylius_product_variant`
*   `sylius_product_translation`

