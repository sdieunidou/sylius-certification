# Détails sur les avis produits (reviews)

## Objectif
Gestion de la preuve sociale.

## Modèle
*   **Reviewer** : L'auteur (Customer ou invité).
*   **Rating** : Note (1-5).
*   **Title, Comment**.
*   **Status** : `new`, `accepted`, `rejected`.

## Workflow
Par défaut, les avis doivent être approuvés par l'admin avant d'apparaître sur le site (Machine à états `sylius_product_review`).

## Configuration
On peut désactiver les avis dans `sylius_core.yaml` (rare).
On peut étendre le modèle pour ajouter des photos dans les avis.

