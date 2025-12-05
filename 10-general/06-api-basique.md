# Questions basiques sur l'API Sylius

## Objectif
Comprendre la nouvelle API unifiée (API Platform).

## REST & JSON-LD
L'API suit les standards REST et utilise le format JSON-LD (Linked Data) / Hydra pour l'hypermédia.
*   `@context`, `@id`, `@type`.

## Authentification
*   **Admin** : JWT (JSON Web Token).
*   **Shop** : JWT.

## Endpoints
Tout est ressource.
*   `GET /api/v2/shop/products`
*   `POST /api/v2/shop/orders` (Cart)
*   `PATCH /api/v2/shop/orders/{tokenValue}` (Update Cart)

## Commandes (CQRS)
Certaines opérations complexes ne sont pas de simples CRUD (ex: valider le checkout). Elles passent par des endpoints "Command" ou des opérations `custom` dans API Platform.
*   Ex: `/api/v2/shop/orders/{tokenValue}/complete`

## Extension
Pour ajouter un champ à l'API :
1.  Étendre la ressource API Platform (XML/Attribute).
2.  Utiliser des `Serialization Groups` (`shop:product:read`, `admin:product:write`) pour contrôler l'exposition.

