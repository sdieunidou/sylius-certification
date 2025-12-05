# Calculateurs de prix disponibles et extension

## Objectif
Comprendre comment le nouveau prix est calculé mathématiquement.

## Actions Natives

1.  **PercentageDiscountPriceCalculator** (`percentage_discount`)
    *   Formule : `Price = Price * (1 - amount)`
    *   Exemple : 100€ * (1 - 0.20) = 80€.
    
2.  **FixedDiscountPriceCalculator** (`fixed_discount`)
    *   Formule : `Price = Price - amount`
    *   Exemple : 100€ - 10€ = 90€.
    *   Sécurité : Le prix ne peut pas descendre en dessous de 0 (ou 1 centime selon config).

## Étendre les calculateurs

Si vous voulez une logique complexe (ex: "Prix coûtant + 10%").

### 1. Implémenter `ActionCalculatorInterface`

```php
class CostPlusMarginCalculator implements ActionCalculatorInterface
{
    public function calculate(ChannelPricingInterface $channelPricing, array $configuration, array $context): int
    {
        // Logique personnalisée
        // Retourne le nouveau prix (int)
    }
}
```

### 2. Taguer le service
Tag : `sylius.catalog_promotion.action_calculator`.

## Minimum Price
Sylius permet de définir un `minimum_price` sur la variante/channel pricing pour empêcher les promos de vendre à perte. Les calculateurs doivent respecter cette limite.

