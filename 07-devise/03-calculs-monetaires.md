# Calculs monétaires et présentations

## Objectif
Manipuler les montants dans le code.

## CurrencyConverter

Service : `Sylius\Component\Currency\Converter\CurrencyConverterInterface`.

```php
public function convert(int $amount, string $sourceCurrencyCode, string $targetCurrencyCode): int;
```

Ce service cherche le `ExchangeRate` applicable et fait la mathématique.

## Précision et Arrondi

Comme on manipule des entiers, la conversion 1000 (10.00 EUR) * 1.2345 = 1234.5 doit être arrondie.
Sylius arrondit généralement au "plus proche" (round half up) pour retourner un entier `1235`.

## Affichage Frontend

Dans Twig :
`{{ price|sylius_price(currencyCode, localeCode) }}`

Ce helper :
1.  Formate le symbole ($, €, £).
2.  Place le symbole au bon endroit (avant ou après selon la locale).
3.  Gère les décimales.

## Point important : Prix Psychologique
La conversion automatique donne souvent des prix "moches" (ex: 19.99€ devient 23.41$).
Sylius ne gère pas nativement les "prix par zone" fixes (sauf en utilisant des canaux différents). La conversion est purement mathématique.

