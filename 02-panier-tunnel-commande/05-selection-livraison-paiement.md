# Sélection des méthodes de livraison et de paiement

## Objectif
Détail technique de la résolution et de la sélection des méthodes logistiques et financières.

## Documentation Officielle
*   [Shipments Guide](https://docs.sylius.com/en/latest/book/orders/shipments.html)
*   [Payments Guide](https://docs.sylius.com/en/latest/book/orders/payments.html)

## Sélection de la Livraison (Shipping)

### Modèle de données
*   **Shipment** : Une commande a une ou plusieurs expéditions (`Shipment`).
*   **ShippingMethod** : L'entité de configuration (ex: FedEx, Pickup).

### Résolution des méthodes disponibles
Service : `ShippingMethodResolver`
Critères de filtrage par défaut :
1.  **Zone** : L'adresse de livraison doit matcher la zone de la méthode.
2.  **Category** : Si les produits nécessitent une catégorie spécifique (ex: "Produits Dangereux"), seules les méthodes compatibles sont montrées.
3.  **Rules** : Règles personnalisées (ex: Poids total < 20kg, Total commande > 50€).
4.  **Channel** : La méthode doit être activée pour le canal courant.

### Calcul des frais
Une fois sélectionnée, le coût est calculé par un `Calculator` (FlatRate, PerUnit, TableRate...).

## Sélection du Paiement (Payment)

### Modèle de données
*   **Payment** : Une commande a un ou plusieurs paiements.
*   **PaymentMethod** : Configuration (ex: Stripe, Virement).

### Résolution des méthodes disponibles
Service : `PaymentMethodResolver`
Critères de filtrage :
1.  **Channel** : Activé pour le canal.
2.  **Gateway Config** : La passerelle doit être valide.
3.  **Rules** : Règles personnalisées (rarement utilisé par défaut mais possible).
4.  **État** : Active.

> **Note Importante** : Par défaut, les méthodes de paiement ne sont **pas** liées aux zones géographiques dans Sylius Core (contrairement à la livraison). Si vous devez restreindre un moyen de paiement à un pays, il faut ajouter un résolveur personnalisé ou utiliser un plugin.

## Interaction Shipping <-> Payment

Dans certaines boutiques, le choix de la livraison impacte le paiement (ex: Contre-remboursement disponible uniquement si livraison propre).
Sylius ne gère pas cette dépendance nativement dans le formulaire, mais elle peut être implémentée via les événements de formulaire ou un `PaymentMethodResolver` personnalisé qui regarde la méthode de livraison sélectionnée (`$order->getShipments()->first()->getMethod()`).

