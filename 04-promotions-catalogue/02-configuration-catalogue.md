# Configuration des promotions catalogue

## Objectif
Paramétrer une réduction catalogue via l'admin ou YAML.

## Structure

Entité : `Sylius\Component\Core\Model\CatalogPromotion`.

*   **Code / Nom**
*   **Channels**
*   **Scopes** (Portée) : "À QUOI ça s'applique ?" (ex: Variantes, Taxons).
*   **Actions** : "QUEL EST l'effet ?" (ex: -20%).
*   **État** : Active / Inactive.
*   **Dates** : Start / End.

> **Note** : Contrairement aux promos panier qui utilisent des "Rules", le catalogue utilise des "Scopes".

## Configuration Admin

**Marketing > Catalog Promotions**

1.  **Scope** :
    *   `For Taxons` : Sélectionner "T-Shirts".
    *   `For Variants` : Sélectionner des SKU spécifiques.
    *   `For Products` : Sélectionner des produits entiers.
2.  **Action** :
    *   `Percentage discount` : -20%.
    *   `Fixed discount` : -10 EUR.

## Exemple YAML (Fixtures)

```yaml
sylius_fixtures:
    suites:
        default:
            fixtures:
                catalog_promotion:
                    options:
                        custom:
                            summer_tshirts:
                                code: "SUMMER_TSHIRTS"
                                name: "Summer T-Shirts Sale"
                                scopes:
                                    - type: for_taxons
                                      configuration:
                                          taxons: ["t_shirts"]
                                actions:
                                    - type: percentage_discount
                                      configuration:
                                          amount: 0.2 # 20%
```

## Indexation
Après avoir créé ou modifié une promo catalogue, si le worker asynchrone ne tourne pas, les prix ne changent pas.
Commande CLI pour forcer le recalcul :
`bin/console sylius:process-catalog-promotions`

