# Machine à états de la livraison

## Objectif
Suivre le colis.

## États (`sylius_shipment`)

1.  `cart` : En cours de construction.
2.  `ready` : Commande validée/payée, prêt à expédier.
3.  `shipped` : Colis remis au transporteur.
4.  `cancelled` : Annulé.

Note : Pas d'état "Livré" (`delivered`) natif dans le core standard v1/v2 (souvent ajouté par plugin ou custom), car Sylius s'arrête souvent à l'expédition. Mais facile à ajouter.

## Transition 'ship'
C'est cette transition qui décrémente le stock physique (`onHand`).
On peut y attacher un listener pour envoyer l'email "Votre colis est parti" avec le tracking number.

