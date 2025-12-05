# Utilitaires de test dans Sylius

## Objectif
Outils pour faciliter l'écriture de tests.

## Documentation Officielle
*   [Testing Guide](https://docs.sylius.com/en/latest/book/testing/index.html)

## Fixtures (Test Environment)
Les tests Behat chargent des fixtures à la volée pour chaque scénario.

## Page Objects (Pattern)
En Behat, Sylius utilise le pattern Page Object pour découpler le test du HTML.
*   On n'écrit pas "Click on #btn-submit".
*   On écrit `$checkoutPage->placeOrder()`.
*   Si le HTML change, on met à jour seulement la classe `CheckoutPage`.

## ApiTestCase
Classe de base pour tester l'API Platform facilement (client HTTP, assertions JSON).

## Certification
Savoir que Sylius priorise Behat pour la non-régression fonctionnelle.
Savoir lire un scénario Gherkin de base.

