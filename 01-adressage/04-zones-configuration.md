# Les zones et leur configuration

## Objectif
Maîtriser le concept de **Zone**, qui est l'unité fondamentale pour appliquer des règles de gestion (frais de port, taxes, promotions) à des zones géographiques.

## Documentation Officielle
*   [Zones Guide](https://docs.sylius.com/en/latest/book/addresses/zones.html)

## Concepts Clés

Une **Zone** est un regroupement virtuel d'entités géographiques. Elle ne correspond pas forcément à une frontière physique officielle, mais à une frontière "business".

### Types de Zones (`type`)

Une zone ne peut contenir qu'un seul type de membres. Le type est défini à la création de la zone et ne peut (théoriquement) pas changer.

1.  **Country Zone (`country`)** : Contient une liste de **Pays** entiers.
    *   *Exemple* : "Union Européenne", "Amérique du Nord".
2.  **Province Zone (`province`)** : Contient une liste de **Provinces** spécifiques.
    *   *Exemple* : "Côte Ouest US" (CA, OR, WA), "Îles Canaries".
3.  **Zone Zone (`zone`)** : Contient d'autres **Zones**. C'est un regroupement de zones.
    *   *Exemple* : "Monde" (qui contiendrait "Europe", "Asie", "Amériques").
    *   *Attention* : Éviter les boucles infinies (Zone A contient Zone B qui contient Zone A).

### Scope (Portée)

Le champ `scope` permet de filtrer l'usage des zones dans l'admin, bien que fonctionnellement une zone reste une zone.
*   `shipping` : Zones destinées aux transporteurs.
*   `tax` : Zones destinées aux taxes.
*   `all` (par défaut) : Utilisable partout.

### Classe Modèle
Interface : `Sylius\Component\Addressing\Model\ZoneInterface`
Membres : `Sylius\Component\Addressing\Model\ZoneMemberInterface`

```php
interface ZoneInterface extends CodeAwareInterface, TimestampableInterface
{
    public function getType(): ?string; // 'country', 'province', 'zone'
    public function getMembers(): Collection; // Collection de ZoneMember
    public function getScope(): ?string;
}
```

## Configuration

### Via l'interface d'administration
**Configuration > Zones**

1.  **Create** : Choisir le type immédiatement (Country, Province ou Zone).
2.  **Formulaire** :
    *   Code : Identifiant unique (ex: `EU_VAT`).
    *   Name : Nom affiché.
    *   Scope : Tax / Shipping / All.
    *   **Members** : Ajouter les membres (autocomplétion des pays/provinces selon le type choisi).

### Via Fixtures

```yaml
sylius_fixtures:
    suites:
        default:
            fixtures:
                geographical:
                    options:
                        zones:
                            EU: # Code de la zone
                                name: 'European Union'
                                type: country # Obligatoire
                                members: ['FR', 'DE', 'PL', 'ES', ...]
                            
                            US_WEST:
                                name: 'US West Coast'
                                type: province
                                members: ['US-CA', 'US-OR', 'US-WA']
```

## Zone Matcher (Le service clé)

Le `ZoneMatcher` (`sylius.zone_matcher`) est le service qui répond à la question : *"Dans quelle(s) zone(s) se trouve cette adresse ?"*

Il est utilisé massivement par :
*   Le calculateur de taxes.
*   Le résolveur de méthodes de livraison.

Il retourne souvent la zone **la plus spécifique** (celle qui correspond le mieux) ou toutes les zones correspondantes, selon la méthode appelée.

## Points de vigilance
*   **Héritage** : Si une adresse est en "France", elle fait partie de la zone "France" (si elle existe), mais aussi de la zone "Europe" (si France est dans Europe), et de la zone "Monde" (si Europe est dans Monde).
*   **Priorité** : Sylius n'a pas de champ "priorité" explicite sur les zones. La priorité est souvent gérée par les mécanismes qui utilisent les zones (ex: TaxRateResolver cherche la zone la plus précise incluse dans l'adresse).

