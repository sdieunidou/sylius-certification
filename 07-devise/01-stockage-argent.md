# Comment l'argent et les devises sont stockés dans Sylius

## Objectif
Comprendre le modèle de stockage des montants financiers pour éviter les erreurs d'arrondi.

## Entiers (Integers) uniquement

Sylius stocke **TOUS** les montants monétaires en **entiers** (integers), représentant la plus petite unité de la devise.
*   10.00 EUR est stocké comme `1000` (centimes).
*   100 JPY est stocké comme `100` (pas de décimale).
*   0.50 TND est stocké comme `500` (car 1 TND = 1000 millimes).

## Pourquoi ?
Pour éviter les problèmes de précision des nombres flottants (`float`) en informatique (ex: 0.1 + 0.2 != 0.3).

## Le Modèle Currency

L'entité `Currency` (`Sylius\Component\Currency\Model\Currency`) stocke :
*   `code` : Code ISO 4217 (EUR, USD).
*   `name` : Nom affiché (optionnel, souvent géré par Intl).

## Gestion de l'affichage

Pour l'affichage, Sylius utilise le composant `Intl` de Symfony et des Twig Filters.
*   `{{ money.amount|sylius_currency_display(currencyCode) }}`
*   Le filtre divise automatiquement l'entier par 100 (ou 1, ou 1000) selon la configuration de la devise dans les standards internationaux.

## Base de Données
Table `sylius_currency`.
Simple table de référence. Les montants eux-mêmes sont dans `sylius_order`, `sylius_order_item`, etc. sous forme de colonnes `INT`.

