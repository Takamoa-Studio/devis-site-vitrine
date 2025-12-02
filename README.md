# Calculateur de coût – Site vitrine

Ce projet est une page HTML autonome (`index.html`) qui calcule en temps réel le coût estimé d'un site vitrine selon plusieurs paramètres (volume de pages, complexité, options, taux horaires, marge, etc.). Le fonctionnement se fait entièrement côté client : aucune dépendance externe ni build n'est nécessaire.

## Comment utiliser la page

1. **Ouvrir l'outil**
   - Ouvre directement `index.html` dans ton navigateur. Tout le code (style et script) est embarqué dans le fichier.

2. **Renseigner les paramètres projet**
   - Choisis le **type de site** (vitrine, vitrine avancée, e-commerce) depuis la liste déroulante ; cela sert surtout à l'intitulé.
   - Sélectionne la **complexité globale** (x1.0, x1.2 ou x1.5) qui multiplie toutes les tâches.
   - Saisis le nombre de **pages d'accueil** (variantes) et de **pages internes** ; ces valeurs pilotent le volume de design et de développement.
   - Indique le nombre de **pages optimisées SEO** à traiter.
   - Active ou non les options : **logo** (`0`/`1`) et **formation** (`0`/`1`).
   - Ajuste les paramètres financiers : **coefficient de marge** (ex. `1.3` pour +30 %), **taux de change** €→MGA, et **buffer imprévus** en %.
   - (Optionnel) Ajoute un **intitulé de projet** pour tes exports ou captures.

3. **Explorer le résumé rapide**
   - La section "Résumé rapide" affiche dynamiquement :
     - le **volume de pages** (home + internes),
     - la **complexité appliquée**,
     - la liste des **options activées** (logo, formation, SEO).

4. **Ajuster les taux horaires par rôle**
   - Dans la table "Taux horaires" tu peux modifier le **taux €/h** de chaque rôle (chef de projet, webdesigner, développeur, graphiste, SEO, QA). Chaque saisie déclenche un recalcul instantané.

5. **Consulter le résumé financier**
   - Le bloc "Résumé financier" affiche automatiquement :
     - le **coût interne estimé** (somme des coûts des tâches + buffer imprévus),
     - le **prix conseillé HT en €** (coût interne x marge),
     - le **prix conseillé HT en MGA** (conversion par le taux de change saisi).

6. **Détails des tâches et calculs**
   - La table "Détail des tâches & temps estimés" est générée depuis la liste `tasks` du script :
     - Chaque ligne indique la **phase**, la **tâche**, le **rôle** associé, les **heures de base**, le **volume** appliqué, les **heures totales** (base × volume × complexité), le **taux horaire** et le **coût calculé**.
     - Le pied de tableau cumule le **total heures** et le **coût total**.

7. **Boucler sur les réglages**
   - Toute modification de paramètre (volume, complexité, options, taux, marge, buffer) déclenche `recalcAll()` : le résumé rapide, les totaux et la table des tâches se mettent à jour en temps réel.

## Structure interne

- **Données** :
  - `roles` contient les rôles avec leurs taux par défaut et une note explicative.
  - `tasks` décrit chaque tâche (phase, rôle, heures de base, clé de volume).
- **Helpers** : `safeNumber`, `fmtEuro`, `fmtMGA`, `fmtHours` gèrent les conversions et formats.
- **Calculs** :
  - `readParams()` lit et sécurise les valeurs des champs.
  - `getTaskVolume()` renvoie le multiplicateur propre à chaque tâche (pages, options, etc.).
  - `recalcAll()` orchestre le calcul des volumes, heures, coûts, buffer, marge et conversions, puis met à jour le DOM.
- **Initialisation** : `initRolesTable()` et `initTasksTable()` génèrent les tableaux dynamiquement, `bindParamEvents()` attache les listeners, et l'événement `DOMContentLoaded` lance l'initialisation + un premier calcul.

## Besoins techniques

- Aucun serveur ni dépendance : un simple navigateur moderne suffit. Le fichier est responsive et fonctionne en local.
