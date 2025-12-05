# Actions de promotion disponibles et extension

## Objectif
Connaître les effets possibles d'une promotion et savoir en ajouter.

## Actions Natives (Built-in Actions)

Actions définies dans `Sylius\Component\Core\Promotion\Action`.

1.  **Order Fixed Discount** (`order_fixed_discount`) : Réduction fixe sur le total du panier (ex: -10€).
    *   Répartie proportionnellement sur chaque ligne (Distributed).
2.  **Order Percentage Discount** (`order_percentage_discount`) : Réduction en pourcentage sur le total (ex: -10%).
3.  **Item Fixed Discount** (`item_fixed_discount`) : Réduction fixe *par article* éligible (ex: -1€ sur chaque tasse).
    *   Nécessite souvent un filtre (ex: s'applique seulement aux tasses).
4.  **Item Percentage Discount** (`item_percentage_discount`) : Réduction % par article (ex: -50% sur le 2ème).
5.  **Shipping Percentage Discount** (`shipping_percentage_discount`) : Réduction sur les frais de port (ex: -100% = Livraison Gratuite).

## Créer une Action Personnalisée

Exemple : "Ajouter un produit cadeau gratuit au panier".

### 1. Créer l'Executor
Implémenter `ActionExecutorInterface`.

```php
class AddFreeProductActionExecutor implements ActionExecutorInterface
{
    public function execute(SubjectInterface $subject, array $configuration, PromotionInterface $promotion): void
    {
        /** @var OrderInterface $order */
        $order = $subject;
        
        $variantCode = $configuration['variant_code'];
        // Logique pour ajouter l'OrderItem à $order avec prix 0
        // Attention à gérer le cas où il est déjà là pour ne pas l'ajouter 2 fois
    }
}
```

### 2. Enregistrer le Service

```yaml
services:
    app.promotion_action.add_free_product:
        class: App\Action\AddFreeProductActionExecutor
        tags:
            - { name: sylius.promotion_action, type: add_free_product, label: "Add Free Product" }
```

### 3. FormType
Créer le formulaire pour choisir quel produit offrir dans l'admin.

## Distinction importante : Répartition (Distribution)
Les remises fixes sur la commande (`order_fixed_discount`) sont techniquement réparties sur les items dans Sylius.
Si j'ai 2 items à 50€ et une remise de 10€ :
*   Item 1 aura un ajustement de -5€.
*   Item 2 aura un ajustement de -5€.
Cela est crucial pour les retours partiels (refunds) : si je rends l'Item 1, je rembourse 45€, pas 50€.

