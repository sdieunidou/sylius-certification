# Passerelles de paiement (Payment gateways)

## Objectif
Comprendre l'abstraction Payum.

## Payum dans Sylius
Sylius n'implémente pas directement les appels HTTP vers PayPal ou Stripe. Il délègue cela à la librairie **Payum**.

## Architecture
1.  **Sylius Payment** : Entité business (Montant, Devise, Commande).
2.  **Payum Payment** : Modèle interne Payum (Details JSON).
3.  **Gateway** : L'objet qui exécute les requêtes.
4.  **Action** : Classes unitaires qui font le travail (`CaptureAction`, `AuthorizeAction`, `StatusAction`).

## Créer une intégration personnalisée
1.  Implémenter une `GatewayFactory`.
2.  Implémenter les Actions (`CaptureAction` est la plus importante).
3.  Définir le formulaire de configuration (`GatewayConfigurationType`) pour saisir les clés API dans l'admin Sylius.

## Avenir (Sylius Payments)
Sylius travaille sur une couche d'abstraction plus moderne pour s'éloigner de Payum à terme, mais pour la certification actuelle, Payum est la référence.

