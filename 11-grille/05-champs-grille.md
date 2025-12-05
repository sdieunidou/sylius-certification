# Champs de grille disponibles et extension

## Objectif
Afficher les données dans les colonnes.

## Champs Natifs
*   `string` : Texte simple (échappé).
*   `datetime` : Date formatée.
*   `twig` : Rendu d'un template Twig (Le plus puissant).
*   `actions` : Affiche les boutons d'action.

## Créer un Champ Personnalisé

Si vous voulez afficher une barre de progression colorée.

1.  **Classe PHP** : `FieldType` implémentant `FieldTypeInterface` (Optionnel si on utilise juste Twig).
2.  **Template Twig** : Le plus simple est souvent d'utiliser le type `twig` directement.

```yaml
fields:
    progress:
        type: twig
        label: Progression
        options:
            template: "@App/Grid/Field/progress.html.twig"
```

Dans le template :
```twig
<div class="progress">
    <div class="bar" style="width: {{ data }}%"></div>
</div>
```
Ici `data` est la valeur du champ (ou l'objet entier si configuré avec `path: .`).

