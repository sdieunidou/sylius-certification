# Taxation des commandes, articles et expéditions

## Objectif
Comprendre l'application de la TVA.

## Application
Les taxes s'appliquent à 3 niveaux :
1.  **Items (Produits)** : Selon la `TaxCategory` du produit.
2.  **Shipping (Livraison)** : Selon la `TaxCategory` de la méthode de livraison.
3.  **Order (Global)** : Rarement utilisé direct, somme des deux précédents.

## Included in Price
Concept crucial.
*   Si "Included in price" est **activé** (B2C Europe) : Le prix affiché (120€) inclut la taxe. Sylius *extrait* la taxe pour le reporting (100€ + 20€).
*   Si "Included in price" est **désactivé** (B2B ou US) : Le prix affiché (100€) est HT. Sylius *ajoute* la taxe au total (100€ + 20€ = 120€).

Ceci est configuré par **Groupe de Taxe** (TaxRate).

