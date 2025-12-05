# Actions de grille disponibles et extension

## Objectif
Ajouter des boutons dans la grille.

## Types d'actions

1.  **Main** : Actions globales (en haut à droite). Ex: "Créer".
2.  **Item** : Actions par ligne. Ex: "Editer", "Supprimer".
3.  **Bulk** : Actions de masse (checkboxes). Ex: "Supprimer la sélection".

## Actions Natives
*   `create` : Lien vers la route de création.
*   `update` : Lien vers la route d'édition.
*   `delete` : Formulaire de suppression (avec token CSRF).
*   `show` : Lien simple.

## Créer une Action Personnalisée

Si vous voulez un bouton "Envoyer Email" sur chaque ligne.

1.  Déclarer l'action dans la grille :
    ```yaml
    actions:
        item:
            send_email:
                type: send_email # Votre type personnalisé OU 'link' générique
                label: Envoyer Email
                options:
                    link:
                        route: app_admin_supplier_send_email
                        parameters:
                            id: resource.id
    ```

2.  Si besoin d'une logique complexe (template spécifique), créer un `ActionRenderer` ou simplement configurer le template de l'action de type `link`.

## Action Type 'link' (Le couteau suisse)
Le type `link` est le plus utilisé pour les boutons custom.
```yaml
type: link
options:
    route: my_route
    icon: envelope
    class: primary
```

