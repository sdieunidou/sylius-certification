# Envoi d'emails aux clients

## Objectif
Gestion des notifications transactionnelles.

## Documentation Officielle
*   [Mailer Guide](https://docs.sylius.com/en/latest/book/support/mailer.html)

## SyliusMailerBundle
Abstraction au-dessus de Symfony Mailer.

## Sender
L'expéditeur est configuré par **Canal**.

## Configuration Email
Fichier : `sylius_mailer.yaml`.
On définit des "codes" d'email (ex: `order_confirmation`).

```yaml
sylius_mailer:
    emails:
        order_confirmation:
            subject: "Votre commande {{ order.number }}"
            template: "@SyliusShop/Email/orderConfirmation.html.twig"
            enabled: true
```

## Envoi (PHP 8.2)

Service : `Sylius\Component\Mailer\Sender\SenderInterface`.

```php
use Sylius\Component\Mailer\Sender\SenderInterface;

public function sendConfirmation(SenderInterface $sender, OrderInterface $order): void
{
    $email = $order->getCustomer()?->getEmail();
    
    if ($email) {
        $sender->send('order_confirmation', [$email], ['order' => $order]);
    }
}
```

