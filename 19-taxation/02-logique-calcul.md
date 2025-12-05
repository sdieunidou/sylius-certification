# Logique de calcul des taxes

## Objectif
Comment le taux est choisi.

## TaxRateResolver
1.  Détermine la **Zone** fiscale (basée sur l'adresse de livraison ou de facturation selon config).
2.  Cherche un **TaxRate** qui matche :
    *   La `TaxCategory` de l'objet.
    *   La `Zone` déterminée.

## TaxCalculationStrategy
Définit comment on arrondit.
*   **OrderItemsBased** : Calcule la taxe sur chaque ligne, arrondit, puis somme. (Méthode par défaut).
*   **OrderBased** : Somme les montants HT, calcule la taxe sur le total, arrondit.

Cela peut créer des différences de 1 ou 2 centimes.

## Extensibilité
On peut créer son propre calculateur (ex: TaxJar, Avalara pour les US) en implémentant `TaxCalculatorInterface` et en remplaçant le service par défaut.

