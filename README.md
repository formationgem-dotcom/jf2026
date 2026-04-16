# 🚀 Guide de déploiement — Filtering Game JF2026

Deux étapes : **créer une base de données Firebase** (gratuit) puis **mettre le site en ligne sur GitHub Pages** (gratuit).
Durée totale estimée : **20 minutes**.

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

Dans les deux fichiers, cherchez le bloc `FIREBASE_CONFIG` et remplacez les valeurs `"VOTRE_..."` par vos vraies valeurs :

```js
const FIREBASE_CONFIG = {
  apiKey:            "AIzaSy...",          // ← votre vraie valeur
  authDomain:        "jf2026-filtering.firebaseapp.com",
  databaseURL:       "https://jf2026-filtering-default-rtdb.europe-west1.firebasedatabase.app",
  projectId:         "jf2026-filtering",
  storageBucket:     "jf2026-filtering.appspot.com",
  messagingSenderId: "123456789",
  appId:             "1:123456789:web:abc123"
};
```

> ⚠️ Ne modifiez rien d'autre. Sauvegardez les deux fichiers.

---

## ÉTAPE 3 — Mettre en ligne sur GitHub Pages

### 3.1 Créer un compte GitHub (si vous n'en avez pas)

Allez sur **[github.com](https://github.com)** → Sign up → compte gratuit.

### 3.2 Créer un dépôt et uploader les fichiers

1. Cliquez sur le **"+"** en haut à droite → **"New repository"**
2. Nom : `jf2026` — Visibilité : **Public** — Cliquez **"Create repository"**
3. Cliquez **"uploading an existing file"**
4. Glissez-déposez les 3 fichiers : `index.html`, `leaderboard.html`, `README.md`
5. Cliquez **"Commit changes"**

### 3.3 Activer GitHub Pages

1. Dans votre dépôt : onglet **Settings** → menu gauche **Pages**
2. Source : **"Deploy from a branch"**
3. Branch : **main** → dossier **(root)** → **Save**
4. Attendez 1 à 2 minutes → votre site est en ligne à l'adresse :
   `https://VOTRE_PSEUDO.github.io/jf2026/`

---

## ÉTAPE 4 — Générer les QR codes

Chaque produit a un URL unique. Générez un QR code pour chacun.

### URLs à encoder en QR code

**Atelier Aspiration (15 QR codes) :**
```
https://VOTRE_PSEUDO.github.io/jf2026/?p=ASP-01
https://VOTRE_PSEUDO.github.io/jf2026/?p=ASP-02
https://VOTRE_PSEUDO.github.io/jf2026/?p=ASP-03
https://VOTRE_PSEUDO.github.io/jf2026/?p=ASP-04
https://VOTRE_PSEUDO.github.io/jf2026/?p=ASP-05
https://VOTRE_PSEUDO.github.io/jf2026/?p=ASP-06
https://VOTRE_PSEUDO.github.io/jf2026/?p=ASP-07
https://VOTRE_PSEUDO.github.io/jf2026/?p=ASP-08
https://VOTRE_PSEUDO.github.io/jf2026/?p=ASP-09
https://VOTRE_PSEUDO.github.io/jf2026/?p=ASP-10
https://VOTRE_PSEUDO.github.io/jf2026/?p=ASP-11
https://VOTRE_PSEUDO.github.io/jf2026/?p=ASP-12
https://VOTRE_PSEUDO.github.io/jf2026/?p=ASP-13
https://VOTRE_PSEUDO.github.io/jf2026/?p=ASP-14
https://VOTRE_PSEUDO.github.io/jf2026/?p=ASP-15
```

**Atelier Broyeurs Café (15 QR codes) :**
```
https://VOTRE_PSEUDO.github.io/jf2026/?p=CAF-01
https://VOTRE_PSEUDO.github.io/jf2026/?p=CAF-02
...jusqu'à...
https://VOTRE_PSEUDO.github.io/jf2026/?p=CAF-15
```

**Classement (1 QR code — à projeter ou afficher) :**
```
https://VOTRE_PSEUDO.github.io/jf2026/leaderboard.html
```

### Générer les QR codes rapidement

Outil recommandé : **[qr-code-generator.com](https://qr-code-generator.com)**

1. Coller l'URL → Générer → Télécharger en PNG (taille min. 400×400 px)
2. Répéter pour chacune des 30 URLs + la page classement

> 💡 Astuce : dans Microsoft Edge, ouvrez chaque URL et faites  
> **clic droit → "Créer un QR code pour cette page"** — c'est le plus rapide !

---

## ÉTAPE 5 — Personnaliser les noms d'équipes (optionnel)

Par défaut les équipes s'appellent "Équipe 1" à "Équipe 10".

**Option A — Les équipes choisissent leur nom elles-mêmes**
Dans `index.html`, remplacez la ligne :
```js
const TEAMS = Array.from({length: 10}, (_, i) => ({
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
Faites la même modification dans `leaderboard.html`.

---

## Récapitulatif — Le jour J

| Action | Où |
|--------|-----|
| Classement en direct | `leaderboard.html` — à projeter sur écran |
| Les équipes scannent | QR codes sur les fiches produit |
| Réinitialiser les scores | `leaderboard.html` → bouton **Admin** → PIN `2026` → Remettre à zéro |
| Changer d'équipe | Page d'accueil → bouton avec le nom d'équipe |

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
