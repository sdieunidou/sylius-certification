# Résolution de la locale

## Objectif
Savoir comment Sylius décide en quelle langue afficher le site.

## LocaleContext

Le `LocaleContextInterface` retourne la locale courante.

## Stratégie de Résolution (LocaleProvider)

1.  **URL** : Si l'URL contient le code locale (ex: `/fr_FR/products`), c'est prioritaire.
2.  **User** : Si l'utilisateur est connecté, sa préférence linguistique (si stockée).
3.  **Session** : La locale stockée en session `_locale` (si l'utilisateur a changé via le sélecteur de langue).
4.  **Channel** : La `defaultLocale` du Canal courant.

## URL Strategy
Sylius permet de configurer si le code locale doit apparaître dans l'URL.
*   Par défaut : Oui (SEO friendly).
*   Configurable dans `config/packages/sylius_shop.yaml` (`locale_switcher`).

## Point Certification
Le **Fallback** : Si une traduction n'existe pas dans la locale courante (ex: es_ES), Sylius peut être configuré pour afficher la locale par défaut (en_US) au lieu de vide, via le `TranslatableListener` config (`fallback_locale`).

