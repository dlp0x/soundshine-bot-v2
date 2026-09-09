# soundSHINE Bot

Bot Discord officiel de **soundSHINE Radio**.  
Il diffuse le stream radio dans un Stage Channel, gère les demandes de morceaux et expose une API légère pour le monitoring et la synchronisation avec RadioDJ.

🌐 [soundshineradio.com](https://soundshineradio.com)

---

## Fonctionnalités

- Diffusion du stream radio dans un **Stage Channel** Discord
- Système de **requests** (demande, édition, liste, suppression)
- Commandes de gestion de la station (`/station`)
- API HTTP sécurisée (santé, mise à jour playlist…)
- Architecture modulaire et testée (Vitest)
- Intégration avec **RadioDJ**

---

## Structure du projet

```text
.
├── src/
│   ├── api/          # Serveur Express + routes HTTP
│   ├── bot/          # Client Discord, commandes, events, services, tasks
│   ├── core/         # Logique métier et cycle de vie
│   ├── config/       # Configurations (ESLint, Vitest…)
│   ├── data/         # Accès données
│   ├── shared/       # Utilitaires partagés
│   └── tests/        # Tests Vitest
├── scripts/          # Scripts de développement et déploiement
├── docs/             # Documentation additionnelle
└── package.json
```

Point d’entrée : `src/index.js`

---

## Prérequis

- Node.js 18+
- npm
- Un bot Discord configuré avec les permissions nécessaires
- Accès à RadioDJ (API)

---

## Configuration

Le bot charge les variables d’environnement dans cet ordre :
1. `.env`
2. `.env.<env>` (ex: `.env.dev`, `.env.prod`)

### Variables obligatoires

```env
DISCORD_TOKEN=
ADMIN_ROLE_ID=
VOICE_CHANNEL_ID=
PLAYLIST_CHANNEL_ID=
REQ_ROLE_ID=
STREAM_URL=
JSON_URL=
API_PORT=3000
API_TOKEN=
```

### Variables optionnelles / utiles

```env
CLIENT_ID=
GUILD_ID=
DEV_GUILD_ID=
BOT_ROLE_NAME=soundSHINE
LOG_LEVEL=info
UNSPLASH_ACCESS_KEY=
RADIODJ_API_URL=
RADIODJ_API_KEY=
```

---

## Installation & démarrage

```bash
# Installation des dépendances
npm install

# Mode développement
npm run dev

# Mode production
npm run prod
```

---

## Scripts utiles

| Commande              | Description                          |
|-----------------------|--------------------------------------|
| `npm run deploy:dev`  | Déploie les commandes (guild de dev) |
| `npm run deploy:global` | Déploie les commandes globalement  |
| `npm run clear:dev`   | Supprime les commandes de dev        |
| `npm run clear:global`| Supprime les commandes globales      |
| `npm run db:deploy`   | Déploie / met à jour la base         |
| `npm run lint`        | Vérifie le code                      |
| `npm run lint:fix`   | Corrige automatiquement le code      |
| `npm test`            | Lance les tests Vitest               |
| `npm run context:md`  | Génère le contexte Markdown          |

---

## Commandes Discord

### Utilisateurs

| Commande              | Description                          |
|-----------------------|--------------------------------------|
| `/help`               | Affiche l’aide                       |
| `/ping`               | Vérifie la latence du bot            |
| `/radio nowplaying`   | Affiche le morceau en cours          |
| `/station schedule`   | Affiche le planning                  |
| `/request ask`        | Demander un morceau                  |
| `/request edit`       | Modifier une demande                 |
| `/drink`              | Commande fun                         |
| `/getwallpaper`       | Récupère un wallpaper                |

### Admin / Modération radio

| Commande                    | Description                              |
|-----------------------------|------------------------------------------|
| `/request delete`           | Supprimer une demande                    |
| `/request list`             | Lister les demandes                      |
| `/station stats`            | Statistiques de la station               |
| `/station stream-config`    | Configuration du stream                  |

---

## API HTTP

Base URL par défaut : `http://localhost:3000`

| Méthode | Endpoint                 | Description                     |
|---------|--------------------------|---------------------------------|
| `GET`   | `/`                      | Racine                          |
| `GET`   | `/v1/health`             | Santé du bot                    |
| `POST`  | `/v1/playlist-update`    | Mise à jour de la playlist      |

Exemple :

```bash
curl http://localhost:3000/v1/health
```

L’API est protégée par le token défini dans `API_TOKEN`.

---

## Roadmap

- [ ] Dashboard web léger de monitoring (statut, now playing, logs, stats simples)
- [ ] Commande `/request top10` (morceaux les plus demandés)
- [ ] Amélioration de l’historique des morceaux
- [ ] Documentation API plus complète

---

## Licence

Projet privé / usage interne soundSHINE Radio.

---

## Liens

- Site : [soundshineradio.com](https://soundshineradio.com)
- Repo : [github.com/dlp0x/soundshine-bot](https://github.com/dlp0x/soundshine-bot)
