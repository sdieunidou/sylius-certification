# Étendre les formulaires et templates

## Objectif
Modifier l'apparence et les champs de saisie.

## 1. Form Types (Form Extensions)
Vous avez ajouté un champ `nickname` au Customer, il faut l'afficher dans le formulaire d'inscription.

Utilisez le système d'extension de formulaire Symfony.

1.  Créer `App\Form\Extension\CustomerProfileTypeExtension`.
2.  Étendre `AbstractTypeExtension`.
3.  Cibler `Sylius\Bundle\CustomerBundle\Form\Type\CustomerProfileType`.

```php
public function buildForm(FormBuilderInterface $builder, array $options): void
{
    $builder->add('nickname', TextType::class, [
        'label' => 'app.form.customer.nickname',
    ]);
}

public static function getExtendedTypes(): iterable
{
    return [CustomerProfileType::class];
}
```

## 2. Templates (Surcharge Twig)

Sylius utilise un système de thèmes (`SyliusThemeBundle`) mais aussi la surcharge standard Symfony.

### Structure Standard
Les templates originaux sont dans `vendor/sylius/sylius/src/Sylius/Bundle/ShopBundle/Resources/views/`.
Pour surcharger `Product/show.html.twig` :
Copier dans `templates/bundles/SyliusShopBundle/Product/show.html.twig`.

### Événements de Template (Sylius UI Events)
Sylius découpe ses pages en petits blocs injectés via des événements `sylius_ui`.
Au lieu de copier tout le fichier, on peut "hooker" un block.

**Exemple** : Ajouter quelque chose après le bouton "Ajouter au panier".

Dans `config/packages/sylius_ui.yaml` :

```yaml
sylius_ui:
    events:
        sylius.shop.product.show.add_to_cart_form:
            blocks:
                my_custom_message:
                    template: "product/message.html.twig"
                    priority: 5
```
C'est la méthode recommandée pour une meilleure maintenabilité (upgrades plus faciles).

