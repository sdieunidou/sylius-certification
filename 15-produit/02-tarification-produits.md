# Détails sur la tarification des produits

## Objectif
Comment les prix sont stockés.

## ChannelPricing
Le prix n'est PAS sur la Variante directement (car il dépend du canal).
Il est dans `Sylius\Component\Core\Model\ChannelPricing` (Table `sylius_channel_pricing`).

*   Lien : `ProductVariant` -> OneToMany -> `ChannelPricing`.
*   Clé : `channelCode`.
*   Champs :
    *   `price` : Prix de vente actuel (INT).
    *   `originalPrice` : Prix barré (INT, optionnel).
    *   `minimumPrice` : Plancher pour les promotions (INT).

## Récupération du prix
```php
$variant->getChannelPricingForChannel($channel)->getPrice();
```

## Devises
Le `ChannelPricing` est exprimé dans la `baseCurrency` du canal.
Si le canal est en EUR, le prix est en centimes d'EUR.
L'affichage en USD se fait par conversion dynamique, pas par stockage.

