# Les pays et leur configuration

## Objectif
Comprendre comment Sylius gère les pays, qui sont l'entité racine pour la configuration géographique, la livraison et la taxation.

## Concepts Clés

Dans Sylius, un **Pays** (`Country`) représente une nation vers laquelle la boutique peut expédier ou facturer.

*   **Code ISO** : Chaque pays est identifié de manière unique par un code ISO 3166-1 alpha-2 (ex: `FR`, `US`, `DE`).
*   **Toggleable** : Un pays peut être activé ou désactivé. S'il est désactivé, il n'apparaîtra pas dans le checkout ou les formulaires d'adresse.
*   **Provinces** : Un pays peut contenir une collection de provinces (voir fiche dédiée).

### Classe Modèle
L'interface principale est `Sylius\Component\Addressing\Model\CountryInterface`.
L'implémentation par défaut est `Sylius\Component\Addressing\Model\Country`.

```php
// Exemple simplifié de l'interface
interface CountryInterface extends CodeAwareInterface, ToggleableInterface, TimestampableInterface
{
    public function getCode(): ?string;
    public function setCode(?string $code): void;
    
    public function getProvinces(): Collection;
    public function hasProvince(ProvinceInterface $province): bool;
    public function addProvince(ProvinceInterface $province): void;
    public function removeProvince(ProvinceInterface $province): void;
}
```

## Configuration

Les pays sont généralement gérés via le panneau d'administration ou chargés via des fixtures.

### Via l'interface d'administration
1.  Aller dans **Configuration > Countries**.
2.  Cliquer sur **Create**.
3.  Sélectionner le code pays (la liste est fournie par le bundle `symfony/intl`).
4.  Activer le pays via le toggle "Enabled".

### Via Fixtures (YAML)
Pour initialiser des pays lors de l'installation :

```yaml
sylius_fixtures:
    suites:
        default:
            listeners:
                logger: ~
            fixtures:
                geographical:
                    options:
                        countries:
                            - 'FR'
                            - 'US'
                            - 'DE'
                            - 'PL'
```

Ou avec une configuration plus détaillée (si vous utilisez une suite personnalisée) :

```yaml
sylius_fixtures:
    suites:
        default:
            fixtures:
                addressing:
                    options:
                        custom:
                            countries:
                                - code: "FR"
                                  enabled: true
                                - code: "US"
                                  enabled: true
                                  provinces: # Voir fiche Provinces
                                      - "US-CA"
```

## Base de Données
Table : `sylius_country`

| Colonne | Type | Description |
| :--- | :--- | :--- |
| `id` | integer | Clé primaire |
| `code` | string | Code ISO (ex: "FR"). Unique. |
| `enabled` | boolean | Statut d'activation. |

## Points de vigilance pour la certification (v2)
*   **Immutabilité du code** : Une fois créé, le code ISO d'un pays ne devrait pas changer car il sert d'identifiant métier.
*   **Relation avec les Zones** : Un pays ne fait *pas* automatiquement partie d'une zone. Vous devez explicitement ajouter le pays à une Zone (type "Country") pour qu'il soit utilisable dans les règles de livraison ou de taxation.
*   **Traductions** : Le nom du pays affiché à l'utilisateur ne vient pas de la base de données `sylius_country`, mais du composant `Intl` de Symfony, basé sur la locale de l'utilisateur. Sylius ne stocke que le Code ISO.

## Exemple de code (Récupération)

```php
/** @var RepositoryInterface $countryRepository */
$countryRepository = $container->get('sylius.repository.country');

// Trouver par code ISO
/** @var CountryInterface|null $france */
$france = $countryRepository->findOneBy(['code' => 'FR']);

if ($france && $france->isEnabled()) {
    // Logique métier
}
```

