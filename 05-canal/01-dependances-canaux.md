# Ce qui dépend des canaux

## Objectif
Le Canal (`Channel`) est le point central de la configuration contextuelle. Il faut savoir exactement ce qui change quand on change de canal.

## Définition
Un Canal représente un point d'accès à la boutique : Site Web FR, Site Web US, Application Mobile, Point de Vente Physique (POS).

## Ce qui est configuré PAR Canal

1.  **Produits (Activé/Désactivé)** : Un produit peut être vendu sur le canal Web mais pas sur le Mobile.
2.  **Prix (Pricing)** : La table `sylius_channel_pricing` stocke le prix par variante ET par canal.
    *   Un T-Shirt peut coûter 20€ sur le canal FR et 25$ sur le canal US.
3.  **Devise (Currency)** :
    *   **Base Currency** : La devise de référence pour ce canal.
    *   **Supported Currencies** : Les devises dans lesquelles le client peut payer.
4.  **Locale (Langue)** :
    *   **Default Locale** : Langue par défaut.
    *   **Supported Locales** : Langues disponibles.
5.  **Zones & Taxes** : Le calcul des taxes peut dépendre de la zone par défaut du canal (pour l'affichage des prix TTC/HT).
6.  **Méthodes de Paiement & Livraison** : Chaque méthode est activée ou non par canal.
7.  **Thème (Theme)** : Le design (Twig templates) peut changer selon le canal (ex: Thème Noël vs Thème Standard).
8.  **Menu (Taxons)** : On peut définir un taxon racine différent par canal (ex: Menu Homme pour un site dédié Homme).
9.  **Emails** : L'expéditeur des emails (contact@maboutique.fr) est configuré par canal.

## Ce qui est GLOBAL (ne dépend PAS du canal)
*   **L'Utilisateur (ShopUser)** : Un compte client est global à l'instance Sylius (sauf personnalisation). Il peut se connecter sur tous les canaux.
*   **Les Attributs Produit** : La définition des attributs (ex: Couleur) est globale.
*   **L'Inventory (Stock)** : Par défaut, le stock est global (sauf si Multi-Inventory Plugin).

