# Types de tests dans Sylius

## Objectif
Sylius est célèbre pour sa culture du test (TDD/BDD).

## 1. Behat (Acceptance / E2E)
Le plus important. Teste le comportement métier en langage naturel (Gherkin).
*   Scenario: "En tant que client, je peux ajouter un t-shirt au panier".
*   Couvre : UI (via Selenium/Chrome) et API (via requêtes HTTP).
*   Localisation : `features/`.

## 2. PHPSpec (Unit)
Teste le comportement des classes (SpecBDD).
*   "Describe generic shipping calculator".
*   Force à écrire des petites classes découplées.
*   Localisation : `spec/`.

## 3. PHPUnit (Functional / Integration)
Utilisé pour tester les Repositories, les configurations de services, et les contrôleurs (si pas couverts par Behat).
*   Localisation : `tests/`.

