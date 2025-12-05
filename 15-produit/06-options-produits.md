# Détails sur les options de produits

## Objectif
Créer des variantes (Taille, Couleur).

## Option
Entité `ProductOption`.
*   Code : `size`.
*   Values : `S`, `M`, `L`, `XL`.

## ProductOptionValue
Les valeurs possibles pour une option.
*   Code : `size_s`.
*   Value : `Small`.

## Fonctionnement
1.  On assigne des Options à un Produit (ex: Ce T-Shirt a l'option Taille).
2.  On crée des Variantes.
3.  Chaque Variante doit définir une Valeur pour chaque Option du Produit.
    *   Variante 1 : Taille = S.
    *   Variante 2 : Taille = M.

## Unicité
La combinaison des valeurs d'option doit être unique par produit. On ne peut pas avoir deux variantes "Taille S" pour le même T-Shirt.

