# Détails sur les attributs de produits

## Objectif
Gérer les caractéristiques techniques (Poids, Matière, ISBN).

## EAV (Entity-Attribute-Value)
Sylius utilise un modèle EAV optimisé pour permettre des attributs dynamiques sans changer le schéma de la base.

1.  **Attribute** : La définition (Code: `material`, Type: `text`, Label: `Matière`).
2.  **AttributeValue** : La valeur pour un produit donné (Value: `100% Coton`).
    *   Lié au Produit (Subject).
    *   Lié à l'Attribut.
    *   Contient la valeur (stockée dans `text_value`, `integer_value`, `boolean_value` etc. selon le type).

## Traduction
Les valeurs des attributs de type `text` ou `textarea` peuvent être traduisibles (stockées dans `sylius_product_attribute_value` avec un code `locale`).

## Types d'attributs natifs
*   Text, Textarea
*   Checkbox (Boolean)
*   Integer, Float
*   Date, Datetime
*   Select (Choix prédéfinis)

Note : Les attributs ne créent PAS de variantes. Ce sont des infos.

