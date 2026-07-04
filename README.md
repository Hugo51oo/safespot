# SafeSpot 🛡️

> La sécurité, à portée de main.

SafeSpot est un compagnon de sécurité ancré localement, pensé pour réduire les restrictions de mobilité que vivent les femmes dans l'espace public. L'application affiche un réseau de **points sûrs vérifiés**, calcule l'**itinéraire à pied** vers le plus proche, et propose une **alerte SOS** vers des contacts de confiance.

Projet étudiant — Université de Reims Champagne-Ardenne (URCA).

---

## ✨ Fonctionnalités

- 🗺️ **Carte interactive** des points sûrs (commerces refuges, pharmacies, lieux publics, campus, gares)
- 📍 **Point sûr le plus proche** avec itinéraire à pied et durée estimée
- 🔴 **Bouton SOS** : compte à rebours, partage de position, appel d'un contact ou du 112
- 👤 **Contacts de confiance** (stockés sur l'appareil)
- 🟢 **Mode « Rentrer en sécurité »** : suivi de position en direct
- 🔍 **Recherche d'adresse**
- ➕ **Proposition de points** par les utilisateurs, soumise à **modération**
- 🛠️ **Mode admin** intégré pour valider / supprimer les points
- 📱 **Installable (PWA)** : icône sur l'écran d'accueil, lancement plein écran, fonctionnement hors-ligne

---

## 🛠️ Stack technique

| Brique | Technologie |
|---|---|
| Carte & fonds de plan | [Leaflet](https://leafletjs.com) + OpenStreetMap |
| Itinéraire à pied | OSRM (serveur public) |
| Recherche d'adresse | Nominatim |
| Base de données & auth | [Supabase](https://supabase.com) |
| Application | HTML / CSS / JavaScript (un seul fichier) + PWA |

Aucune compilation, aucune dépendance à installer : tout tient dans un fichier statique.

---

## 📁 Structure du dépôt

```
safespot/
├── index.html            ← l'application (renommer SafeSpot_App.html en index.html)
├── manifest.webmanifest  ← configuration PWA
├── sw.js                 ← service worker (hors-ligne)
├── icon-192.png          ← icône
└── icon-512.png          ← icône
```

---

## 🚀 Lancer le projet

**En local** : ouvrir `index.html` dans un navigateur (idéalement sur mobile, autoriser la localisation).
> ⚠️ L'installation PWA et le service worker ne fonctionnent **pas** en `file://` — il faut héberger l'app (voir ci-dessous).

**En ligne (gratuit)** :
- **Netlify** : glisser le dossier sur [app.netlify.com/drop](https://app.netlify.com/drop) → URL `https` instantanée.
- **GitHub Pages** : *Settings → Pages → Deploy from branch* → l'app est servie sur `https://<pseudo>.github.io/safespot/`.

---

## ☁️ Configuration Supabase

L'app fonctionne en **mode local** tant qu'aucune clé n'est renseignée. Pour activer le cloud (points partagés) :

1. Créer un projet gratuit sur [supabase.com](https://supabase.com).
2. Créer la table et les règles de sécurité (script SQL fourni dans le projet).
3. Renseigner les clés en haut de `index.html` :

```js
var SUPABASE_URL="https://xxxx.supabase.co";
var SUPABASE_ANON_KEY="eyJhbGci...";
```

> La clé **anon public** est conçue pour vivre côté navigateur — c'est sans danger. Ce sont les règles **RLS** (Row Level Security) qui protègent la base, pas le secret de la clé.

---

## 🔒 Sécurité & modération

- **RLS** activée : lecture des points approuvés uniquement, écriture encadrée.
- **Validation serveur** des entrées (formats, longueurs, bornes).
- **Modération** : les points proposés ne sont publiés qu'après validation.
- **Mode admin** réservé à un compte unique (auth Supabase).

---

## ⚠️ Avertissement

SafeSpot est un **prototype étudiant**. Il ne remplace pas les services de secours.
**En cas de danger immédiat, appelez le 17 (police) ou le 112 (urgences).**

---

## 📄 Licence

Projet étudiant, à usage pédagogique. Définir une licence (ex. MIT) avant toute diffusion publique.
