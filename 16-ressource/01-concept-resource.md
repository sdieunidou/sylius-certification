# Qu'est-ce que Sylius Resource ?

## Objectif
Comprendre la philosophie "Resource" qui structure tout Sylius.

## Documentation Officielle
*   [Resource Bundle Documentation](https://docs.sylius.com/en/latest/components_and_bundles/bundles/SyliusResourceBundle/index.html)

## Concept
`SyliusResourceBundle` est un bundle autonome (utilisable hors Sylius E-commerce) qui fournit une couche d'abstraction pour gérer les entités PHP (CRUD).

Au lieu de réécrire manuellement Controller, Repository, Factory pour chaque entité, on déclare une "Ressource" et le bundle génère tout dynamiquement.

## Métadonnées
Une ressource est définie par :
*   Un nom d'application (`sylius`, `app`).
*   Un nom de ressource (`product`, `supplier`).
*   Une classe de modèle (`App\Entity\Supplier`).
*   (Optionnel) Des classes spécifiques pour Controller, Repository, Factory, Form.

L'alias complet est `app.supplier`.

