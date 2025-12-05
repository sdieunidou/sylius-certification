# Ordre d'exécution, résultats et comportement

## Objectif
Comprendre la différence fondamentale entre Promotion Panier (Cart) et Promotion Catalogue.

## Documentation Officielle
*   [Catalog Promotions Guide](https://docs.sylius.com/en/latest/book/products/catalog_promotions.html)

## Concept
Une **Promotion Catalogue** modifie le prix d'une variante de produit **avant** qu'elle ne soit mise au panier.
Elle s'applique au catalogue produit directement.
*   *Exemple* : "Tout le rayon T-Shirt à -20%".
*   Le client voit le prix barré (Original Price) et le nouveau prix sur la page produit.

## Processus Asynchrone

Contrairement aux promos panier (calculées à la volée), les promos catalogue sont **pré-calculées**.
Vu qu'elles peuvent affecter des milliers de produits, le calcul est lourd.

1.  **Configuration** : L'admin crée la promo.
2.  **Dispatch** : Un événement est lancé.
3.  **Traitement (Processor)** : Le `CatalogPromotionProcessor` identifie les variantes impactées.
4.  **Application** : Le prix est modifié dans la table `sylius_channel_pricing`.
    *   `price` : Devient le nouveau prix réduit.
    *   `originalPrice` : Stocke l'ancien prix (pour l'affichage barré).
    *   `appliedPromotions` : Stocke la liste des promos appliquées (JSON).

## Résultat
Le prix en base de données EST modifié.
Lorsqu'on ajoute le produit au panier, c'est ce nouveau prix qui est utilisé comme base. Les promos panier s'appliqueront *par dessus* ce prix déjà réduit.

## Ordre d'exécution (Priorité)
Comme pour le panier, la `priority` détermine l'ordre.
Si deux promos catalogue s'appliquent (-10% et -5€) :
1.  Prix initial : 100€.
2.  Promo A (-10%) : Nouveau prix 90€.
3.  Promo B (-5€) : Nouveau prix 85€.

## Délai de mise à jour
Dans une architecture avec des queues (Messenger), il peut y avoir un délai entre la sauvegarde de la promo et l'affichage du nouveau prix sur le site.

