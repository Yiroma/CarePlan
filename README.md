# 🏥 Care Plan - Gestion Médicale Intelligente

## 📋 À propos du projet

**Care Plan** est une application web moderne conçue pour optimiser la gestion des rendez-vous et des utilisateurs dans un environnement hospitalier. Développée pour répondre aux besoins spécifiques des établissements de santé, cette solution permet une coordination fluide entre les agents d'accueil, secrétaires, professionnels de santé et administrateurs grâce à des fonctionnalités clés :

- 👨‍⚕️ Gestion des plannings médicaux
- 📅 Prise de rendez-vous intelligente
- 🔐 Contrôle granulaire des accès utilisateurs
- 📤 Notifications automatisées par email
- 🗂 Archivage sécurisé des dossiers patients

---

## 🔥 Objectif pédagogique

Ce projet est réalisé dans le cadre de la formation **CDA - Concepteur Développeur d'Applications** par une équipe de 5 étudiants.

---

## 👥 Rôles & Permissions

| Rôle                          | Droits & Accès                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| ----------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 🟢 **Agent**                  | - Accès mobile uniquement<br>- Recherche patient (nom / n° sécu)<br>- Affichage du lieu et horaire du rendez-vous                                                                                                                                                                                                                                                                                                                                      |
| 🟡 **Secrétaire**             | - Gestion complète des rendez-vous (créer, modifier, supprimer)<br>- Accès à l'emploi du temps de tous les professionnels de santé<br>- Consultation des absences et congés du personnel médical<br>- Aucun accès aux dossiers médicaux<br>- Ne peut pas poser de congés ou indiquer une absence                                                                                                                                                       |
| 🔵 **Professionnel de santé** | - Consultation et historique de ses rendez-vous<br>- Consultation de ses anciennes consultations<br>- Accès à tous les dossiers médicaux<br>- Rédaction obligatoire d'un compte rendu par consultation<br>- Ne peut pas modifier ni supprimer un compte rendu<br>- Peut rédiger un compte rendu correctif<br>- Peut consulter son propre planning<br>- Peut faire une demande de congé ou d'absence<br>- Ne peut pas voir le planning de ses collègues |
| 🔴 **Admin**                  | - Création, modification, suppression d'utilisateurs<br>- Modification des rôles utilisateurs<br>- Accès au planning de tout le personnel (agents, secrétaires, professionnels de santé, admins)<br>- Peut modifier le planning de tout le personnel<br>- Aucun accès aux dossiers médicaux ni aux rendez-vous des patients                                                                                                                            |

## 🔐 Modèle de permissions

| Rôle       | Dossiers patients     | RDV | Congés / Absences                 | Planning              | Comptes utilisateurs |
| ---------- | --------------------- | --- | --------------------------------- | --------------------- | -------------------- |
| Agent      | ❌                    | ✅  | ❌                                | ❌                    | ❌                   |
| Secrétaire | ❌                    | ✅  | Lecture seule congés/absences pro | Lecture planning pro  | ❌                   |
| Médecin    | ✅ Lecture / Ajout CR | ✅  | ✅ (sur soi-même)                 | ✅ (perso uniquement) | ❌                   |
| Admin      | ❌                    | ❌  | ✅ (tout personnel)               | ✅ (tout personnel)   | ✅ (CRUD + rôles)    |

---

## 🧱 Architecture technique

L'application repose sur une architecture **microservices** combinant **GraphQL** (pour le service principal) et **REST** (pour les services auth, email et upload). Un **reverse proxy Nginx** centralise les accès sur un point d'entrée unique.

---

## 🚀 Technologies utilisées

### Frontend

- ⚛️ **React 18** - Interfaces dynamiques
- 🔷 **TypeScript 5** - Typage statique robuste
- ⚡ **Vite 5** - Build tool rapide
- 🎨 **TailwindCSS 4** - Framework CSS utilitaire
- 🧩 **Shadcn UI** - Composants UI accessibles (Radix UI)
- 🔄 **Apollo Client 3** - Client GraphQL
- 🗺️ **React Router 7** - Routage
- 📋 **React Hook Form** - Gestion des formulaires
- 📅 **react-big-calendar** - Calendrier interactif
- 🕐 **date-fns** - Manipulation des dates
- 🔔 **react-toastify** - Notifications
- 🔍 **Lucide React** - Icônes
- 📏 **Joi** - Validation côté client
- 📏 **casl** - Gestion des permissions
- 🧹 **ESLint 8** - Linter de code
- 🔷 **Prettier** - Formatage de code
- 🔍 **Husky** - Pre-commit hooks
- 🧪 **Vitest** - Tests unitaires & intégration
- 🎭 **Playwright** - Tests E2E

### Backend

- 🟢 **Node.js 22** - Runtime JavaScript
- 🔷 **TypeScript 5** - Typage statique
- 🚀 **Apollo Server 4** - Serveur GraphQL
- 🌐 **Express 4/5** - Framework HTTP REST
- 🗃️ **TypeORM** - ORM TypeScript
- 🗄️ **PostgreSQL 17** - Base de données relationnelle
- 🔴 **Redis** - Cache performant
- 📧 **Nodemailer 7** - Emails transactionnels
- 📄 **Handlebars** - Templates d'emails
- 📁 **Multer 2** - Upload de fichiers
- 🔐 **JWT** - Authentification sécurisée
- 🔑 **Argon2** - Hashing des mots de passe
- ✅ **Joi / class-validator** - Validation des données
- 📊 **Winston** - Logging
- 🔍 **Nginx** - Reverse proxy / gateway
- 🐳 **Docker** - Conteneurisation
- ⚙️ **Makefile** - Orchestration des commandes

---

## 📁 Structure du dépôt

```
care-plan/
│
├── .github/
│   └── workflows/            # Pipelines CI/CD GitHub Actions
│       ├── integration-test.yml
│       └── statics.yml
├── .husky/                   # Git hooks (pre-commit)
├── backend/
│   ├── appointment-service/  # GraphQL — rendez-vous, patients, consultations
│   ├── auth-service/         # REST — authentification JWT
│   ├── email-service/        # REST — envoi d'emails transactionnels
│   └── upload-service/       # REST — upload de fichiers
├── docs/                     # Documentation projet
├── files/
│   ├── .env-dev-default      # Variables d'environnement (référence)
│   ├── datatest/             # Données SQL pour les tests
│   ├── nginx.conf            # Configuration du reverse proxy
│   └── webhook.sample.yml
├── frontend/                 # Application React (Vite)
├── docker-compose.dev.yml    # Orchestration développement
├── docker-compose.predeploy.yml
├── docker-compose.test.yml   # Orchestration tests d'intégration
├── Makefile                  # Commandes raccourcies Docker
├── .eslintrc.js              # Configuration ESLint centralisée
├── .prettierrc               # Configuration Prettier
├── lint-staged.config.js     # Hooks pre-commit lint-staged
└── README.md
```

---

## 🧩 Microservices & Ports

| Service             | Description                                    | Port interne | Route Nginx             |
| ------------------- | ---------------------------------------------- | ------------ | ----------------------- |
| **Frontend**        | Application React (Vite)                       | 5173         | `/`                     |
| **Appointment**     | GraphQL — RDV, patients, consultations, congés | 4000         | `/graphql`              |
| **Auth Service**    | REST — Authentification, JWT, rôles            | 9500         | `/auth`                 |
| **Email Service**   | REST — Emails transactionnels (interne)        | 9501         | _(non exposé)_          |
| **Upload Service**  | REST — Upload de fichiers                      | 5000         | `/upload/`              |
| **PostgreSQL**      | Base de données                                | 5432         | _(interne)_             |
| **Redis**           | Cache                                          | 6379         | _(interne)_             |
| **Adminer**         | Interface de gestion BDD                       | 8080         | _(direct)_              |
| **Gateway (Nginx)** | Reverse proxy — point d'entrée unique          | **7700**     | `http://localhost:7700` |

---

## 🛠️ Installation

### Prérequis

- [Docker](https://www.docker.com/) & Docker Compose
- [Node.js](https://nodejs.org/) (pour les outils de qualité de code)
- `make` (pour utiliser le Makefile)

### 1. Cloner le dépôt

```bash
git clone https://github.com/WildCodeSchool-CDA-FT-2025-03/CDA-Projet-2-Team-1.git
cd care-plan
```

### 2. Configurer les variables d'environnement

```bash
cp files/.env-dev-default files/.env
# Adapter les valeurs si nécessaire
```

### 3. Installer les dépendances racine (qualité de code)

```bash
npm install
```

### 4. Lancer tous les services avec Docker

```bash
# Via Makefile (recommandé)
make run       # Build + démarrage en avant-plan
make run-bg    # Build + démarrage en arrière-plan

# Ou via Docker Compose directement
docker compose -f docker-compose.dev.yml --env-file files/.env-dev-default up --build
```

### 5. Accéder à l'application

| Accès                  | URL                           |
| ---------------------- | ----------------------------- |
| Application (frontend) | http://localhost:7700         |
| API GraphQL            | http://localhost:7700/graphql |
| Auth REST API          | http://localhost:7700/auth    |
| Upload REST API        | http://localhost:7700/upload/ |
| Adminer (gestion BDD)  | http://localhost:8080         |

---

## 🧪 Tests

### Lancer les tests d'intégration (via Docker)

```bash
make test                       # Tous les tests d'intégration
make test-integration           # Tests appointment-service
make test-email-integration     # Tests email-service
```

### Lancer les tests frontend (hors Docker)

```bash
cd frontend

npm run test                    # Tous les tests
npm run test:unit               # Tests unitaires (Vitest)
npm run test:integration        # Tests d'intégration (Vitest)
npm run test:e2e                # Tests E2E (Playwright)
npm run test:unit:coverage      # Coverage unitaire
npm run test:e2e:report         # Rapport Playwright
```

---

## 🧹 Bonnes pratiques

### Convention de commits

- `feat:` Nouvelle fonctionnalité
- `fix:` Correction de bug
- `docs:` Documentation
- `refactor:` Refacto sans changement fonctionnel
- `style:` Changement visuel / CSS uniquement

### Workflow de développement

```bash
npm run lint          # Analyse statique du code (ESLint)
npm run format        # Vérification du formatage (Prettier)
npm run format:fix    # Correction automatique du formatage
npm run lint:fix      # Correction automatique ESLint
```

> Les hooks Husky + lint-staged s'exécutent automatiquement à chaque `git commit`.

### Commandes Makefile utiles

```bash
make run              # Build + démarrage
make run-bg           # Build + démarrage (arrière-plan)
make down             # Arrêt des services
make clean            # Arrêt + suppression containers + images
make prune            # clean + suppression volumes
make deploy           # Redéploiement complet
```

---

## ⚙️ CI/CD

| Pipeline               | Déclencheur         | Actions                            |
| ---------------------- | ------------------- | ---------------------------------- |
| `statics.yml`          | PR vers `dev`       | Install deps, ESLint, Prettier     |
| `integration-test.yml` | PR vers `predeploy` | Build Docker + tests d'intégration |

---

## 📆 Roadmap

- [x] Définition des rôles utilisateurs
- [x] Choix technologiques
- [x] Authentification JWT sécurisée
- [x] Service d'emails transactionnels
- [x] Service d'upload de fichiers
- [x] API GraphQL (appointment-service)
- [x] Interface agent mobile
- [x] Intégration des tests (unitaires + intégration + E2E)
- [ ] Dashboard professionnel complet
- [ ] Panel de gestion administrateur complet
- [ ] Déploiement (Docker / VPS / NAS)

---

## 👨‍💻 Équipe projet

| Nom        | GitHub                                                         |
| ---------- | -------------------------------------------------------------- |
| Florian    | [@eustasio](https://github.com/eustasio)                       |
| Maximilien | [@Maxwellmilien](https://github.com/Maxwellmilien)             |
| Rodolphe   | [@li-rodolphetournier](https://github.com/li-rodolphetournier) |
| Romaric    | [@Yiroma](https://github.com/Yiroma)                           |
| Ryan       | [@ryandecian](https://github.com/ryandecian)                   |

---

## 📜 Licence

Projet développé dans un cadre pédagogique — toute utilisation externe doit être autorisée par l'équipe.
