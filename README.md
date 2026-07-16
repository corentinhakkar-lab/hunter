# SYSTÈME — Entraînement

Suivi d'entraînement gamifié (thème Solo Leveling), en **une seule page HTML**, sans build, sans dépendance, sans serveur.

- **XP / niveaux / rangs** (E → S) calculés sur les raids archivés
- **Séances libres** salle + bureau, entièrement éditables
- **Périodisation 12 semaines** (calibrage → accumulation → deload → intensification → pic), deload automatique
- **Minuteur de repos** avec alarme bloquante, écran maintenu allumé pendant un raid
- **Records par exercice** (1RM estimé, formule d'Epley) et **suivi du poids de corps**
- Exercices au poids de corps gérés proprement (la charge saisie = lest ajouté)

## Données

Tout est stocké **localement dans le navigateur** (`localStorage`, clé `sl_training_v1`). Rien n'est envoyé nulle part, il n'y a pas de compte.

- **Sauvegarde / transfert** : onglet *Système* → `Exporter (JSON)` / `Importer (JSON)`.
- Une sauvegarde de départ est **embarquée dans `index.html`** : elle n'est chargée que si le navigateur n'a encore aucune donnée. Elle n'écrase jamais des données existantes.

> ⚠️ Si le dépôt est **public**, cette sauvegarde embarquée (séances + historique) est visible dans le code source. Pour l'enlever, voir « Retirer les données embarquées » plus bas.

## Publier sur GitHub Pages

1. Créer un dépôt et y déposer **le contenu de ce dossier à la racine** (`index.html`, `manifest.webmanifest`, les `.png`, `.nojekyll`).
2. Dans le dépôt : **Settings → Pages**.
3. *Source* : **Deploy from a branch** — branche `main`, dossier `/ (root)`. Enregistrer.
4. Attendre ~1 minute : le site est sur `https://<utilisateur>.github.io/<dépôt>/`.

## Installer sur iPhone

1. Ouvrir l'URL GitHub Pages dans **Safari** (obligatoire, pas Chrome).
2. Bouton **Partager** → **Sur l'écran d'accueil**.
3. L'icône apparaît ; l'app s'ouvre en plein écran, sans barre d'adresse.

Sur Android : Chrome → menu → *Installer l'application*.

### À savoir sur le minuteur

Le décompte est calé sur l'horloge réelle : il reste juste même après un verrouillage. En revanche, **iOS gèle les pages web en arrière-plan** : si l'iPhone est verrouillé ou que tu passes sur une autre app, le bip et la pop-up ne se déclenchent pas à cet instant — ils se déclenchent **à ton retour** dans l'app. Pendant un raid, l'écran est maintenu allumé automatiquement (Wake Lock) : si tu laisses l'app ouverte, l'alarme fonctionne normalement.

## Fichiers

| Fichier | Rôle |
|---|---|
| `index.html` | L'application entière (HTML + CSS + JS + données de départ) |
| `manifest.webmanifest` | Métadonnées PWA (nom, couleurs, icônes, mode plein écran) |
| `icon-180.png` | Icône du raccourci iPhone (`apple-touch-icon`) |
| `icon-192.png` / `icon-512.png` | Icônes PWA (Android / Chrome) |
| `icon-512-maskable.png` | Icône *maskable* Android (avec zone de sécurité) |
| `favicon-32.png` | Icône d'onglet |
| `.nojekyll` | Désactive Jekyll sur GitHub Pages (sert les fichiers tels quels) |

## Retirer les données embarquées

Dans `index.html`, chercher `const SEED=` et remplacer toute la valeur par `null` :

```js
const SEED=null;
```

L'app démarrera alors sur les séances par défaut ; la sauvegarde s'importe ensuite via *Système → Importer (JSON)*.

## Personnaliser

Aucune compilation : ouvrir `index.html` dans un éditeur.

- **Couleurs** : variables CSS en haut (`:root { --acc, --bg, ... }`).
- **Niveaux / récompenses** : tableau `LEVELS` (ou *Progression → Éditer les récompenses* dans l'app).
- **Zones musculaires** : tableau `ZONES`. **XP** : `XP_SET` / `XP_FULL`.
- **Exercices au poids de corps** : détectés par mots-clés (`BW_WORDS`), et réglables par exercice via la case à cocher dans l'éditeur ✎.
