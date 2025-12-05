# Calculateur de devis – vitrines et boutiques e-commerce

Deux estimateurs autonomes aident à chiffrer des sites vitrines et des boutiques WooCommerce sans dépendance externe. Chaque calculateur est un fichier HTML autoporté que l’on ouvre directement dans le navigateur.

## Fichiers inclus
- `index.html` : calculateur pour sites vitrines/landing pages, avec tableau des tâches, filtres par rôle et export CSV.
- `ecommerce.html` : calculateur e-commerce avec modules produits, catégories, paiement/livraison, multilingue, chatbot et identité visuelle.
- `assets/` : styles et visuels partagés par les deux pages.

## Prise en main rapide
1. Ouvre le fichier voulu dans un navigateur moderne (double-clic ou « Ouvrir avec… »).
2. Choisis un preset pour injecter des valeurs de départ.
3. Ajuste les volumes, options et tarifs horaires selon le projet.
4. Consulte les résumés (volumes, coûts, prix conseillés) et exporte/importes la configuration au format JSON.

## Calculateur site vitrine (`index.html`)
- **Presets de site** : landing page, vitrine, vitrine avancée ; le bouton *Reset* réapplique les valeurs du preset sélectionné.
- **Volumes & options** : nombre de pages home/interne/légale, complexité globale, services, réalisations, blog (articles, visuels, SEO), logo/charte, formation et paramètres financiers (buffer imprévus, marge, taux €→MGA).
- **Tâches & tarifs** : tableau des rôles avec taux horaires éditables ; chaque modification relance le calcul du coût freelance, du prix conseillé HT et de la conversion MGA.
- **Exports** : sauvegarde/chargement JSON des paramètres et export CSV du tableau filtré (par rôle ou en masquant les tâches à 0 €).

## Calculateur e-commerce (`ecommerce.html`)
- **Presets WooCommerce** : démarrage, standard et catalogue étendu couvrant trois niveaux de complexité produit/catégorie.
- **Pages & contenus** : volumes de pages principales, intensité SEO, blog (activation, articles, visuels, optimisation), import d’articles par batch avec dégressivité.
- **Catalogue produit** : fiches produit, variations, gabarits supplémentaires, rédaction/SEO produit, catégories (gabarits, listing, SEO) et estimation de profilage paiement/livraison.
- **Multilingue & chatbot** : bascule de traduction (aucune, GTranslate, WPML) avec volumes pages/produits à traduire ; trois offres chatbot (plugin, externe, sur-mesure) avec heures et abonnements paramétrables.
- **Identité & options** : module logo (pistes, exports), charte graphique/templating, formation, hébergement/domaine, marge, buffer, taux de change et presets de taux horaires (freelance/offshore/Europe).
- **Exports** : sauvegarde/chargement JSON des paramètres et export CSV du tableau des tâches visibles.

## Conseils d’utilisation
- Renseigne un intitulé de projet pour générer des exports horodatés faciles à retrouver.
- Ajuste les filtres (rôle, masquage des tâches à 0) pour préparer un devis synthétique à partager.
- Modifie les taux horaires ou la complexité pour simuler plusieurs scénarios de marge avant l’envoi au client.
