# Comportement des provinces par rapport aux pays

## Objectif
Comprendre l'interaction dynamique entre Pays et Provinces, notamment dans les formulaires d'adresse (Checkout, Carnet d'adresses).

## Relation Parent-Enfant

La relation est de type **One-to-Many** :
*   Un Pays a plusieurs Provinces (`Collection<ProvinceInterface>`).
*   Une Province appartient à un seul Pays.
*   **Cascade** : La suppression d'un Pays entraîne généralement la suppression de ses Provinces (cascade remove), bien que dans un e-commerce, on supprime rarement des pays; on les désactive.

## Comportement dans les Formulaires (Frontend)

C'est un point crucial pour l'expérience utilisateur (UX) et la certification.

### Le champ `provinceCode` vs `provinceName`

L'entité `Address` possède deux champs liés :
1.  `provinceCode` (stocke le code si une province est sélectionnée depuis la liste).
2.  `provinceName` (stocke le nom si l'utilisateur l'a tapé manuellement).

### Logique d'affichage (Form Listener)

Sylius utilise un écouteur d'événements JavaScript (dans le thème Shop) et des `FormEvents` côté Symfony pour adapter le formulaire :

1.  **Si le Pays sélectionné a des provinces configurées en BDD :**
    *   Le champ Province devient un **Menu Déroulant** (`ChoiceType`).
    *   L'utilisateur *doit* choisir une province de la liste.
    *   La valeur est stockée dans `provinceCode`.
    
2.  **Si le Pays sélectionné N'A PAS de provinces configurées :**
    *   Le champ Province devient un **Champ Texte** (`TextType`) ou peut être masqué.
    *   L'utilisateur tape le nom de sa région/état.
    *   La valeur est stockée dans `provinceName`.

### Validation

La validation de l'adresse (`Sylius\Component\Addressing\Model\Address`) dépend de cette logique :
*   Si le pays a des provinces, la contrainte vérifie que `provinceCode` est valide et appartient au pays.
*   L'intégrité des données est assurée par le `ProvinceCodeValidator`.

## Impact sur les Zones

Lorsqu'on définit une **Zone** basée sur les provinces :
*   On ne peut ajouter que des provinces qui existent réellement en base de données.
*   Si un client tape "California" manuellement (champ texte) parce que les provinces US ne sont pas configurées, le système de Zone ne pourra pas faire la correspondance automatique avec une zone "West Coast" définie par des codes provinces.

> **Best Practice** : Toujours configurer les provinces pour les pays où la fiscalité ou les frais de port varient selon la région (ex: USA, Canada).

## Manipulation Programmatique

```php
$country = $address->getCountryCode(); // 'US'
$provinces = $countryRepository->findOneBy(['code' => $country])->getProvinces();

if (!$provinces->isEmpty()) {
    // Logique pour forcer la sélection d'une province
}
```

