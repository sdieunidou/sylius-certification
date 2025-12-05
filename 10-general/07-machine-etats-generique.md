# Utilisation générique de la machine à états

## Objectif
Comprendre que State Machine n'est pas que pour la commande.

## Principe
Tout objet qui a un cycle de vie complexe devrait utiliser une machine à états.

## Exemples dans Sylius
1.  **Order** : `sylius_order` (new -> fulfilled).
2.  **Checkout** : `sylius_order_checkout` (cart -> completed).
3.  **Payment** : `sylius_payment` (new -> processing -> completed/failed).
4.  **Shipment** : `sylius_shipment` (ready -> shipped).
5.  **Product Review** : `sylius_product_review` (new -> accepted/rejected).
6.  **Catalog Promotion** : `sylius_catalog_promotion` (inactive -> processing -> active).

## Configuration
Toujours via `winzou_state_machine.yaml`.

## Utilisation Service
Le service `sylius.resource_controller.state_machine` permet d'appliquer des transitions via l'API ou les contrôleurs de ressource.
Dans le code :
```php
$stateMachine = $factory->get($order, 'sylius_order');
if ($stateMachine->can('cancel')) {
    $stateMachine->apply('cancel');
}
```

