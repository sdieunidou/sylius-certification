# Structure et architecture de haut niveau

## Objectif
Visualiser comment Sylius est organisé.

## Documentation Officielle
*   [Architecture Guide](https://docs.sylius.com/en/latest/book/architecture/index.html)

## Full Stack Framework
Sylius n'est pas juste une lib, c'est une application Symfony complète.

## Architecture en Couches (Layered Architecture)

1.  **Domain (Component)** : Le cœur pur PHP. Entités, Interfaces, Logique métier agnostique. Pas de dépendance à Symfony (théoriquement).
    *   Ex: `Sylius\Component\Order`.
2.  **Infrastructure (Bundle)** : L'intégration avec Symfony et les librairies tierces. Configuration DI, Doctrine mapping, Event Listeners.
    *   Ex: `Sylius\Bundle\OrderBundle`.
3.  **Application (Core)** : La logique spécifique "E-commerce". Lie tous les composants ensemble (Product + Order + User + Taxonomy...).
    *   Ex: `Sylius\Bundle\CoreBundle`.
4.  **Interface (UI/API)** : La couche de présentation.
    *   `SyliusShopBundle` : Frontend Twig.
    *   `SyliusAdminBundle` : Backend Twig.
    *   `SyliusApiBundle` : API Platform (REST/JSON-LD).

## Découplage
On peut utiliser `SyliusOrderBundle` seul dans une application non-Sylius si on veut juste un système de commande, sans le catalogue produit.

