# Team Famille — l'app qui transforme l'entraînement en jeu

Une application pour toute la famille : **XP, niveaux, quêtes, badges, défis mensuels et courbe de progression**.
Vélo (MyWhoosh), course à pied, natation, renforcement doux avec élastique, marche — chacun son sport, ses objectifs, son historique.

Aucun compte, aucun serveur à payer, **aucune donnée ne quitte l'appareil**.

---

## 1. Installer l'app sur les téléphones (2 minutes)

Le principe : on pose le dossier sur une adresse web gratuite, puis chaque téléphone « installe » l'app depuis cette adresse.

### Le plus rapide : Cloudflare Drop (sans compte)

1. Sur l'ordinateur, aller sur **`https://www.cloudflare.com/drop/`** (fonctionnalité lancée en juillet 2026).
2. **Glisser-déposer le dossier `velo-quest-app`** (ou le zip `team-famille.zip`) sur la page.
3. Une **URL publique en https** s'affiche immédiatement. Le déploiement vit 60 minutes : tant qu'on est dans ce délai, cliquer sur **« Claim »** pour le rendre permanent avec un compte Cloudflare gratuit (c'est là que ça devient durable).
4. Ouvrir cette URL sur le téléphone de chacun → installer (voir § 2).

> Alternative sans compte non plus : `static.app` (déposer le zip, il devient un site en ligne, il faut juste une adresse e-mail gratuite).

### Si tu préfères une adresse à toi (gratuit, plus stable)

- **GitHub Pages** : dépôt public `team-famille` **initialisé avec un README** (sinon pas de branche `main`, pas d'upload possible) → « Add file ▸ Upload files » → déposer le **contenu** du dossier (les 8 fichiers, pas le `.zip`, pas le dossier) → un fichier vide `.nojekyll` → Settings ▸ Pages ▸ Deploy from a branch ▸ `main` ▸ `/ (root)` → l'app est sur `https://ton-pseudo.github.io/team-famille/`. Pas d'expiration, contrairement à un lien Drop.
  → La procédure complète, écran par écran, et l'installation sur Android/iPhone : **`DEPLOIEMENT-GITHUB.md`** (à côté de ce README ; lui, tu n'as pas besoin de l'envoyer sur GitHub).
- **Netlify Drop** (`https://app.netlify.com/drop`) : glisser le dossier, ça donne une adresse. Netlify est aussi utilisable en local avec l'onglet « Deploys ».
- **Cloudflare Pages** : le plus pérenne, gratuit, illimité en trafic.

⚠️ **Important** : déposer le **contenu du dossier** (`index.html`, `sw.js`, `manifest.webmanifest`, les icônes) à la racine, pas un sous-dossier. Sinon le service worker et le manifest ne sont pas trouvés, et l'installation est refusée.

## 2. Installer vraiment (icône sur l'écran d'accueil)

| Téléphone | geste |
|---|---|
| **Android / Chrome** | menu **⋮** → **« Installer l'application »** (ou « Ajouter à l'écran d'accueil ») |
| **iPhone / Safari** | bouton **Partager** → **« Sur l'écran d'accueil »** |

Une fois installée, l'app s'ouvre **en plein écran, sans barre de navigateur, et fonctionne hors connexion** (garage, cave, train) : le service worker garde une copie du site.

Pour chaque membre de la famille : la même adresse, chacun **crée son propre profil** dans l'onglet Famille. Sur un même téléphone, on bascule d'un profil à l'autre en tapant l'avatar en haut de l'écran.

## 3. Mettre à jour plus tard

1. Modifier le fichier `index.html` (ou me demander).
2. Redéposer le dossier sur le même hébergeur (par-dessus l'ancien).
3. **Changer `CACHE_VERSION` dans `sw.js`** (ex. `tf-2026-10-05a`), sinon les téléphones gardent l'ancienne version en cache.
4. Fermer puis rouvrir l'app (deux fois la première fois, le temps que le nouveau service worker prenne la main).

---

## Comment ça marche

### L'XP, moteur du jeu

| Ce que tu fais | Ce que ça rapporte |
|---|---|
| Une minute de vélo | 2 XP |
| Une minute de course ou de natation | 3 XP |
| Une minute de renforcement | 2 XP |
| Chaque séance, quelle que soit sa durée | +25 XP |
| Séance à intensité 😮 / 🔥 | +10 / +30 XP |
| Séance marquée HIIT / fractionné | +50 XP |
| Séance de 60 / 90 / 120 min ou plus | +20 / +30 / +50 XP |
| Dénivelé | +0,2 XP par mètre |
| Longueurs de piscine | +0,5 XP par longueur |
| Une pesée | +20 XP |
| Une habitude alimentaire cochée | +5 XP |
| Joker repas libre | +30 XP |
| Un kilo perdu | +100 XP |
| Un kilomètre (objectif distance) | +20 XP |
| Un défi du mois vaincu | +300 XP |
| Un badge | +100 XP |

10 niveaux, avec des **noms qui suivent le sport** : « Cyclo du dimanche » → « Maillot Jaune » à vélo, « Élastique tendu » → « Colonne d'acier » en renforcement, « Dauphin » → « Or olympique » en natation.

**Rien n'est jamais retiré.** Un badge gagné reste gagné, un kilo reperdu ne fait pas disparaître le record, une semaine vide ne coûte rien. L'XP ne peut que monter.

### L'alimentation, sans jamais compter

Trois règles, et une seule case à cocher par règle :

1. **½ assiette de légumes** midi et soir
2. **Zéro calorie liquide** (ni soda, jus, sirop, alcool)
3. **Une portion de protéine** à chaque repas

Plus une quatrième optionnelle (« 20 minutes dehors ») et une **habitude personnalisée** par personne. Objectif d'une quête : **3 jours sur 7**, la semaine « propre » étant fixée à 5 sur 7. Et une **carte Joker** : un repas totalement libre par semaine, prévu dans le règlement, sans justification.

Aucun champ de calories nulle part. Pas d'aliment interdit, pas de régime, pas de compensation.

### Les quêtes de la semaine (remise à zéro le lundi, sans punition)

- 2 séances · 60 à 150 min cumulées selon le profil · 3 jours propres · 1 pesée

### Les défis du mois

Huit boss par personne, un par mois, jusqu'en avril 2027, **sur de vrais parcours**.
Exemples côté vélo : *Bruges* (10,6 km, plat, septembre 2026) → *Golden Gate Bridge* (12,2 km / 100 m D+) → *Mystic Metropolis* → l'anneau de *Bhutan* (22,8 km / 370 m) → *Ascend* à Hudayriyat → le *Blaze Climb* ×2 → *Coast and Country* (57,8 km / 815 m) → le boss final **Blaze and Blizzard** (23,9 km / 1 014 m D+, avril 2027).
Côté renforcement, c'est « 10 jours d'élastique », « 200 squats », « 30 jours de gainage », et le boss final : **30 minutes sans téléphone**. C'est le plus dur de tous.

### Les préférences de séances

Chacun déclare **ses créneaux réels** (15, 20, 30, 45, 60, 90 min) et **son style** — « très court et intense (HIIT) », « mélange » ou « long et doux ». Le catalogue de séances se re-trie en conséquence : à un cycliste qui n'a que 20 minutes et aime souffrir peu de temps, on propose des Tabata et des 30/30 ; à une maman qui veut du doux, on propose mobilité et élastique, jamais du fractionné en tête de liste. Si aucune séance ne tient dans le créneau, l'app le dit au lieu de faire semblant.

### Chacun choisit son prénom (ou son surnom)

Le champ **Prénom ou surnom** est la première question de l''éditeur de profil : c''est toi qui l''écris. « Maman », « Papa », « Léa » ne sont que des **pastilles de suggestion** sous le champ — un tap les copie dans la case, tu peux aussi taper ce que tu veux (« Julie », « Coco », « Maman-Course »…).

- **Le prénom est obligatoire** (sinon le classement et le duel ne sauraient pas à qui attribuer les points) : si tu valides sans rien écrire, l''app ne crée rien et te repose la question, sans message rouge ni drame.
- **18 caractères maximum**, pour que le classement tienne sur une ligne.
- **Pas de doublon** : la comparaison ignore les majuscules et les accents (« Julie » = « julie »), et l''app te demande d''en changer un. À l''import d''une base, deux homonymes sont numérotés (« Papa 2 ») plutôt que fusionnés par erreur.
- Les préréglages famille (`👩 Maman en 1 clic`) **laissent la case vide** exprès : rien n''est collé dans son dossier.

### Un objectif de poids par profil (et aucun si tu n’en veux pas)

Chaque profil a **son propre** objectif : type (kg, km ou minutes), valeur de départ, valeur actuelle, cible, date de début, échéance. Ça se règle dans **Famille ▸ Éditer**, et c’est la même fenêtre qui crée un profil : l’app demande donc le poids de départ à qui choisit « Perdre du poids (kg) » — elle ne le devine jamais.

- **Rien n’est obligatoire.** Laisse le départ vide : l’app continue de compter les séances, les quêtes, les badges et le niveau, sans jamais regarder la balance. Le classement famille, lui, est toujours en **minutes**, jamais en kilos.
- **Pendant la saisie**, une ligne calcule l’allure : « 6 kg en 32 semaines = 0,19 kg par semaine · allure confortable ». C’est une droite de progression, pas un verdict.
- **Le poids de départ du premier profil** (le tien) est pré-rempli depuis un bloc repérable en tête du `index.html` :

```js
/* ⚠️  À PERSONNALISER */
const PROFIL_DEFAUT={name:"Papa",emoji:"🚴",sport:"velo",
  times:[20,30,45],int:"hiit",weeklyMin:150,
  kg:{start:87,target:72,until:"2027-04-30"}};
```

Change ces chiffres (ou passe `start:null` pour que l’app redemande le poids à chaque création). Les préréglages famille — `Maman en 1 clic` sur l’écran d’accueil —, eux, **laissent toujours le poids vierge** : c’est à chacun de saisir le sien.

### Ton objectif, en chiffres

Départ 87 kg le 18/09/2026 → cible 72 kg le 30/04/2027 = **32 semaines, 0,47 kg par semaine**.
La courbe compare à la trajectoire idéale et annonce une avance ou un léger retard en kilogrammes — jamais un jugement. Si le rythme visé dépasse 1,2 kg/semaine, l'app propose gentiment de ralentir : c'est ce qui fait tenir jusqu'au bout.

### Un appareil ou dix, au choix

Les données vivent dans le navigateur de chaque appareil (`localStorage`). Deux possibilités :

- **Un appareil par personne** : chacun son app, son score, son intimité. Rien à synchroniser.
- **Un compte pour la famille** (le même sur le téléphone et l'ordi) : onglet Famille → **« Copier le code »**, puis « Importer » sur l'autre appareil. L'import **fusionne** au lieu d'écraser : pas de doublon de séance, les badges se complètent. « Exporter en fichier » produit un `.json` de secours à garder.

### Le duel famille (⚔️) — 100 % gratuit, sans serveur

Toi contre Maman sur les minutes de la semaine, ou toute la famille sur les séances. Le perdant paie le pari (la vaisselle, les poubelles, la sortie vélo du dimanche imposée). **Coût : zéro euro, zéro compte, zéro abonnement.** Rien ne quitte les téléphones : pas de base de données, pas d'API, pas de compte à créer.

Comment ça marche :

1. Onglet **Duel → Lancer un duel** : le nom, le pari, le terrain de jeu (minutes de sport, nombre de séances, jours avec une habitude cochée, quêtes bouclées), la durée en semaines, et l'objectif de chacun.
2. **Chacun compte chez soi.** Le score de la semaine se lit automatiquement dans les séances déjà saisies sur le téléphone de chacun — rien à noter de plus.
3. **Une fois par semaine, on échange un code** (bouton « Échanger les scores »). Une soixantaine de caractères, préfixés `TFD1-`, à coller dans la conversation famille ou à se passer de main en main. L'import fusionne la semaine ; il ne **baisse jamais** un score déjà accordé.
4. **3 points** au gagnant de la semaine, **+1** à qui tient son objectif. Le classement s'affiche en direct.

Deux façons de jouer, au choix :

- **À distance** : chacun son téléphone, on s'envoie les codes le dimanche soir. 40 secondes à trois.
- **Ensemble, sur le canapé** : on se passe le téléphone et on appuie sur le nom de celui qui a gagné la semaine (« Donner le point »). Pas de code du tout, on compte à la loyale.

Le terrain de jeu se choisit **par joueur** : papa peut viser 150 minutes, maman 90, la petite 60. Le score reste donc honnête entre un coureur et une séance d'élastique. Deux badges s'y collent : « À toi de jouer » (une semaine de duel jouée) et « Trois semaines de guerre » (trois objectifs tenus d'affilée).

Et si un jour l'automatisation totale (les codes qui circulent seuls) te tente, il faudra un petit backend — un compte Cloudflare Workers au palier gratuit suffit largement pour une famille, donc ça reste gratuit, mais avec un compte quelque part. Ce n'est pas le choix retenu ici : **la version actuelle fonctionne sans rien créer du tout.**

## Le fond, derrière le jeu

- **80 % du temps à 😌 ou 🙂** : tu dois pouvoir parler. C'est ce qui construit l'endurance sans te casser.
- **Après 5 ans d'arrêt, le cardio revient en 3-4 semaines, les tendons en 8-12.** Le piège classique de la reprise sur home trainer connecté, c'est de rouler au ressenti du chiffre de puissance. Ce plan bride exprès les 3 premières semaines.
- **Le HIIT : 1 à 2 séances par semaine maximum.** C'est efficace et court, c'est pour ça qu'on en voudrait tous les jours.
- **Une pesée par semaine**, le même jour, au réveil, à jeun. Un +1 kg le lendemain d'une crêpe, c'est de l'eau : seul le trend du mois compte.
- **Les heures de selle valent plus que la balance.** Si une semaine est blanche, l'objectif n'est pas de « rattraper » par deux heures de vélo en punition, mais d'être là la semaine suivante.

## Écran vide ? Ce qu’il faut savoir

Si l’adresse s’ouvre sur un bandeau sombre sans rien dessous, l’app affiche désormais une carte « **Oups** » avec le message d’erreur exact de Chrome (au lieu d’un écran muet). Les deux causes possibles, dans l’ordre :

1. **une extension bloque les scripts inline** sur ce site → ajouter `ton-domaine.github.io` à la liste blanche, ou tester en navigation privée (extensions désactivées) ;
2. **la page est ouverte dans un navigateur intégré** (aperçu d’un lien, messagerie, navigateur d’un autre site) → copier l’adresse et la coller dans une vraie fenêtre de Chrome, Safari, Edge ou Firefox.

Diagnostic complet dans la console (F12) en tapant `tfCheck()` : ça répond si le script a tourné, si les données sont chargées, si le manifeste et le service worker sont là.

Note pour iPhone : l’app reste stockée dans le navigateur **de chaque téléphone**. Une sauvegarde mensuelle par « Exporter en fichier » (onglet Famille) reste le seul vrai garde-fou.

## Contenu du dossier

```
index.html              l'app entière (HTML + CSS + JS, aucune dépendance externe)
sw.js                   service worker → fonctionnement hors connexion
manifest.webmanifest    nom, icônes, couleurs, raccourcis d'app
icon.svg                icône vectorielle
icon-192.png / icon-512.png / icon-maskable-512.png
```

Aucune bibliothèque, aucun CDN, aucune analyse ni tracking : le fichier `index.html` peut aussi s'ouvrir seul, en double-clic, sur un ordinateur.

### Les tests (optionnels)

`tests/` contient 359 vérifications automatiques de l'app : barème d'XP, quêtes, courbe de poids, cloisonnement des profils, import/export, logique des duels (score, départage, codes, matchs nuls), rendu de chaque écran dans un navigateur simulé. Elles ont servi à écrire et à corriger l'app ; elles servent à vérifier qu'un changement n'a rien cassé.

```sh
cd tests && sh run.sh      # installe jsdom à la demande, puis tout exécute
```

Résultat attendu : `Suite A (maths de l'app) : 150/150 ✓` et `Suite B (UI) : 122/122 ✓`.
