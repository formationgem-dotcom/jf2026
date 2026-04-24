# 🚀 Guide de déploiement — Filtering Game JF2026

Deux étapes : **créer une base de données Firebase** (gratuit) puis **mettre le site en ligne sur GitHub Pages** (gratuit).
Durée totale estimée : **20 minutes**.

> **Nouveautés V3** : triple défi par produit — **diagnostic Filtering/Réparation + saisie du N° de série + saisie du mot-clé SAVVY** (caché dans la contribution de base de connaissances liée au produit).

---

## Aperçu du scoring

| Action | Points |
|--------|-------:|
| ✅ Filtering correct | +2 |
| ✅ Réparation correcte | +1 |
| ❌ Erreur Filtering / Réparation | −1 |
| 🔖 N° de série correct | +1 |
| ❌ N° de série erroné | −1 |
| 🔑 Mot-clé SAVVY correct | +1 |
| ❌ Mot-clé SAVVY erroné | −1 |

- **Diagnostic** : les boutons **Filtering** ou **Réparation** s'affichent sur la fiche produit.
- **N° de série** : champ de saisie sur la même page (étiquette produit).
- **Mot-clé SAVVY** : champ de saisie sur la même page. L'équipe doit **ouvrir la contribution SAVVY** du produit (QR ou lien) et y repérer le mot-clé volontairement inséré — cela force la lecture avant d'agir.
- L'équipe valide les **3 réponses ensemble** avec un seul bouton.
- Le classement affiche une **colonne par atelier** (ASP / CAF / MUL) + une **colonne bonus globale N° Série** + une **colonne bonus globale Mot-clé SAVVY**.

---

## ÉTAPE 1 — Créer la base de données Firebase

Firebase est le service Google qui stocke les réponses des équipes en temps réel.

### 1.1 Créer un projet Firebase

1. Allez sur **[firebase.google.com](https://firebase.google.com)**
2. Cliquez sur **"Commencer"** (connectez-vous avec un compte Google)
3. Cliquez sur **"Ajouter un projet"**
4. Nom du projet : `jf2026-filtering` → Continuer
5. Désactivez Google Analytics (pas nécessaire) → **Créer le projet**

### 1.2 Créer la base de données Realtime

1. Dans le menu gauche : **Création → Realtime Database**
2. Cliquez **"Créer une base de données"**
3. Choisissez la région **Europe-ouest** → Suivant
4. Sélectionnez **"Commencer en mode test"** → Activer

> ⚠️ Le mode test autorise toutes les lectures/écritures pendant 30 jours.
> Suffisant pour un événement ponctuel.

### 1.3 Récupérer la configuration Firebase

1. Dans le menu gauche : ⚙️ **Paramètres du projet** (roue dentée)
2. Onglet **"Général"** → descendez jusqu'à **"Vos applications"**
3. Cliquez sur l'icône **`</>`** (Web)
4. Nom de l'app : `filtering-game` → **Enregistrer l'application**
5. Copiez le bloc `firebaseConfig` qui s'affiche — il ressemble à ceci :

```js
const firebaseConfig = {
  apiKey: "AIzaSy...",
  authDomain: "jf2026-filtering.firebaseapp.com",
  databaseURL: "https://jf2026-filtering-default-rtdb.europe-west1.firebasedatabase.app",
  projectId: "jf2026-filtering",
  storageBucket: "jf2026-filtering.appspot.com",
  messagingSenderId: "123456789",
  appId: "1:123456789:web:abc123"
};
```

---

## ÉTAPE 2 — Coller la config dans les fichiers HTML

Ouvrez **`index.html`** et **`leaderboard.html`** avec un éditeur de texte (Bloc-notes, Notepad++, VS Code…).

Dans les deux fichiers, cherchez le bloc `FIREBASE_CONFIG` et remplacez les valeurs par vos vraies valeurs Firebase.

> ⚠️ Ne modifiez rien d'autre. Sauvegardez les deux fichiers.

---

## ÉTAPE 3 — Renseigner les N° de série ET les mots-clés SAVVY attendus

C'est **l'étape clé** avant l'événement. Deux champs à renseigner pour chacun des 45 produits :

- `serial:"SN-ASP-001"` → à remplacer par le **vrai N° de série** du produit physique en atelier (étiquette constructeur).
- `keyword:"MOT-ASP-001"` → à remplacer par le **mot-clé que vous aurez caché** dans la contribution SAVVY liée au produit (par ex. un mot à repérer dans la procédure : `FILTRE`, `MOTEUR`, `VEILLE`, etc.).

### 3.1 Ouvrir `index.html`

Cherchez le bloc `const PRODUCTS = {` (vers la ligne 190).

### 3.2 Pour chaque produit, remplacer les champs `serial` ET `keyword`

Exemple avant :

```js
"ASP-01":{workshop:"asp", type:"Aspirateur traîneau", serial:"SN-ASP-001", keyword:"MOT-ASP-001",
  symptom:"Depuis quelques semaines, mon aspirateur n'aspire presque plus rien...",
  ...
}
```

Exemple après :

```js
"ASP-01":{workshop:"asp", type:"Aspirateur traîneau", serial:"RF71R-14587324A", keyword:"FILTRE",
  symptom:"Depuis quelques semaines, mon aspirateur n'aspire presque plus rien...",
  ...
}
```

> 💡 **Tolérance de saisie** (identique pour série ET mot-clé) : la validation ignore la casse, les espaces, les tirets et underscores. `filtre`, `FILTRE` et `Filtre` sont donc équivalents.

### 3.3 Parcourir les 45 produits

- `ASP-01` à `ASP-15` → 15 produits Aspiration
- `CAF-01` à `CAF-15` → 15 produits Broyeurs Café
- `MUL-01` à `MUL-15` → 15 produits Multimédia

> 📌 **Astuce N° série** : imprimez les étiquettes-repère (code produit + vraie référence SAV) et collez-les physiquement sur les appareils en atelier. Le N° de série doit rester sur la carte produit existante (étiquette constructeur).
>
> 📚 **Astuce Mot-clé SAVVY** : privilégiez des mots **simples, courts et mémorisables** (5 à 10 lettres), directement en lien avec la procédure décrite. Intégrez-les dans la contribution SAVVY de façon volontairement visible mais pas en titre — l'objectif est de garantir que l'équipe a bien **lu la fiche** avant de se prononcer.

---

## ÉTAPE 3 bis — (Optionnel) Ajouter une vidéo symptôme via Vimeo

Certains produits peuvent être accompagnés d'une **courte vidéo du symptôme** (ex. aspirateur qui fume, TV avec lignes verticales). Une vignette cliquable s'affiche alors dans la fiche produit — au clic, la vidéo s'ouvre en modale plein écran avec lecteur Vimeo natif.

### 3bis.1 Uploader la vidéo sur Vimeo (compte gratuit)

1. Créez un compte sur **[vimeo.com](https://vimeo.com)** (plan gratuit = 500 Mo d'upload par semaine).
2. Cliquez **"+ New video"** → **"Upload"** → sélectionnez votre fichier `.mp4`.
3. Une fois l'upload terminé, ouvrez la vidéo et allez dans **Settings → Privacy**.
4. Réglez **"Who can watch"** sur **"Unlisted"** (Non répertoriée) — la vidéo devient invisible en recherche mais intégrable partout via son lien direct.
5. Dans **"Where can this be embedded?"**, laissez **"Anywhere"**.
6. Notez l'**ID numérique** de la vidéo, visible dans son URL : `https://vimeo.com/1185440837` → ID = `1185440837`.

### 3bis.2 Remplir les champs vidéo dans `index.html`

Ouvrez `index.html`, retrouvez le produit concerné (ex. `"ASP-03"`) et ajoutez les champs `vimeoId` et `videoRatio` :

```js
"ASP-03":{workshop:"asp", type:"Aspirateur traîneau", serial:"SN-ASP-003", keyword:"MOT-ASP-003",
  vimeoId:"1185440837", videoRatio:"1/1",   // ← vidéo carrée Vimeo
  symptom:"Une odeur de brûlé se dégage de l'appareil lorsqu'il fonctionne.",
  correct:R, points:1, explanation:"..."}
```

Champs disponibles :

| Champ | Obligatoire | Valeur | Usage |
|-------|:---:|-------|-------|
| `vimeoId` | Oui | `"1185440837"` | ID numérique Vimeo (sans l'URL) |
| `videoRatio` | Non | `"1/1"` ou `"16/9"` | Format de la vignette. Défaut : `"16/9"` |
| `videoPoster` | Non | URL vignette personnalisée | Par défaut, vignette auto-générée via `vumbnail.com/<id>.jpg` |

> 💡 **Les produits sans vidéo** (aucun champ `vimeoId`) affichent uniquement le texte client, exactement comme avant. Aucune régression.
> 🎬 **Bonne pratique** : limitez chaque vidéo à 15-45 secondes et un format carré (1:1) ou vertical — plus lisible sur smartphone après scan QR.

### 3bis.3 Tester la vidéo

1. Après avoir sauvegardé `index.html`, ouvrez la fiche du produit (ex. `?p=ASP-03`).
2. La vignette doit apparaître au-dessus de la phrase client, avec un bouton Play central.
3. Au clic, la vidéo s'ouvre en modale — elle se ferme en cliquant hors de la vidéo, sur la croix ✕, ou avec la touche Échap.

---

## ÉTAPE 4 — Mettre en ligne sur GitHub Pages

### 4.1 Créer un compte GitHub (si vous n'en avez pas)

Allez sur **[github.com](https://github.com)** → Sign up → compte gratuit.

### 4.2 Créer un dépôt et uploader les fichiers

1. Cliquez sur le **"+"** en haut à droite → **"New repository"**
2. Nom : `jf2026` — Visibilité : **Public** — Cliquez **"Create repository"**
3. Cliquez **"uploading an existing file"**
4. Glissez-déposez les 3 fichiers : `index.html`, `leaderboard.html`, `README.md`
5. Cliquez **"Commit changes"**

### 4.3 Activer GitHub Pages

1. Dans votre dépôt : onglet **Settings** → menu gauche **Pages**
2. Source : **"Deploy from a branch"**
3. Branch : **main** → dossier **(root)** → **Save**
4. Attendez 1 à 2 minutes → votre site est en ligne à l'adresse :
   `https://VOTRE_PSEUDO.github.io/jf2026/`

---

## ÉTAPE 5 — Générer les QR codes

Chaque produit a un URL unique. Il vous faut **45 QR codes produit + 1 QR code classement**.

### URLs à encoder en QR code

**Atelier Aspiration (15 QR codes) :**
```
https://VOTRE_PSEUDO.github.io/jf2026/?p=ASP-01
https://VOTRE_PSEUDO.github.io/jf2026/?p=ASP-02
...
https://VOTRE_PSEUDO.github.io/jf2026/?p=ASP-15
```

**Atelier Broyeurs Café (15 QR codes) :**
```
https://VOTRE_PSEUDO.github.io/jf2026/?p=CAF-01
https://VOTRE_PSEUDO.github.io/jf2026/?p=CAF-02
...
https://VOTRE_PSEUDO.github.io/jf2026/?p=CAF-15
```

**Atelier Multimédia (15 QR codes) :**
```
https://VOTRE_PSEUDO.github.io/jf2026/?p=MUL-01
https://VOTRE_PSEUDO.github.io/jf2026/?p=MUL-02
...
https://VOTRE_PSEUDO.github.io/jf2026/?p=MUL-15
```

**Classement (1 QR code — à projeter ou afficher) :**
```
https://VOTRE_PSEUDO.github.io/jf2026/leaderboard.html
```

### Générer les QR codes rapidement

Outil recommandé : **[qr-code-generator.com](https://qr-code-generator.com)**

1. Coller l'URL → Générer → Télécharger en PNG (taille min. 400×400 px)
2. Répéter pour chacune des 45 URLs + la page classement

> 💡 Astuce : dans Microsoft Edge, ouvrez chaque URL et faites
> **clic droit → "Créer un QR code pour cette page"** — c'est le plus rapide !

---

## ÉTAPE 6 — Personnaliser les noms d'équipes (optionnel)

Par défaut les équipes s'appellent "Équipe 1" à "Équipe 30" (30 slots communs aux 3 ateliers) — les équipes renseignent elles-mêmes leur nom + leurs membres au premier scan. **Une fois validée, l'inscription est verrouillée** : plus aucune modification possible du nom ni des membres, pas de changement d'équipe. Aucune modif nécessaire côté code.

Si vous voulez pré-remplir des noms d'équipes (ex: "Les Aspirants", "Team Café"…) :

Dans `index.html` **ET** `leaderboard.html`, remplacez :
```js
const TEAMS = Array.from({length: 30}, (_, i) => ({
  id: `E${String(i+1).padStart(2,'0')}`,
  name: `Équipe ${i+1}`
}));
```
par :
```js
const TEAMS = [
  {id:"E01", name:"Les Aspirants"},
  {id:"E02", name:"Team Café"},
  {id:"E03", name:"Les Filtreurs"},
  // ... ajoutez vos vrais noms d'équipes
];
```

---

## Récapitulatif — Le jour J

| Action | Où |
|--------|-----|
| Classement en direct | `leaderboard.html` — à projeter sur écran |
| Les équipes scannent | 45 QR codes sur les fiches produit |
| Saisir le N° de série | Sur la fiche produit, après avoir choisi Filtering / Réparation |
| Saisir le mot-clé SAVVY | Sur la fiche produit, après le N° de série — à trouver dans la contribution SAVVY du produit |
| Réinitialiser les scores | `leaderboard.html` → bouton **Admin** → PIN `2026` → Remettre à zéro |
| Exporter les résultats | Panneau Admin → **📥 Télécharger CSV** (diag + série + SAVVY + membres) |

---

## Répartition du scoring maximum

Le max par atelier dépend du nombre de produits dont la bonne réponse est **Filtering** (+2 pts) ou **Réparation** (+1 pt).

| Atelier | Filtering | Réparation | Max diagnostic | Max N° série | Max Mot-clé SAVVY |
|---------|:---:|:---:|:---:|:---:|:---:|
| 🌪️ Aspiration | 11 | 4 | **26 pts** | 15 pts | 15 pts |
| ☕ Broyeurs Café | 12 | 3 | **27 pts** | 15 pts | 15 pts |
| 🎮 Multimédia | 8 | 7 | **23 pts** | 15 pts | 15 pts |
| **TOTAL** | **31** | **14** | **76 pts** | **45 pts** | **45 pts** |

> Score plafond théorique : **166 pts** (sans faute sur les 45 produits : diag 76 + série 45 + SAVVY 45).
> Score plancher : **−135 pts** (tout faux : −1×45 diag − 1×45 série − 1×45 SAVVY).

---

## En cas de problème

**Les réponses ne s'enregistrent pas**
→ Vérifiez que la `databaseURL` dans Firebase Config contient bien `europe-west1`
→ Vérifiez que la base de données est en **mode test** (pas en production)

**La page ne s'affiche pas**
→ Attendez 2 minutes après l'activation de GitHub Pages
→ Vérifiez que le fichier s'appelle exactement `index.html` (minuscules)

**Le QR code ne fonctionne pas**
→ Testez l'URL directement dans un navigateur avant de générer le QR code

**Le N° de série est toujours rejeté alors qu'il est correct**
→ Ouvrez `index.html`, retrouvez le bon produit (ex: `"ASP-01"`) et vérifiez le champ `serial:"..."` — la tolérance porte sur casse/espaces/tirets/underscores mais pas sur les caractères exotiques (é, ç, ñ…). Utilisez de préférence des caractères ASCII (A–Z, 0–9).

**Le mot-clé SAVVY est rejeté alors qu'il est correct**
→ Même logique : ouvrez `index.html`, produit concerné, vérifiez le champ `keyword:"..."`. Évitez les accents et les caractères spéciaux dans le mot-clé choisi (préférez `MOTEUR` à `Démarreur`). La casse et les espaces sont ignorés.
