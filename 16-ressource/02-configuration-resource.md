# Configuration de Sylius Resource

## Objectif
Déclarer une nouvelle entité comme Ressource.

## YAML
Fichier `config/packages/sylius_resource.yaml` (ou `app_resource.yaml`).

```yaml
sylius_resource:
    resources:
        app.supplier:
            classes:
                model: App\Entity\Supplier
                # repository: App\Repository\SupplierRepository (Optionnel)
                # form: App\Form\Type\SupplierType (Optionnel)
            translation: # Si traduisible
                classes:
                    model: App\Entity\SupplierTranslation
```

## Ce que ça génère
Dès cette déclaration, vous avez accès à :
*   Service Factory : `app.factory.supplier`.
*   Service Repository : `app.repository.supplier`.
*   Service Manager : `app.manager.supplier`.
*   Service Controller : `app.controller.supplier`.
*   Routes (si configurées dans `routes.yaml`).

