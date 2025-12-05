# Utilisateurs Boutique vs Clients

## Objectif
Distinction clé pour la certification.

## ShopUser (L'Authentification)
*   Étend `User` (Symfony Security).
*   Gère : Email, Password, Rôles (`ROLE_USER`), Salt.
*   Table : `sylius_shop_user`.

## Customer (Le Profil)
*   Gère : Prénom, Nom, Genre, Téléphone, Groupe.
*   Lié aux commandes.
*   Peut exister SANS User (Invité / Guest).
*   Table : `sylius_customer`.

## Relation
Un `ShopUser` a obligatoirement un `Customer` (OneToOne).
Un `Customer` peut avoir un `ShopUser` (s'il a créé un compte) ou NULL (s'il a commandé en invité).

Lorsqu'un invité crée un compte plus tard, Sylius attache son Customer existant (basé sur l'email) au nouveau ShopUser.

