# Calculateur de devis – site vitrine

Cette page HTML autonome (`index.html`) calcule en temps réel le coût d'un site vitrine en combinant volumes, options, taux horaires, marge et conversion monétaire. Aucune dépendance externe n'est requise : il suffit d'ouvrir le fichier dans un navigateur moderne.

## Utiliser le calculateur

1. **Ouvrir et choisir un preset**
   - Ouvre `index.html` dans le navigateur puis sélectionne un **type de site** (landing, vitrine, vitrine avancée). Chaque preset injecte une série de valeurs par défaut pour les champs du formulaire. 【F:index.html†L1875-L1990】
   - Le bouton **Reset** réapplique les valeurs du preset actuellement sélectionné. 【F:index.html†L2530-L2545】

2. **Renseigner les paramètres de production**
   - Saisis les volumes de pages (home, internes, légales) et la **complexité globale** qui servira de multiplicateur. 【F:index.html†L2075-L2104】【F:index.html†L2465-L2469】
   - Active les options de **services**, **réalisations**, **blog**, **logo/charte** et **formation** selon le périmètre voulu ; les champs associés sont neutralisés si l'option est désactivée (ex. blog absent ⇒ import et articles à 0). 【F:index.html†L2105-L2138】【F:index.html†L2147-L2168】
   - Ajuste les paramètres financiers : **buffer imprévus** (en %), **marge de vente**, **taux de change €→MGA**. 【F:index.html†L2169-L2180】【F:index.html†L2498-L2509】

3. **Importer/exporter une configuration**
   - Clique sur **Exporter les paramètres** pour télécharger un JSON contenant toutes les entrées et les taux horaires courants ; le nom de fichier est horodaté et dérivé de l'intitulé du projet. 【F:index.html†L2554-L2562】【F:index.html†L2623-L2645】
   - Utilise **Importer un fichier** pour charger un JSON précédemment exporté : les champs sont renseignés, les taux horaires mis à jour puis un recalcul global est déclenché. 【F:index.html†L2626-L2641】

4. **Explorer les résultats**
   - Le bloc **Résumé rapide** liste le volume de pages, la complexité appliquée, les pages légales et les options actives (services, réalisations, SEO, blog/import). 【F:index.html†L2398-L2450】
   - Le bloc **Résumé financier** affiche le coût total freelance, le coût interne avec buffer, puis le prix conseillé HT en euros et en MGA. 【F:index.html†L2498-L2509】
   - La table **Taux horaires** permet de modifier le tarif de chaque rôle ; chaque saisie relance le calcul. 【F:index.html†L1498-L1551】【F:index.html†L2223-L2235】
   - Le tableau **Détail des tâches & temps estimés** se filtre par rôle, peut masquer les tâches à 0 €, et propose un export CSV des lignes visibles. 【F:index.html†L2230-L2330】【F:index.html†L2452-L2492】【F:index.html†L2573-L2580】

## Comment sont faits les calculs

- **Lecture des paramètres** : `readParams()` sécurise les entrées (bornes min/max) et construit les variables métier : volumes de pages, activation des options, intensité SEO, volumes de contenus/visuels, réglages financiers et paramètres d'import. 【F:index.html†L2075-L2180】
- **Coût d'import** : `computeImportCost()` calcule le coût total d'import d'articles par batch avec dégressivité (`coût × dégressif^batchIndex`) et renvoie le nombre de batchs. 【F:index.html†L2181-L2196】
- **Volume par tâche** : `getTaskVolume()` associe une clé de volume à chaque tâche (pages, options, blog, etc.) pour multiplier les heures de base. 【F:index.html†L2197-L2228】
- **Heures et coûts** : `recalcAll()` lit les paramètres, calcule pour chaque tâche : `heures = baseHours × volume × complexité` puis `coût = heures × taux horaire`. Les tâches d'import utilisent le coût calculé par `computeImportCost`. 【F:index.html†L2389-L2492】
- **Totaux et prix de vente** : le total des coûts alimente le **buffer imprévus** (`coût × buffer/100`), puis le **prix conseillé** (`(coût + buffer) × marge`) et sa conversion MGA (`prix × taux de change`). 【F:index.html†L2494-L2509】
- **Mises à jour UI** : les totaux, résumés et filtres sont rafraîchis après chaque modification de champ ou de filtre, et l'état peut être exporté/importé en JSON ou en CSV pour les tâches visibles. 【F:index.html†L2521-L2562】【F:index.html†L2573-L2644】

## Variables et constantes clés

- **Rôles** : liste `roles` avec identifiant, libellé, taux horaire par défaut, note et icône (Chef de projet, Webdesigner, Développeur WordPress, Graphiste, Rédacteur/SEO, QA). 【F:index.html†L1498-L1551】
- **Tâches** : tableau `tasks` décrivant la phase, le rôle, les heures de base et la clé de volume associée pour chaque activité (cadrage, design, graphisme, développement, contenus, SEO, recette, formation). 【F:index.html†L1597-L1870】
- **Presets de site** : objet `SITE_PRESETS` pour les types *landing*, *vitrine* et *vitrine avancée* ; chaque preset remplit les champs du formulaire (pages, options, SEO, marge, buffer, import). 【F:index.html†L1875-L1990】
- **Paramètres surveillés** : `PARAM_INPUT_IDS`/`ALL_INPUT_IDS` répertorient les champs pris en compte pour les calculs et les exports (volumes, options, finance, import, commentaire). 【F:index.html†L2046-L2074】【F:index.html†L2554-L2562】
- **Filtres et états UI** : `activeRoleFilter`, `hideZeroCost` et `lastTotals` contrôlent respectivement le filtre par rôle, l'affichage des tâches à 0 € et la comparaison des totaux. 【F:index.html†L1543-L1550】【F:index.html†L2265-L2329】

## Pistes d'amélioration

- **Personnalisation avancée des tâches** : permettre d'ajouter/éditer des tâches et de choisir le rôle associé directement dans l'interface, avec persistance dans l'export JSON.
- **Décomposition des phases** : autoriser des coefficients spécifiques par phase (design, dev, SEO…) pour moduler la complexité autrement que par un facteur global.
- **Bibliothèque de presets** : offrir l'enregistrement de presets personnalisés (par secteur, par stack technique) et un partage facile via URL ou QR code.
- **Gestion des risques** : ajouter des lignes de contingence paramétrables (maintenance, TMA, hébergement) et des marges distinctes par type de coût.
- **Accessibilité et collaboration** : prévoir un mode impression/PDF, un verrouillage des champs pour partager un chiffrage en lecture seule, et une option multi-devise avec taux de change multiples.

