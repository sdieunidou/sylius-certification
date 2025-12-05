# Configuration des devises et taux

## Objectif
Configurer le système monétaire.

## Admin
1.  **Configuration > Currencies** : Ajouter les devises supportées par le système (Codes ISO).
2.  **Configuration > Exchange Rates** : Définir les ratios entre paires.

## Fixtures

```yaml
sylius_fixtures:
    suites:
        default:
            fixtures:
                currency:
                    options:
                        currencies: ['USD', 'EUR', 'GBP']
                exchange_rate:
                    options:
                        rates:
                            EUR: # Source
                                USD: 1.12 # Target: Ratio
                                GBP: 0.85
```

## Le Provider
Le `CurrencyProvider` détermine quelle est la devise courante :
1.  Celle choisie par l'utilisateur (stockée en session `_currency`).
2.  Sinon, la devise par défaut du Canal.

## Changer la devise par défaut
Changer la devise par défaut d'un canal (`baseCurrency`) est lourd de conséquences car tous les prix saisis (`sylius_channel_pricing`) sont supposés être dans cette devise. Sylius ne convertit pas les prix en base lors d'un changement de config.

