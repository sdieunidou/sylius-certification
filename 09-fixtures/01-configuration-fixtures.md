# Configuration des fixtures et comment les étendre

## Objectif
Peupler la base de données avec des données de test ou initiales.

## SyliusFixturesBundle
Sylius utilise son propre bundle au-dessus de `DoctrineFixturesBundle` pour offrir une configuration YAML flexible.

## Structure YAML

Fichier `config/packages/sylius_fixtures.yaml` :

```yaml
sylius_fixtures:
    suites:
        default: # Nom de la suite
            listeners:
                logger: ~ # Active les logs
            fixtures:
                user: # Nom de la fixture (alias du service)
                    options:
                        custom: # Options passées au Loader
                            my_user:
                                username: "test"
                                password: "test"
```

## Créer une Fixture Personnalisée

1.  **Classe Fixture** : Étend `AbstractFixture` (implémente `FixtureInterface`).
    *   Définit le nom (`getName()`).
    *   Injecte le `ExampleFactory` ou le Manager.
2.  **Enregistrement** : Tag `sylius_fixtures.fixture`.

```php
class SupplierFixture extends AbstractFixture implements FixtureInterface
{
    public function getName(): string { return 'supplier'; }

    public function load(array $options): void
    {
        // Appel à un service qui crée les données
        $this->supplierExampleFactory->create($options);
    }

    protected function configureOptionsNode(ArrayNodeDefinition $optionsNode): void
    {
        $optionsNode
            ->children()
                ->arrayNode('suppliers')...
    }
}
```

