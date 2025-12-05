# Les taux de change et leur comportement

## Objectif
Gérer la conversion entre la devise de base du canal et les autres devises supportées.

## Documentation Officielle
*   [Exchange Rates](https://docs.sylius.com/en/latest/book/configuration/currencies.html#exchange-rates)

## Exchange Rate (Taux de Change)

L'entité `ExchangeRate` lie deux devises :
*   `sourceCurrency` : Devise de départ (souvent la base currency du canal).
*   `targetCurrency` : Devise cible.
*   `ratio` : Le taux (Float). Ex: 1.20 pour EUR -> USD.

## Sens de la conversion

Sylius utilise une logique unidirectionnelle par paire explicite pour éviter les inversions mathématiques imprécises.
Si vous gérez EUR et USD, vous devez définir le taux EUR->USD.

## Mises à jour

Sylius ne met pas à jour les taux automatiquement par défaut (pas de connexion native à la Banque Centrale Européenne en core).
Il faut soit :
1.  Les mettre à jour manuellement dans l'admin.
2.  Utiliser une commande personnalisée ou un plugin pour fetcher les taux via API externe.

## Utilisation dans le calcul
Lorsqu'un client navigue en USD sur un canal dont la base est EUR :
1.  Sylius prend le prix en EUR (ChannelPricing).
2.  Applique le `ratio` (Prix * Ratio).
3.  Arrondit le résultat selon la devise cible.

