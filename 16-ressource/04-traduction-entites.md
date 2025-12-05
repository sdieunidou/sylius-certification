# Comment fonctionne la traduction des entités ?

## Objectif
Gérer le multilingue (Translatable).

## Pattern
Sylius utilise le pattern standard Doctrine Translatable.

1.  **Entité Principale** (`Product`) implémente `TranslatableInterface`.
    *   Méthode `getTranslations()`.
    *   Trait `TranslatableTrait`.
2.  **Entité Traduction** (`ProductTranslation`) implémente `TranslationInterface`.
    *   Propriété `locale` (code langue).
    *   Propriété `translatable` (lien vers parent).
    *   Trait `TranslationTrait`.

## Fallback
Sylius Resource configure automatiquement le `TranslatableListener`.
Quand vous faites `$product->getName()`, Sylius :
1.  Cherche la traduction dans la locale courante.
2.  Si pas trouvé et fallback activé, cherche dans la locale par défaut.
3.  Retourne la valeur.

## Proxy Methods (PHP 8.2)

Sur l'entité principale, on crée des méthodes magiques ou manuelles :

```php
public function getName(): ?string 
{
    return $this->getTranslation()->getName();
}
```

