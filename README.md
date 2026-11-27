# TANIT-GESS – Serveur gratuit (GitHub + Netlify)

TANIT SECURITY S.A.R.L – Sécurité • Vidéosurveillance • Réseaux

## État actuel du dépôt

Le dossier `public/` contient uniquement une page d’état provisoire pour permettre le déploiement sur Netlify. L’application web, les téléchargements et l’API de synchronisation ne sont pas disponibles dans cette version.

Pour publier l’application complète, restaurez le dossier `public/` d’origine (en remplaçant `public/index.html`) et le dossier `netlify/functions/` d’origine, notamment `netlify/functions/api.mjs`. Vérifiez ensuite le déploiement avant de suivre les instructions de connexion ci-dessous.

## Application complète

Une fois les fichiers d’origine restaurés, ce dépôt héberge :
- **l'application web** (même interface que l'APK) : `public/` ;
- **l'API de synchronisation** : `netlify/functions/api.mjs` ;
- **la base de données en ligne** : Netlify Blobs (gratuit, aucun serveur à gérer).

```
   Logiciel PC  ⇄  Serveur Netlify (base + sauvegardes)  ⇄  APK Android / application web
```

Le serveur fonctionne seul, **même quand le PC est éteint** :
- les devis, factures et clients créés sur le téléphone sont gardés sur le serveur ;
- les autres téléphones les voient tout de suite ;
- le PC les intègre à sa base dès qu'il est rallumé.

---

## 1. Créer le dépôt GitHub (5 min)

1. Créez un compte sur https://github.com, puis **New repository**.
2. Nom : `tanitsecurity`. Cochez **Private**.
3. Cliquez **Add file → Upload files**.
4. Glissez **tout le contenu** de ce dossier (`netlify/`, `public/`, `outils/`, `netlify.toml`, `package.json`, `package-lock.json`, `README.md`, `.gitignore`).
5. Validez avec **Commit changes**.

> Ne publiez jamais votre clé sur GitHub.

## 2. Publier sur Netlify (5 min)

1. Créez un compte sur https://app.netlify.com en choisissant **« Sign up with GitHub »**.
2. Cliquez **Add new site → Import an existing project → GitHub**, puis choisissez `tanitsecurity`.
3. Laissez les réglages proposés : ils sont lus dans `netlify.toml`. Cliquez **Deploy**.
4. Renommez le site dans **Site configuration → Change site name**, par exemple `tanit-gess`. L'adresse devient **https://tanit-gess.netlify.app**.

**Aucune clé à configurer sur Netlify** (rien de payant) : la clé est choisie dans le logiciel PC.
La **première** clé envoyée au serveur (12 caractères minimum) devient définitivement sa clé ; toute autre clé est ensuite refusée.
Branchez donc le PC **juste après** la mise en ligne.

Pour vérifier : ouvrez `https://tanit-gess.netlify.app/api/ping`. La page doit afficher `"serveur":"ok"`.

## 3. Brancher le logiciel PC

Dans TANIT-GESS 2.0 :
1. Cliquez **🌐 Serveur**.
2. Saisissez l'adresse `https://tanit-gess.netlify.app` et **votre clé** (choisissez-la : 12 caractères minimum, lettres et chiffres — notez-la bien).
3. Cochez la case d'activation, cliquez **Tester**, puis **Enregistrer et synchroniser**.

Ensuite, tout est automatique :
- **à chaque ouverture**, une copie de sauvegarde est créée dans `Documents\TANIT-GESS\Sauvegardes` (les 60 dernières sont gardées) ;
- toutes les **2 minutes**, le logiciel récupère les saisies du téléphone et envoie les données à jour ;
- la **base complète** est envoyée au serveur à l'ouverture, toutes les 6 heures et à la fermeture ;
- le serveur garde **une sauvegarde par jour pendant 60 jours** ;
- **🌐 Serveur → Restaurer** récupère une base sauvegardée sur le serveur, par exemple sur un nouveau PC.

## 4. Brancher le téléphone

- **APK** : installez `TANIT-GESS_Mobile.apk` (version 2.1). Choisissez **Se connecter au serveur**, puis saisissez l'adresse et la clé.
- **Sans APK** : ouvrez `https://tanit-gess.netlify.app` dans Chrome, puis **⋮ → Ajouter à l'écran d'accueil**.

## 5. Mettre les installateurs en téléchargement (facultatif)

Dans GitHub, ouvrez **Releases → Create a new release**, avec le tag `v2.0`. Joignez :
- `TANIT-GESS_Installation.exe` ;
- `TANIT-GESS_Mobile.apk`.

La limite est de 2 Go par fichier dans les Releases. Remplacez ensuite `VOTRE-COMPTE` dans `public/telechargements.html` par votre nom GitHub. La page `/telechargements.html` donne alors les liens directs.

## Limites de l'offre gratuite Netlify

- **300 crédits par mois.** Chaque déploiement en production coûte 15 crédits. Évitez donc de modifier GitHub plusieurs fois par jour.
- La synchronisation ordinaire consomme très peu de crédits.
- Si les crédits sont épuisés, le site est mis en pause jusqu'au mois suivant. Le logiciel PC continue de fonctionner avec sa base locale.
- Les fichiers PDF, Word et Excel d'origine (Archives) restent sur le PC et sur Google Drive/OneDrive. Seules les données vont sur le serveur.

## Essai sur le PC (développeurs)

```
npm install
node outils/serveur_local.mjs   →  http://localhost:8899
```
