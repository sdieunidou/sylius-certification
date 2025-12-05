# Configuration des écouteurs (listeners) de fixtures

## Objectif
Exécuter du code avant ou après le chargement des fixtures.

## Listener
Un listener réagit aux événements du cycle de vie des fixtures (`suite_before`, `suite_after`, `fixture_before`, `fixture_after`).

## Utilité
*   **Logger** : Afficher la progression (activé par défaut).
*   **Backup** : Dumper la base avant chargement.
*   **Indexation** : Forcer la réindexation ElasticSearch après le chargement massif.
*   **Nettoyage** : Vider le dossier `/public/media` avant de charger de nouvelles images.

## Configuration

```yaml
sylius_fixtures:
    suites:
        default:
            listeners:
                my_cleanup_listener:
                    options:
                        delete_media: true
```

## Création
Implémenter `ListenerInterface`.
Taguer avec `sylius_fixtures.listener`.

```php
class MediaCleanupListener implements ListenerInterface
{
    public function getName(): string { return 'my_cleanup_listener'; }
    
    public function beforeSuite(SuiteEvent $event, array $options): void
    {
        // Supprimer les fichiers
    }
}
```

