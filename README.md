# Certification Sylius v2 - Guide de Révision

Ce dépôt contient des fiches pédagogiques pour la préparation à la certification Sylius (basée sur la branche v2).

> **Note** : Ce contenu a été entièrement généré par une intelligence artificielle sans vérification humaine préalable ; veuillez toujours vous référer à la documentation officielle de Sylius.

## Table des Matières

### [1. Adressage (Addressing)](./01-adressage/)
* [Les pays et leur configuration](./01-adressage/01-pays-configuration.md)
* [Les provinces et leur configuration](./01-adressage/02-provinces-configuration.md)
* [Comportement des provinces par rapport aux pays](./01-adressage/03-comportement-provinces.md)
* [Les zones et leur configuration](./01-adressage/04-zones-configuration.md)
* [Comment et où les zones sont utilisées](./01-adressage/05-utilisation-zones.md)

### [2. Panier & Tunnel de commande (Cart & Checkout)](./02-panier-tunnel-commande/)
* [Détails sur la machine à états (state machine) du checkout](./02-panier-tunnel-commande/01-state-machine-checkout.md)
* [Détails et prérequis pour chaque étape du processus de commande](./02-panier-tunnel-commande/02-etapes-checkout.md)
* [Actions possibles sur le panier dans Sylius](./02-panier-tunnel-commande/03-actions-panier.md)
* [Gestion des stocks durant le processus de commande](./02-panier-tunnel-commande/04-gestion-stocks.md)
* [Sélection des méthodes de livraison et de paiement](./02-panier-tunnel-commande/05-selection-livraison-paiement.md)
* [Comportement du carnet d'adresses durant le checkout](./02-panier-tunnel-commande/06-carnet-adresses-checkout.md)

### [3. Promotions Panier (Cart Promotion)](./03-promotions-panier/)
* [Ordre d'exécution et résultats du calcul des promotions](./03-promotions-panier/01-ordre-execution.md)
* [Configuration des promotions de panier](./03-promotions-panier/02-configuration-promotions.md)
* [Configuration des coupons](./03-promotions-panier/03-configuration-coupons.md)
* [Règles de promotion disponibles et comment les modifier/étendre](./03-promotions-panier/04-regles-promotion.md)
* [Actions de promotion disponibles et comment les modifier/étendre](./03-promotions-panier/05-actions-promotion.md)

### [4. Promotions Catalogue (Catalog Promotion)](./04-promotions-catalogue/)
* [Ordre d'exécution, résultats du calcul et comportement](./04-promotions-catalogue/01-ordre-execution-catalogue.md)
* [Configuration des promotions catalogue](./04-promotions-catalogue/02-configuration-catalogue.md)
* [Variant checkers disponibles et comment les modifier/étendre](./04-promotions-catalogue/03-variant-checkers.md)
* [Calculateurs de prix disponibles et comment les modifier/étendre](./04-promotions-catalogue/04-calculateurs-prix.md)
* [Traitement des promotions catalogue et sa configuration](./04-promotions-catalogue/05-traitement-promotions.md)

### [5. Canal (Channel)](./05-canal/)
* [Ce qui dépend des canaux](./05-canal/01-dependances-canaux.md)
* [Comment les canaux sont résolus (resolved)](./05-canal/02-resolution-canaux.md)
* [Configuration des canaux](./05-canal/03-configuration-canaux.md)

### [6. CLI (Command Line Interface)](./06-cli/)
* [Commandes Sylius et leur utilisation](./06-cli/01-commandes-sylius.md)

### [7. Devise (Currency)](./07-devise/)
* [Comment l'argent et les devises sont stockés dans Sylius](./07-devise/01-stockage-argent.md)
* [Les taux de change et leur comportement](./07-devise/02-taux-change.md)
* [Calculs monétaires et présentations](./07-devise/03-calculs-monetaires.md)
* [Configuration des devises et des taux de change](./07-devise/04-configuration-devises.md)

### [8. Extensibilité](./08-extensibilite/)
* [Étendre les modèles, repositories et factories Sylius](./08-extensibilite/01-etendre-modeles.md)
* [Étendre les contrôleurs Sylius](./08-extensibilite/02-etendre-controleurs.md)
* [Étendre les formulaires et les templates Sylius](./08-extensibilite/03-etendre-formulaires-templates.md)

### [9. Fixtures](./09-fixtures/)
* [Configuration des fixtures et comment les étendre](./09-fixtures/01-configuration-fixtures.md)
* [Fonctionnalités des fixtures](./09-fixtures/02-fonctionnalites-fixtures.md)
* [Configuration des écouteurs (listeners) de fixtures](./09-fixtures/03-ecouteurs-fixtures.md)

### [10. Général](./10-general/)
* [Licences](./10-general/01-licences.md)
* [Structure et architecture de haut niveau de Sylius](./10-general/02-structure-architecture.md)
* [Rôle des principaux composants Sylius](./10-general/03-role-composants.md)
* [Ce qui est préconfiguré selon les environnements](./10-general/04-environnements.md)
* [Dépendances actuelles de Sylius](./10-general/05-dependances.md)
* [Questions basiques sur l'API Sylius](./10-general/06-api-basique.md)
* [Utilisation générique de la machine à états](./10-general/07-machine-etats-generique.md)

### [11. Grille (Grid)](./11-grille/)
* [Comment les grilles peuvent être déclarées](./11-grille/01-declaration-grilles.md)
* [Optimisations des grilles](./11-grille/02-optimisations-grilles.md)
* [Actions de grille disponibles et extension](./11-grille/03-actions-grille.md)
* [Filtres de grille disponibles et extension](./11-grille/04-filtres-grille.md)
* [Champs de grille disponibles et extension](./11-grille/05-champs-grille.md)
* [Utilisation des grilles et drivers](./11-grille/06-utilisation-drivers.md)

### [12. Locale](./12-locale/)
* [Configuration des locales](./12-locale/01-configuration-locales.md)
* [Résolution de la locale](./12-locale/02-resolution-locale.md)

### [13. Commande (Order)](./13-commande/)
* [Détails sur les étapes du traitement d'une commande](./13-commande/01-etapes-traitement.md)
* [Comment personnaliser le traitement d'une commande](./13-commande/02-personnaliser-traitement.md)
* [Rôle de chacune des étapes du traitement](./13-commande/03-role-etapes.md)
* [États de la commande adaptés aux processeurs de commande](./13-commande/04-etats-commande.md)
* [Comportement et détails sur les ajustements de commande](./13-commande/05-ajustements-commande.md)
* [Cycle de vie de la commande après le checkout](./13-commande/06-cycle-vie-post-checkout.md)

### [14. Paiement (Payment)](./14-paiement/)
* [Machine à états des paiements](./14-paiement/01-machine-etats-paiement.md)
* [Configuration des méthodes de paiement](./14-paiement/02-configuration-methodes.md)
* [Passerelles de paiement (Payment gateways)](./14-paiement/03-passerelles-paiement.md)

### [15. Produit (Product)](./15-produit/)
* [Détails sur la configuration des produits](./15-produit/01-configuration-produits.md)
* [Détails sur la tarification des produits](./15-produit/02-tarification-produits.md)
* [Détails sur le produit et sa relation avec la taxonomie](./15-produit/03-relation-taxonomie.md)
* [Détails sur les associations de produits](./15-produit/04-associations-produits.md)
* [Détails sur les attributs de produits](./15-produit/05-attributs-produits.md)
* [Détails sur les options de produits](./15-produit/06-options-produits.md)
* [Détails sur les avis produits (reviews)](./15-produit/07-avis-produits.md)
* [Gestion et traitement des images](./15-produit/08-gestion-images.md)

### [16. Ressource (Resource)](./16-ressource/)
* [Qu'est-ce que Sylius Resource ?](./16-ressource/01-concept-resource.md)
* [Configuration de Sylius Resource](./16-ressource/02-configuration-resource.md)
* [Services disponibles et fonctionnalités par défaut](./16-ressource/03-services-resource.md)
* [Comment fonctionne la traduction des entités ?](./16-ressource/04-traduction-entites.md)
* [Création d'une Ressource pas à pas](./16-ressource/05-creation-resource.md)

### [17. Livraison (Shipping)](./17-livraison/)
* [Configuration des méthodes de livraison](./17-livraison/01-configuration-livraison.md)
* [Calculateurs de frais de port](./17-livraison/02-calculateurs-livraison.md)
* [Rule checkers de livraison](./17-livraison/03-rules-livraison.md)
* [Machine à états de la livraison](./17-livraison/04-machine-etats-livraison.md)

### [18. Boutique (Shop)](./18-boutique/)
* [Envoi d'emails aux clients](./18-boutique/01-emails-clients.md)
* [Utilisateurs de la boutique (Shop Users) vs Clients (Customers)](./18-boutique/02-users-vs-customers.md)

### [19. Taxation](./19-taxation/)
* [Taxation des commandes, articles et expéditions](./19-taxation/01-taxation-objets.md)
* [Logique de calcul des taxes](./19-taxation/02-logique-calcul.md)

### [20. Tests (Testing)](./20-tests/)
* [Types de tests dans Sylius](./20-tests/01-types-tests.md)
* [Utilitaires de test dans Sylius](./20-tests/02-utilitaires-tests.md)
