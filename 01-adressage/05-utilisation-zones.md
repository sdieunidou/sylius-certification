# Comment et où les zones sont utilisées

## Objectif
Comprendre les applications pratiques des Zones dans l'écosystème Sylius pour configurer correctement une boutique.

## 1. Livraison (Shipping)

C'est l'utilisation la plus courante. Les méthodes de livraison sont restreintes par zone.

*   **Disponibilité** : Une méthode de livraison (ex: "Colissimo France") est configurée pour appartenir à une Zone spécifique (ex: "France").
*   **Résolution** : Lors du checkout, à l'étape "Shipping", Sylius :
    1.  Prend l'adresse de livraison saisie.
    2.  Utilise le `ZoneMatcher` pour trouver toutes les zones auxquelles l'adresse appartient.
    3.  Filtre les méthodes de livraison disponibles : seules celles dont la zone correspond à l'une des zones de l'adresse sont affichées.

> **Cas pratique** : Si un client habite aux USA, il ne verra pas la méthode "Chronopost France" si celle-ci est configurée sur la Zone "France".

## 2. Taxation (Taxation)

Les taxes sont appliquées en fonction de la destination (et parfois de l'origine, selon la configuration fiscale).

*   **Taux de Taxe (Tax Rate)** : Un taux de taxe lie une **Catégorie de Taxe** (ex: "TVA Vêtements") à une **Zone** (ex: "Union Européenne") et définit un pourcentage.
*   **Calcul** :
    1.  Le `OrderTaxationProcessor` analyse chaque article du panier.
    2.  Il détermine la catégorie de taxe du produit.
    3.  Il demande au `TaxRateResolver` le taux applicable pour cette catégorie et l'adresse de livraison (donc la Zone).
    4.  Si l'adresse est dans la Zone "EU", le taux correspondant est appliqué.

## 3. Promotions (Promotions)

Les zones ne sont pas directement liées aux promotions dans le modèle de base (contrairement à Shipping/Tax), **MAIS** :

*   On peut créer des **Règles de Promotion** basées sur l'adresse de livraison ("Shipping country is...").
*   Bien que l'interface par défaut propose souvent "Shipping Country", il est possible d'étendre cela pour utiliser des Zones complexes via un RuleChecker personnalisé si besoin.

## 4. Canaux (Channels) - Indirectement

Un Canal (`Channel`) définit un ensemble de pays activés, mais ne pointe pas directement vers une zone. Cependant, pour simplifier la gestion, on configure souvent les pays d'un canal pour qu'ils correspondent aux zones de livraison définies.

## Exemple de Flux Complet (Zone Matcher)

Imaginons une commande vers **Paris, France**.

1.  **Adresse** : Country=FR.
2.  **Zones existantes** :
    *   Zone A (France) : Membres [FR]
    *   Zone B (Europe) : Membres [FR, DE, ES...]
    *   Zone C (USA) : Membres [US]
3.  **ZoneMatcher** :
    *   `match(address)` retournera Zone A et Zone B.
4.  **Shipping** :
    *   Méthode "La Poste" (Zone A) -> **Affichée**.
    *   Méthode "DHL Europe" (Zone B) -> **Affichée**.
    *   Méthode "USPS" (Zone C) -> **Masquée**.
5.  **Taxes** :
    *   Taux TVA 20% (Zone A) -> **Prioritaire** (si configuré avec la logique "included in").

## Code : Utiliser le ZoneMatcher

```php
public function checkZone(AddressInterface $address): void 
{
    /** @var ZoneMatcherInterface $matcher */
    $matcher = $this->container->get('sylius.zone_matcher');

    // Trouver TOUTES les zones
    $zones = $matcher->matchAll($address);

    // Trouver UNE zone (souvent la plus appropriée selon le scope)
    $shippingZone = $matcher->match($address, Scope::SHIPPING);

    foreach ($zones as $zone) {
        echo "L'adresse est dans la zone : " . $zone->getName();
    }
}
```

