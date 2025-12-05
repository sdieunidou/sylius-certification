# Comment les canaux sont résolus (resolved)

## Objectif
Savoir comment Sylius devine sur quel canal se trouve l'utilisateur.

## Le ChannelContext

Le service clé est `Sylius\Component\Channel\Context\ChannelContextInterface`.
Méthode : `getChannel()`.

## Les Providers (Stratégie de résolution)

Sylius utilise une chaîne de responsabilité (`CompositeChannelContext`). Il essaie plusieurs méthodes dans l'ordre jusqu'à en trouver une qui marche.

Par défaut (dans `sylius_channel.yaml`) :

1.  **Request Host (HostnameBasedRequestResolver)** :
    *   Regarde le domaine de l'URL (`$_SERVER['HTTP_HOST']`).
    *   Si `maboutique.fr` correspond au `hostname` configuré pour le canal "France", alors c'est le canal France.
    *   C'est la méthode la plus courante.

2.  **Code (Get parameter)** (Souvent désactivé en prod) :
    *   `?_channel_code=US_WEB`. Utile pour le débogage.

3.  **Single Channel** :
    *   S'il n'y a qu'un seul canal actif dans la base de données, c'est forcément lui.

## Cas d'erreur (`ChannelNotFoundException`)
Si aucun resolver ne trouve de canal (ex: on accède via une IP inconnue ou un domaine non configuré), Sylius lance une exception qui affiche généralement une page d'erreur ou 404.

## En CLI / Commandes
Lorsqu'on lance une commande console qui a besoin du contexte (ex: envoi d'emails différés), il faut souvent passer le code du canal en argument ou le définir manuellement car il n'y a pas de requête HTTP.

```php
$channelContext->setChannel($myChannel); // Si le contexte est mutable
// Ou passer le canal directement aux services qui en ont besoin.
```

