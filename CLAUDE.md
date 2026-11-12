# MyFit — contexte pour Claude

App perso de suivi sport et nutrition. Interface 100 % en français.
En ligne : https://onihxh.github.io/myfit/ · Dépôt : https://github.com/OniHxh/myfit (public, branche `main`, GitHub Pages à la racine).

## Règles de travail (à respecter à chaque session)

- **Ne jamais effacer les données de l'utilisateur.** Elles vivent dans le `localStorage` du téléphone (clé `myfit.v1`), pas dans le dépôt. Toute évolution du format doit rester compatible avec les données existantes (fusion avec `blank()` au chargement).
- **Avant chaque publication (`git push`)** : prévenir l'utilisateur pour qu'il exporte ses données depuis l'app, attendre son feu vert, puis pousser.
- Après le push : attendre ~50 s, vérifier le site en ligne avec `curl`.
- À chaque mise à jour publiée, incrémenter `CACHE='myfit-vN'` dans `sw.js`.
- Tester dans le navigateur intégré (format téléphone 375×812) avec des données factices, console sans erreur, avant de publier.
- Le dépôt est **public** : ne jamais y mettre de données perso (poids, photos, mensurations, e-mail…).
- L'utilisateur n'est pas développeur : expliquer simplement, en étapes courtes. Il aime les graphiques, la 3D, les animations et une expérience soignée, style sombre premium.

## Architecture

- Une seule page : `index.html` (HTML + CSS + JS vanilla, aucune dépendance). Plus `manifest.webmanifest` (« MyFit – Sport & Nutrition », thème `#07080c`), `sw.js` network-first, et les icônes `icon-192.png`, `icon-512.png`, `apple-touch-icon.png`.
- Données : `localStorage['myfit.v1']`, avec export / import JSON (`exportData`, `importData`, partage via `navigator.share`).
- Vues :
  - `vOnboarding` : profil de départ.
  - `vHome` : accueil.
  - `vMeals` : repas (petit-déjeuner, déjeuner, dîner, collations).
  - `vSport` et `vSession` : séances.
  - `vProg` : progrès (poids, mensurations taille / hanches / bras / cuisse, photos).
  - `vMe` : profil et réglages.
- Pas de synchronisation entre appareils pour l'instant. Si on en ajoute une, reprendre le modèle de Plan : Gist privé chiffré AES-GCM, clé GitHub limitée à `gist` et créée par l'utilisateur lui-même.

## Historique

1. Création : app de suivi sport et nutrition.
2. Pesée imposée, bilan des pesées, comparaison photo avant/après.
3. Ajustement auto des calories, mensurations, bilan hebdo, copie de repas, repas plaisir, records, minuteur boxe, calories brûlées, rappel de sauvegarde, badges.
4. Thème sport premium sombre, graphiques calories + sport, calendrier des séances.
