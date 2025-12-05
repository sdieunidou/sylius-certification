# Configuration des coupons

## Objectif
Gérer les codes promotionnels (Coupons) liés aux promotions de panier.

## Documentation Officielle
*   [Coupons Guide](https://docs.sylius.com/en/latest/book/orders/promotions.html#coupons)

## Relation Promotion-Coupon

Une **Promotion** peut être :
1.  **Automatique** : S'applique dès que les règles sont remplies (pas de coupon).
2.  **Basée sur coupon (`couponBased: true`)** : Ne s'applique QUE si un coupon valide lié à cette promotion est saisi dans le panier.

## Le Modèle Coupon

Entité : `Sylius\Component\Promotion\Model\Coupon`

Attributs :
*   `code` : La chaîne que l'utilisateur tape (ex: `SUMMER2025`).
*   `usageLimit` : Nombre total de fois que ce code peut être utilisé (ex: 100 premiers clients).
*   `perCustomerUsageLimit` : Nombre de fois qu'un *même* client peut l'utiliser.
*   `expiresAt` : Date d'expiration du code (peut être plus restrictive que la promotion elle-même).
*   `promotion` : La promotion parente.

## Génération de Coupons

Sylius offre un outil pour générer des coupons en masse.
1.  Dans la page d'édition de la promotion.
2.  Bouton "Generate coupons".
3.  Options :
    *   Quantité (ex: 1000).
    *   Longueur du code (ex: 8 caractères).
    *   Préfixe / Suffixe.

Cela est utile pour des campagnes d'emailing uniques.

## Saisie Frontend

Le formulaire de panier (`CartType`) inclut un champ `promotionCoupon`.
Lors de la soumission :
1.  Sylius cherche le coupon par code.
2.  Vérifie sa validité (dates, limites d'usage).
3.  Vérifie si la promotion parente est éligible (règles).
4.  Si tout est OK, le coupon est attaché à la commande.

## Astuce Certification
Une promotion peut avoir *plusieurs* coupons différents (ex: `VIP_ALICE`, `VIP_BOB`) qui déclenchent tous la *même* promotion (-10%). Cela permet de tracker qui a utilisé le code tout en centralisant la règle métier.

