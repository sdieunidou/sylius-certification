# Les provinces et leur configuration

## Objectif
Comprendre le rôle des provinces (ou états/régions) dans l'adressage Sylius et leur lien avec les pays.

## Concepts Clés

Une **Province** représente une subdivision administrative d'un pays (ex: État aux USA, Département ou Région en France).

*   **Dépendance** : Une province appartient obligatoirement à un seul Pays.
*   **Code** : Elle possède un code unique (souvent le code ISO 3166-2, ex: `US-CA` pour la Californie), mais ce format n'est pas strictement forcé par Sylius, c'est une chaîne de caractères.
*   **Nom** : Contrairement aux pays (qui utilisent Intl), les provinces ont un nom stocké en base de données.
*   **Abraviation** : Peut avoir une abréviation (ex: "CA" pour Californie).

### Classe Modèle
Interface : `Sylius\Component\Addressing\Model\ProvinceInterface`
Implémentation : `Sylius\Component\Addressing\Model\Province`

```php
interface ProvinceInterface extends CodeAwareInterface, ResourceInterface
{
    public function getName(): ?string;
    public function setName(?string $name): void;

    public function getAbbreviation(): ?string;
    public function setAbbreviation(?string $abbreviation): void;

    public function getCountry(): ?CountryInterface;
    public function setCountry(?CountryInterface $country): void;
}
```

## Configuration

### Via l'interface d'administration
Les provinces ne se créent pas dans un menu séparé, mais directement **dans la configuration du Pays**.

1.  Aller dans **Configuration > Countries**.
2.  Editer un pays (ex: United States).
3.  Une section "Provinces" permet d'ajouter dynamiquement des lignes.
4.  Pour chaque province : Code, Nom, Abréviation.

### Via Fixtures
Les provinces sont définies comme des enfants des pays dans les fixtures.

```yaml
sylius_fixtures:
    suites:
        default:
            fixtures:
                geographical:
                    options:
                        provinces:
                            'US': # Code du pays parent
                                'US-CA': 'California' # Code Province: Nom Province
                                'US-NY': 'New York'
```

## Base de Données
Table : `sylius_province`

| Colonne | Type | Description |
| :--- | :--- | :--- |
| `id` | integer | Clé primaire |
| `country_id` | foreign key | Lien vers `sylius_country`. Not Null. |
| `code` | string | Identifiant unique (ex: "US-CA"). |
| `name` | string | Nom affiché (ex: "California"). |
| `abbreviation` | string | Court (ex: "CA"). |

## Points de vigilance pour la certification
*   **Validation d'adresse** : Si un Pays possède des Provinces définies dans Sylius, le champ "Province" du formulaire d'adresse devient généralement un menu déroulant (select) obligatoire ou conditionnel selon la configuration. Si le pays n'a pas de provinces configurées, c'est souvent un champ texte libre ou absent.
*   **Unicité du code** : Le code de la province doit être unique globalement (pas seulement au sein du pays). C'est pourquoi on préfixe souvent avec le pays (ex: `US-CA` et non juste `CA`, car le Canada pourrait aussi utiliser `CA`).
*   **Resource** : La province est une Resource Sylius standard, on peut donc facilement étendre ses attributs.

## Différence entre "Province" et "Zone Member"
Ne pas confondre une Province (entité géographique physique) et un "Zone Member" (qui peut référencer une province pour définir une zone de livraison). Une Zone contient des références aux provinces, elle ne les "contient" pas physiquement.

