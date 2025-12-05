# Configuration des promotions de panier

## Objectif
Savoir configurer une promotion standard via l'admin ou le code.

## Concepts Clés

Une `Promotion` est définie par :
*   **Code / Nom** : Identifiants.
*   **Canaux** : Sur quels canaux elle s'applique.
*   **Règles (Rules)** : Les conditions *sine qua non* ("SI le panier...").
*   **Actions** : L'effet de la promo ("ALORS réduction de...").
*   **Dates** : Début / Fin.
*   **Usage Limit** : Nombre max d'utilisations globales ou par client.
*   **Priorité** : Entier (par défaut 0).
*   **Coupon based** : Si vrai, nécessite un code coupon (voir fiche suivante).

## Configuration Admin

**Marketing > Promotions**

Le formulaire est dynamique :
1.  Ajouter une règle (ex: Item Total).
2.  Configurer la règle (ex: > 50 EUR).
3.  Ajouter une action (ex: Order fixed discount).
4.  Configurer l'action (ex: -10 EUR).

## Configuration Fixtures (YAML)

```yaml
sylius_fixtures:
    suites:
        default:
            fixtures:
                promotion:
                    options:
                        custom:
                            christmas_sale:
                                name: "Christmas Sale"
                                code: "CHRISTMAS_2025"
                                channels: ["US_WEB"]
                                priority: 10
                                rules:
                                    - type: item_total
                                      configuration:
                                          WEB_US: 
                                              amount: 10000 # 100.00 USD
                                actions:
                                    - type: order_fixed_discount
                                      configuration:
                                          WEB_US:
                                              amount: 2000 # 20.00 USD
```

## Points de vigilance
*   **Cumul** : Par défaut, les promotions se cumulent sauf si l'une d'elles est exclusive.
*   **Canaux** : Une promotion configurée sans canal ne s'appliquera jamais.
*   **Devises** : Les montants (règles et actions) doivent être configurés pour *chaque* devise supportée par le canal.

