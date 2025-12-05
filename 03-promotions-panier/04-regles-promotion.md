# Règles de promotion disponibles et extension

## Objectif
Connaître les conditions natives et savoir en créer de nouvelles.

## Règles Natives (Built-in Rules)

Sylius fournit un jeu de règles standard (`Sylius\Component\Promotion\Checker\Rule`).

1.  **Cart Quantity** (`cart_quantity`) : Nombre total d'articles dans le panier.
    *   Config: `count` (ex: > 3 articles).
2.  **Item Total** (`item_total`) : Montant total des articles.
    *   Config: `amount` par channel.
3.  **Customer Group** (`customer_group`) : Le client appartient à un groupe (ex: VIP, Wholesale).
4.  **Shipping Country** (`shipping_country`) : Le pays de livraison est X.
5.  **Has Taxonomy** (`has_taxon`) : Le panier contient au moins un produit de la catégorie X.
6.  **Nth Order** (`nth_order`) : C'est la N-ième commande du client (ex: offre de bienvenue pour la 1ère).
7.  **Contains Product** (`contains_product`) : Le panier contient le produit spécifique Y.

## Créer une Règle Personnalisée (Custom Rule)

Exemple : "Le panier pèse plus de 10kg".

### 1. Créer le Checker
Implémenter `RuleCheckerInterface`.

```php
class TotalWeightRuleChecker implements RuleCheckerInterface
{
    public function isEligible(SubjectInterface $subject, array $configuration): bool
    {
        // $subject est la Commande (Order)
        $totalWeight = 0;
        foreach ($subject->getItems() as $item) {
            $totalWeight += $item->getVariant()->getWeight() * $item->getQuantity();
        }

        return $totalWeight >= $configuration['weight'];
    }
    
    public function getConfigurationFormType(): ?string 
    {
        return TotalWeightRuleConfigurationType::class; // Formulaire pour l'admin
    }
}
```

### 2. Enregistrer le Service
Taguer avec `sylius.promotion_rule_checker`.

```yaml
services:
    app.promotion_rule_checker.total_weight:
        class: App\Checker\TotalWeightRuleChecker
        tags:
            - { name: sylius.promotion_rule_checker, type: total_weight, label: "Total Weight" }
```

### 3. Créer le FormType
Pour que l'admin puisse saisir le poids cible (ex: 10000g).

La règle apparaîtra désormais dans le menu déroulant de l'admin.

