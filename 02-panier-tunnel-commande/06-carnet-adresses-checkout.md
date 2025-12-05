# Comportement du carnet d'adresses durant le checkout

## Objectif
Comprendre comment Sylius gère les adresses enregistrées des clients connectés pour accélérer le checkout.

## Le Service AddressBook

Pour les clients connectés (`Customer` avec un `User`), Sylius maintient un carnet d'adresses (`addresses`).

### Fonctionnalités
*   **Adresse par défaut** : Une adresse peut être marquée comme défaut (souvent la dernière utilisée).
*   **Stockage** : Les adresses sont stockées dans la table `sylius_address` et liées au `Customer`.

## Intégration dans le Checkout

Lors de l'étape `Addressing` :

### 1. Affichage
Le formulaire (`CheckoutAddressType`) détecte si l'utilisateur est connecté.
Si oui, il rend une vue partielle qui liste les adresses existantes du client.
L'utilisateur peut :
*   Cliquer sur une adresse existante -> Un script JS remplit automatiquement les champs du formulaire.
*   Ou choisir "Nouvelle adresse" -> Formulaire vide.

### 2. Sauvegarde automatique (Address Provider)
C'est un point subtil de Sylius.
Lorsqu'un client passe une commande avec une **nouvelle** adresse :
*   Cette adresse est associée à la commande (`billingAddress`, `shippingAddress`).
*   Elle est **aussi** ajoutée au carnet d'adresses du client pour un usage futur (sauf si c'est un duplicat exact d'une adresse existante).
*   Cela est géré par le `CustomerOption` ou nativement par le `OrderProcessor` selon la version, assurant que le carnet s'enrichit automatiquement.

## Duplication des Adresses

Sylius suit un pattern de **Duplication (Value Object pattern)** pour les commandes :
*   L'adresse liée à une commande (Order) est une **copie** de l'adresse du carnet ou de la saisie.
*   Si le client modifie son adresse dans son profil "Mon Compte" plus tard, cela **N'AFFECTE PAS** les commandes passées. L'historique reste intègre.

## Points de certification
*   Savoir que l'adresse de la commande est distincte de l'adresse du carnet (ID différents en base).
*   L'auto-remplissage est une fonctionnalité UI/Frontend basée sur les données du Customer injectées dans le template.

