# Configuration des canaux

## Objectif
Savoir créer et paramétrer un canal complet.

## Classe Modèle
Interface : `Sylius\Component\Core\Model\ChannelInterface`.
Étend `Sylius\Component\Channel\Model\ChannelInterface`.

## Champs Clés

*   `code` : Identifiant unique (ex: `WEB_US`). Immuable.
*   `name` : Nom affiché.
*   `hostname` : Domaine (ex: `us.store.com`).
*   `color` : Couleur pour l'admin (visuel).
*   `enabled` : Actif ou non.

### Configuration Monétaire
*   `baseCurrency` : La devise pivot. Tous les prix en base (`channel_pricing`) sont saisis dans cette devise pour ce canal.
*   `currencies` : Les devises d'affichage (conversion automatique via taux de change).

### Configuration Locale
*   `defaultLocale` : Langue par défaut.
*   `locales` : Langues traductibles.

### Configuration Shop
*   `menuTaxon` : La racine du menu principal.
*   `contactEmail` : Pour les notifications.
*   `themeName` : Nom logique du thème (si SyliusThemeBundle installé).
*   `shopBillingData` : Adresse de l'entreprise affichée sur les factures de ce canal.

## Fixtures

```yaml
sylius_fixtures:
    suites:
        default:
            fixtures:
                channel:
                    options:
                        custom:
                            us_web:
                                code: "WEB_US"
                                name: "United States"
                                url: "us.store.com"
                                base_currency: "USD"
                                currencies: ["USD"]
                                default_locale: "en_US"
                                locales: ["en_US", "es_US"]
                                operating_countries: ["US"]
                                tax_calculation_strategy: "order_items_based"
```

## Point Certification
*   La suppression d'un canal est possible mais dangereuse si des commandes y sont liées.
*   Changer la `baseCurrency` d'un canal existant est très complexe (recalcul de tous les prix nécessaire), il est conseillé de créer un nouveau canal.

