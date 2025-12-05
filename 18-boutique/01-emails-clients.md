# Envoi d'emails aux clients

## Objectif
Gestion des notifications transactionnelles.

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

## Envoi
Service : `SenderInterface`.
```php
$sender->send('order_confirmation', ['user@test.com'], ['order' => $order]);
```
Le 2ème argument (destinataire) est un tableau.
Le 3ème argument (data) est injecté dans le template Twig.

