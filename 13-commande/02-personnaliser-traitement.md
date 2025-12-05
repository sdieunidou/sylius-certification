# Comment personnaliser le traitement d'une commande

## Objectif
Insérer une logique métier spécifique (ex: envoyer une notif SMS, exporter vers ERP).

## State Machine Callbacks (La méthode royale)
Utiliser les événements de la machine à états `sylius_order`.

Exemple : Exporter vers l'ERP quand la commande est confirmée.

```yaml
winzou_state_machine:
    sylius_order:
        callbacks:
            after:
                export_to_erp:
                    on: ["create"]
                    do: ["@app.erp_exporter", "export"]
                    args: ["object"]
```

## Events Symfony
Sylius lance aussi des événements Symfony classiques via `Sylius\Bundle\ResourceBundle\Event\ResourceControllerEvent`.
*   `sylius.order.post_create`
*   `sylius.order.post_update`
*   `sylius.order.pre_complete` (via le contrôleur de checkout).

Préférez la State Machine pour la logique métier critique, et les Events Resource pour la logique UI/HTTP (flash messages, redirection).

