# Traitement des promotions catalogue et sa configuration

## Objectif
Comprendre l'architecture technique derrière l'application des promos catalogue (Performance & Asynchronisme).

## Architecture Event-Driven

Le recalcul total des prix est une opération coûteuse (O(n) où n = nombre de produits). Elle ne peut pas se faire en temps réel lors de la requête HTTP de sauvegarde.

1.  **Event** : `CatalogPromotionUpdated`
2.  **Listener** : `CatalogPromotionEventListener`
3.  **Message Dispatch** : Envoie un message `ProcessCatalogPromotion` dans le bus Symfony Messenger.
4.  **Handler** : `ProcessCatalogPromotionHandler`
    *   Calcule les variantes impactées.
    *   Met à jour `sylius_channel_pricing`.

## États de la Promotion

Une promotion catalogue a un champ `state` :
*   `inactive` : Pas prête ou désactivée.
*   `processing` : En cours de calcul.
*   `active` : Calculée et appliquée.

Si une promo est en `processing`, l'admin peut voir un loader ou un statut.

## Configuration des Batches

Pour éviter de saturer la mémoire, le traitement se fait par lots (batches).
On peut configurer la taille des lots (ex: 100 variantes à la fois) dans la configuration du bundle.

## Points de Certification
*   Savoir que `sylius_channel_pricing` est la table modifiée.
*   Comprendre pourquoi on utilise Messenger (perf).
*   Savoir que si `originalPrice` est null, il prend la valeur du `price` avant la toute première promo.
*   Savoir comment réinitialiser : Désactiver la promo déclenche un processus inverse qui restaure les prix originaux.

