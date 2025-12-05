# Calculateurs de frais de port

## Objectif
Calculer le coût.

## Calculateurs Natifs
1.  **Flat Rate** : Prix fixe par commande (ex: 5€).
2.  **Per Unit Rate** : Prix par article (ex: 1€ par item).
3.  **Flexible Rate** : ex: 10€ pour le 1er item, 2€ pour les suivants.
4.  **Weight based (Table Rate)** : Grille selon le poids total.
    *   0-1kg : 5€
    *   1-5kg : 8€

## Créer un Calculateur Custom
Interface : `CalculatorInterface`.
Méthode : `calculate(SubjectInterface $subject, array $configuration): int`.

Exemple : Calculateur API (interroge UPS en temps réel).
Attention : `calculate` est appelé souvent, mettre du cache si API externe.

