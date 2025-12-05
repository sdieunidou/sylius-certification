# Étendre les modèles, repositories et factories

## Objectif
Personnaliser la logique métier fondamentale de Sylius.

## 1. Étendre une Entité (Model)
Vous voulez ajouter un champ `nickname` au `Customer`.

1.  **Classe PHP** : Créer `App\Entity\Customer` qui étend `Sylius\Component\Core\Model\Customer`.
    *   Ajouter la propriété et les getters/setters.
2.  **Mapping Doctrine** : Créer le fichier de mapping (XML/YAML/Attribute) pour ce champ.
    *   Si XML (recommandé dans Sylius) : `config/doctrine/Customer.orm.xml` en mappant la table `sylius_customer`.
3.  **Configuration** : Dire à Sylius d'utiliser VOTRE classe.
    ```yaml
    # config/packages/sylius_customer.yaml
    sylius_customer:
        resources:
            customer:
                classes:
                    model: App\Entity\Customer
    ```
    *   Sylius résoudra désormais l'interface `CustomerInterface` vers votre classe.

## 2. Étendre un Repository
Vous voulez une méthode `findVipCustomers()`.

1.  **Classe PHP** : Créer `App\Repository\CustomerRepository` qui étend `Sylius\Bundle\CoreBundle\Doctrine\ORM\CustomerRepository`.
2.  **Configuration** :
    ```yaml
    sylius_customer:
        resources:
            customer:
                classes:
                    repository: App\Repository\CustomerRepository
    ```

## 3. Étendre une Factory
Vous voulez initialiser le `nickname` par défaut.

1.  **Classe PHP** : Créer `App\Factory\CustomerFactory` qui implémente `CustomerFactoryInterface` (ou décore l'existante).
    *   *Best Practice* : Utiliser la décoration de service Symfony.
2.  **Décoration** :
    ```yaml
    App\Factory\CustomerFactory:
        decorates: sylius.factory.customer
        arguments: ['@.inner']
    ```

```php
public function createNew(): CustomerInterface {
    $customer = $this->decorated->createNew();
    $customer->setNickname('Newbie');
    return $customer;
}
```

