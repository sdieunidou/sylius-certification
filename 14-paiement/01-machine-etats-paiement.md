# Machine à états des paiements

## Objectif
Suivre l'argent.

## Documentation Officielle
*   [Payment State Machine](https://docs.sylius.com/en/latest/book/orders/payments.html#state-machine)

## États (`sylius_payment`)

1.  `new` : Créé, montant défini, mais pas encore communiqué à la banque.
2.  `processing` : L'utilisateur est sur la page de la banque ou la requête API est partie.
3.  `completed` : L'argent est capturé (ou autorisé selon config). Succès.
4.  `failed` : Refus bancaire, erreur technique.
5.  `cancelled` : Annulé par l'utilisateur ou l'admin.
6.  `refunded` : Remboursé.
7.  `authorized` : (Optionnel) L'empreinte bancaire est prise, mais pas débitée.

## Transitions Automatiques
Les webhooks (IPN) des passerelles de paiement déclenchent ces transitions via Payum.
Exemple : Stripe envoie `payment_intent.succeeded` -> Payum notifie Sylius -> Transition vers `completed`.

