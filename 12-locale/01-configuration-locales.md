# Configuration des locales

## Objectif
Gérer les langues disponibles.

## Entité Locale
`Sylius\Component\Locale\Model\Locale`.
*   `code` : Code ISO (fr_FR, en_US, de_DE).

## Administration
**Configuration > Locales**.
Ajouter une locale la rend disponible dans le système, mais pas forcément visible sur le site (il faut l'ajouter au Canal).

## Fixtures

```yaml
sylius_fixtures:
    suites:
        default:
            fixtures:
                locale:
                    options:
                        locales: ['fr_FR', 'en_US', 'pl_PL']
```

## Translations (Traductions)
Les entités traduisibles (Produits, Taxons) utilisent le pattern `Translatable`.
*   `Product` a une collection `translations`.
*   `ProductTranslation` contient `name`, `slug`, `description`.
Sylius utilise la locale courante pour charger automatiquement la bonne traduction via le `TranslatableListener` de Doctrine.

