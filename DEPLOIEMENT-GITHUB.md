# Mettre Team Famille en ligne (GitHub Pages) et sur les téléphones

Tout est gratuit. Le dépôt ne contient **que le code** de l'app : tes séances, ton poids, tes badges ne montent jamais sur GitHub — ils restent dans le navigateur de chaque téléphone.

---

## A. Le site, en 6 étapes (≈ 6 minutes, 100 % à la souris)

### 1. Créer le compte

Va sur <https://github.com/signup>, choisis un identifiant (ce sera le début de ton adresse), valide l'e-mail.

### 2. Créer le dépôt

<https://github.com/new> →

- **Repository name** : `team-famille` (minuscules, pas d'espace, pas d'accent)
- Coche **Add a README file** ← obligatoire : ça crée la branche `main`, et sans branche on ne peut rien téléverser
- **Public** (Pages ne marche pas en public/gratuit sur un dépôt privé)

Bouton **Create repository**.

### 3. Envoyer les fichiers

Dans le dépôt : **Add file → Upload files**.

Dézippe d'abord le dossier `velo-quest-app` quelque part, puis **sélectionne les 8 fichiers à téléverser** (tu peux faire Ctrl/clic pour en prendre plusieurs d'un coup) et fais-les glisser dans la zone grise :

```
index.html  manifest.webmanifest  sw.js
icon.svg  icon-192.png  icon-512.png  icon-maskable-512.png  README.md
```

> Le site web GitHub n'accepte que des fichiers : pas le `.zip` tel quel (il le garderait comme fichier à télécharger, sans le décompresser), et pas un dossier (il crée un sous-dossier, et c'est la panne garantie). 100 Ko au total, ça passe en une seule fois.
> `DEPLOIEMENT-GITHUB.md` et le dossier `tests/` : inutiles en ligne, ne les envoie pas.

> ⚠️ C'est LE piège : on dépose le **contenu** du dossier, pas le dossier.
> Si tu glisses le dossier lui-même, GitHub crée un sous-dossier `velo-quest-app/`, et ton adresse racine renverra un 404 — exactement la panne que tu as eue avec Cloudflare Drop.

Contrôle avant de valider : la liste doit afficher `index.html`, `sw.js`, `manifest.webmanifest`, `icon-192.png`… **sans chemin devant le nom** — 8 lignes, rien de plus.

Bouton vert **Commit changes**.

### 4. Un fichier pour éviter les surprises

**Add file → Create new file** → nom : `.nojekyll` (aucun contenu) → **Commit changes**.
Ça demande à GitHub de servir les fichiers tels quels, sans les « construire ».

### 5. Activer Pages

Onglet **Settings** (⚙️) → dans la colonne de gauche, section *Code, planning, and automation* → **Pages** →

- **Build and deployment → Source** : `Deploy from a branch`
- **Branch** : `main` et, à droite, le dossier **`/(root)`**
- **Save**

Quelques secondes plus tard, un bandeau vert affiche :

```
Your site is live at https://TON-PSEUDO.github.io/team-famille/
```

### 6. Tester sur l'ordi

Ouvre cette adresse. Tu dois voir l'écran d'accueil de l'app (« Crée ton profil »).
Teste vite fait le manifeste : <https://TON-PSEUDO.github.io/team-famille/manifest.webmanifest> → du texte JSON. Si tu as une image de 404, vois la section **D. Ça ne marche pas** tout en bas.

---

## B. L'application sur les téléphones

Le lien GitHub est maintenant **permanent** : pas de compte à réclamer, pas de délai d'une heure. Chaque membre de la famille fait ça sur **son** téléphone.

### Android (Chrome)

1. Ouvre l'adresse dans **Chrome**.
2. Laisse la page chargée 3 secondes → une bannière « **Installer l'application Team Famille** » apparaît en bas, ou dans la barre d'adresse une petite icône ⬇️/➕.
3. Sinon : menu **⋮** (en haut à droite) → **Ajouter à l'écran d'accueil** → *Installer*.
4. L'icône apparaît : un vrai lancement en plein écran, sans barre d'URL.

### iPhone (Safari — Chrome ne sait pas le faire)

1. Ouvre l'adresse dans **Safari**.
2. Bouton **Partager** (le carré avec la flèche vers le haut, sous l'écran).
3. **Sur l'écran d'accueil** → *Ajouter*.
4. Icône sur l'écran d'accueil, ouverture plein écran.

> Sur iPhone, si le menu « Sur l'écran d'accueil » n'apparaît pas : Réglages → Safari → autorise « Icône d'application web », ou bien réessaie après avoir rechargé la page une fois chargée complètement.

### Sur les autres téléphones / l'ordi

Le même lien marche partout. Si l'installation n'est pas proposée, un simple favori fait tourner l'app (tout est dans la page unique), mais sans mode plein écran.

---

## C. Ce qu'il faut savoir (honnêtement)

- **Avant de téléverser, personnalise ton objectif.** En tête de `index.html`, le bloc `const PROFIL_DEFAUT={...}` (kg de départ, cible, échéance, minutes/semaine) ne sert qu''au premier profil créé par « Commencer par moi » : mets tes chiffres ou passe `start:null` pour que l''app les demande. **Les autres membres ne reçoivent aucun poids** : le préréglage `👩 Maman en 1 clic` ouvre son éditeur avec les cases vides, c''est elle qui remplit — ou qui laisse vide, l''app compte alors séances, quêtes et badges sans jamais parler de balance.
- **Le menu du bas ne cache plus rien.** La page se dégage automatiquement de la hauteur réelle du menu (mesurée, pas supposée) : texte agrandi, paysage, encoche, téléphone plus petit — ça suit tout seul. Si un écran semble encore coupé en bas, tirer la page vers le haut puis attendre une demi-seconde suffit à relancer la mesure.
- **Le prénom, c’est chacun qui l’écrit.** Les préréglages (`👩 Maman en 1 clic`) ouvrent l’éditeur avec la case **vide** : « Maman » n’est qu’une suggestion en un tap, elle met son prénom, un surnom, ce qu’elle veut. Seules règles : un prénom court (18 caractères max) et unique dans la maison — l’app refuse deux « Julie » (majuscules et accents ignorés), sinon le classement et le duel ne sauraient plus qui est qui.
- **Chaque téléphone a sa propre base.** Rien n'est synchronisé tout seul, c'est voulu (zéro serveur, zéro compte). Pour partager une base famille sur un seul appareil, ou la sauvegarder : onglet **Famille → Exporter en fichier** (un `.json`), ou « Copier le code » à coller sur l'autre appareil (l'import fusionne, il n'écrase pas).
- **L'app fonctionne hors connexion** une fois ouverte au moins une fois avec l'icône (le service worker a mis la page en cache).
- **Mise à jour de l'app plus tard** : étape A.3 (upload des nouveaux fichiers) → les téléphones rattrapent la version au prochain lancement. Si un téléphone reste bloqué sur l'ancienne : fermer l'app et la rouvrir, ou fermer l'onglet Safari/Chrome et recharger.
- **Sauvegarde** : exporte le fichier `.json` une fois par mois quelque part (Drive, un dossier). C'est un garde-fou, pas une obligation — mais sur iPhone, iOS purge le stockage d'un site **utilisé pendant 7 jours sans aucune interaction** ; une app ajoutée à l'écran d'accueil a son propre compteur, remis à zéro à chaque fois qu'on l'ouvre, donc en pratiquant une séance quasi quotidienne tu n'y touches jamais. Les jours de repos, ouvrir l'app 2 secondes suffit à repousser la date.

---

## D. Ça ne marche pas : la liste de contrôle

| Symptôme | Cause probable | À faire |
|---|---|---|
| 404 sur l'adresse racine | fichiers dans un sous-dossier | Repo → Code → tu dois voir `index.html` **directement**. Sinon : **Add file → Upload files** sur la page racine et redépose les fichiers à ce niveau (ou renomme/déplace les fichiers via l'éditeur) |
| 404 aussi sur `/team-famille/index.html` | Pages pas activé, ou branche/dossier mal choisis | Settings → Pages → `main` + `/(root)`. Le nom de la branche par défaut peut être `master` : choisis-la |
| Page qui s'affiche mais pas de mode plein écran / pas d'install | `manifest.webmanifest` introuvable ou non servi | Ouvre `/manifest.webmanifest` : si c'est du JSON, tout va bien. Si 404, le fichier manque au dépôt → le retéléverser |
| L'icône n'apparaît pas | Safari utilisé sur Android, Chrome utilisé sur iPhone | Android → Chrome. iPhone → Safari |
| L'app est vide sur un 2ᵉ téléphone | normal : la base vit dans chaque navigateur | Créer les profils sur chaque téléphone, ou importer le code/export famille |
| Vieille version affichée après une mise à jour | cache du service worker | Fermer complètement l'app, rouvrir ; en dernier recours vider les données du site dans les réglages du navigateur |
| Bandeau sombre vide, puis carte « Oups » | extension qui bloque les scripts, ou page ouverte dans le navigateur intégré d'une app | Navigation privée (extensions coupées), ou copier l'adresse dans une vraie fenêtre de Chrome/Safari. F12 → Console → taper `tfCheck()` |

Pour vérifier qu'une adresse est bien servie, colle-la dans un onglet : la racine doit renvoyer la page de l'app (pas un 404 GitHub), et `/manifest.webmanifest` doit afficher du JSON.
