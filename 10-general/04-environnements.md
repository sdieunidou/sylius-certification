# Ce qui est préconfiguré selon les environnements

## Objectif
Différences entre `dev`, `prod`, `test`.

## Environnement de Développement (`dev`)
*   **Debug** : Activé (Barre d'outils Symfony, Profiler).
*   **Cache** : Désactivé ou rafraîchi agressivement.
*   **Assets** : Souvent servis directement sans minification.
*   **Erreurs** : Affichage complet des Stack Traces.
*   **Email** : Interceptés par le Profiler ou Mailhog (pas d'envoi réel).

## Environnement de Production (`prod`)
*   **Debug** : Désactivé.
*   **Cache** : Doctrine Metadata, Query, Result caches activés. Conteneur compilé.
*   **Assets** : Minifiés et versionnés.
*   **Erreurs** : Pages d'erreur génériques ("Oops, something went wrong").
*   **Performance** : Optimisé pour la vitesse.

## Environnement de Test (`test`)
*   **Base de données** : Séparée (souvent `_test`).
*   **Services** : Certains services peuvent être "mockés" ou configurés différemment (ex: `filesystem` pour ne pas écrire de vrais fichiers).
*   **Fixtures** : Chargées à la volée.

