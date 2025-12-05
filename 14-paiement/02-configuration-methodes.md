# Configuration des méthodes de paiement

## Objectif
Ajouter un moyen de paiement.

## Entité PaymentMethod
*   `code` : Identifiant.
*   `gatewayConfig` : La configuration technique (API Keys).
*   `channels` : Disponibilité.
*   `instructions` : Texte affiché au client (utile pour virement/chèque).

## Admin
**Configuration > Payment Methods**
1.  Choisir la Gateway Factory (ex: "Offline", "Stripe Checkout", "PayPal Express").
2.  Configurer les clés API.
3.  Activer pour les canaux.

## Gateway Factory
C'est le driver Payum.
Pour ajouter un PSP (Prestataire de Service de Paiement) non supporté :
1.  Installer le bundle Payum correspondant (ou créer une Gateway Factory custom).
2.  Enregistrer la factory dans Sylius.

