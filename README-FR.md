# stage-rtbf-entreprise

> **⚠️ Ce dépôt ne contient pas le code source original pour des raisons de confidentialité.**  
> Il documente l’architecture, les technologies et mes contributions au projet réalisé lors de mon stage de 6 mois à la RTBF.

## 📝 Contexte du projet
Dans le cadre de mon stage à la RTBF, j’ai contribué à la mise en ligne de la nouvelle version du site Entreprise (« RTBF et vous »), destinée à remplacer une version devenue obsolète.
L’objectif était double :
- **Moderniser** l’interface pour l’aligner sur l’identité actuelle de la RTBF.
- **Unifier** les technologies avec celles du site principal (RTBF Actus) en utilisant les mêmes outils et standards.
Le site **RTBF et vous** est une plateforme qui va au-delà des simples programmes. C’est un portail conçu pour créer un lien direct et transparent entre le groupe audiovisuel et ses différents publics.

Il est structuré en plusieurs sections :

- **Public** : découverte des coulisses, visites des studios, participation à des émissions, médiation pour questions et réclamations.
- **Éducation** : espace pour enseignants et élèves, consultation des archives, accueil d’intervenants dans les classes, offres de stages.
- **Pros** : informations pour les entreprises et professionnels, partenariats, sponsoring, actualités, espace presse pour les journalistes.
- **Qui sommes-nous ?** : présentation des engagements, de l’histoire, des lieux, de la gouvernance et des publications de la RTBF.
Des pages spécifiques dédiées à l’emploi et aux contacts complètent ce dispositif, faisant de ce site une vitrine du rôle sociétal, éducatif et professionnel de la RTBF, en plus de sa mission de service public.

## 🛠️ Technologies & Architecture

### Frontend
- **Framework** : [Next.js 15](https://nextjs.org/) + [TypeScript](https://www.typescriptlang.org/)
- **UI** : TailwindCSS v4 + composants React réutilisables
- **API client** : Orval (génération automatique de clients à partir d’OpenAPI)
- **Monorepo** : [NX](https://nx.dev/) (apps `one-site`, `entreprise`, librairies partagées `libs/ui`, `libs/api`…)

### Backend / API
- **Framework** : Laravel 11
- **Qualité & tests** : PestPHP, Laravel Pint
- **OpenAPI / Postman** : génération et mise à jour automatique de la documentation
- **Monitoring** : Prometheus Client PHP
- **Base de données** : MySQL/MariaDB
- **Infrastructure** : Kubernetes (Lens)

# Architecture du projet
Ce document décrit l’architecture globale du projet OAOS (Frontend) développé à la RTBF.
[![](https://mermaid.ink/img/pako:eNqFVdty2jAQ_RWNnpIpGLAxFz90JoG-ddI25KkhD8JeHAUjeSQ5hWbyQfmO_lhXvnAxhvgFJJ9zdrVnV36joYyABjRWLH0mD9O5IPjcPM4pS9OEh8xwKXRnTp9Iu_2V3BYv8o0Smu9PcD_hi5P9Ke6nLFyxGJwXLQW50qHiqdHkbtO5g41pETChc12jfUOa0aEUSx47C6YrMks4LjR5mBWMgqOzRZG-zazYss9tkXEPtaSAtuYG9ukdAFwEgDAKUsV1M8Q70GiDCx1yNdmmCrS-boL3jxTPEUBEJyeoghxI9spjsKL0qHSTpuReZgZULXoFXdiqZwu0r9MMCHNbYtCo9tP-XtaLEF76dkYQLMJsk1zxgfHkDxcRee2fEVwiXKD7Tmnxi27GxTZPJV8gNGUHTPgiAWyey2U8cBxLNqeH0qyqp22MhG3x4I7RG3L1Pf9PFAu5ADKb3deT3zFtx4QJR4vbDQLFm8sJ7rvjIIBb9mPl9HH46q01N5TrFE8oTvyoQOHej2ZAdK5FKoB1NDM8OSfwmYUVrm7hJ74dDGLdOZdV9Tl2rhZ3h2p06RzYTriQpr2UmYguAe1sM2V4mNSvij3GR8zjo-M4Osli_fR0Auzv1Fg5iU0h_Z1eI6qpgPYO3mtMirvZlivjOJhT0DwWZLbVBtbkC5kZqbYLKVfHnV7S3LwNLW-SV1GTH-qVJci7BxYa8isDtW1kenmLKshvF2VY_O9DB6S8QVokb6tGoi1uxAxDv0DZmwSHccVFfDRMtIVfKx7RwKgMWnQNas3skr5ZCH44nmENcxoQq6VWtofekZMy8VvKdUVTMoufabBkicZVlmJYmHKGZdxDMBioCXaEoUHP87u5CA3e6IYGbc_zne5gPB66va476A1HLbqlgTscOP1h3_dHuOmP-v57i_7Nw_acwcjzB-PhaDT23FG3673_B7YnI5c?type=png)](https://mermaid.live/edit#pako:eNqFVdty2jAQ_RWNnpIpGLAxFz90JoG-ddI25KkhD8JeHAUjeSQ5hWbyQfmO_lhXvnAxhvgFJJ9zdrVnV36joYyABjRWLH0mD9O5IPjcPM4pS9OEh8xwKXRnTp9Iu_2V3BYv8o0Smu9PcD_hi5P9Ke6nLFyxGJwXLQW50qHiqdHkbtO5g41pETChc12jfUOa0aEUSx47C6YrMks4LjR5mBWMgqOzRZG-zazYss9tkXEPtaSAtuYG9ukdAFwEgDAKUsV1M8Q70GiDCx1yNdmmCrS-boL3jxTPEUBEJyeoghxI9spjsKL0qHSTpuReZgZULXoFXdiqZwu0r9MMCHNbYtCo9tP-XtaLEF76dkYQLMJsk1zxgfHkDxcRee2fEVwiXKD7Tmnxi27GxTZPJV8gNGUHTPgiAWyey2U8cBxLNqeH0qyqp22MhG3x4I7RG3L1Pf9PFAu5ADKb3deT3zFtx4QJR4vbDQLFm8sJ7rvjIIBb9mPl9HH46q01N5TrFE8oTvyoQOHej2ZAdK5FKoB1NDM8OSfwmYUVrm7hJ74dDGLdOZdV9Tl2rhZ3h2p06RzYTriQpr2UmYguAe1sM2V4mNSvij3GR8zjo-M4Osli_fR0Auzv1Fg5iU0h_Z1eI6qpgPYO3mtMirvZlivjOJhT0DwWZLbVBtbkC5kZqbYLKVfHnV7S3LwNLW-SV1GTH-qVJci7BxYa8isDtW1kenmLKshvF2VY_O9DB6S8QVokb6tGoi1uxAxDv0DZmwSHccVFfDRMtIVfKx7RwKgMWnQNas3skr5ZCH44nmENcxoQq6VWtofekZMy8VvKdUVTMoufabBkicZVlmJYmHKGZdxDMBioCXaEoUHP87u5CA3e6IYGbc_zne5gPB66va476A1HLbqlgTscOP1h3_dHuOmP-v57i_7Nw_acwcjzB-PhaDT23FG3673_B7YnI5c)

### Structure du monorepo (frontend)
```text
applications/
├─ apps/
│  ├─ one-site/
│  │  ├─ app/                     # App Router (routage Next 15)
│  │  │  ├─ layout.tsx            # Layout racine SSR: injecte <ClientLayout>…</ClientLayout>
│  │  │  └─ client-layout.tsx     # Layout client: auth, consent, tracking, providers
│  │  ├─ public/                  # assets publics
│  │  ├─ pages/                   # Pages Router
│  │  ├─ scripts/                 # scripts client spécifiques one-site
│  │  ├─ styles/                  # Tailwind v4, polices
│  │  ├─ next.config.js
│  │  └─ project.json             # cible Nx (build, dev, etc.)
│  ├─ entreprise/
|  |  ├─ app/
│  |  |  ├─ layout.tsx
│  |  |  ├─ client-layout.tsx
│  |  |  ├─ not-found.tsx
│  |  |  ├─ article/
│  |  |  │  └─ page.tsx
│  |  |  └─ [[...slugs]]/
│  |  |     └─ page.tsx
|  |  ├─ components/
│  │  ├─ styles/
|  |  ├─ public/
|  |  ├─ utils/
|  |  ├─ next.config.js
|  |  └─ project.json
│  ├─ one-site-e2e/               # tests E2E (Cypress)
│  └─ entreprise-e2e/
├─ libs/
│  ├─ ui/                         # Design System + Storybook
│  ├─ api/                        # Clients Orval + hooks React Query + types
│  ├─ core/                       # Partagés (scripts, utils)
│  └─ datalayer/                  # Tracking (schemas, helpers)
├─ package.json                   # scripts Nx/Next/storybook, orval, etc.
└─ tsconfig.base.json             # aliases TypeScript du monorepo
```

## 🚀 Mon rôle et contributions
- Développement de **composants UI réutilisables** (React/Next.js + Tailwind CSS + intégration API Orval).
- **Optimisation des performances front-end** (lazy loading, réduction bundle, cache, réduction de la charge JS).
- Gestion des **métadonnées dans le backend Laravel**, avec utilisation de Postman pour la configuration et les tests sur différents environnements (local, UAT, production).
- Intégration de **trackers de fréquentation** (Gemius / CIM Internet).
- **Collaboration** avec les équipes backend, frontend et UX designers.
- Participation aux **pipelines CI/CD (GitLab)** pour automatiser les tests et les déploiements.
- **Agile (Scrum)** : participation aux daily meetings, revues de code et planifications.

## 📂 Ce dépôt
Ce repository **ne contient pas le code source**, mais :
- La **documentation technique** (README, schémas d’architecture…).
- Les **principales décisions techniques** et la stack utilisée.
- Des **captures d’écran** ou **diagrammes** d’architecture (voir dossier `/images`).
- Un **rétro-planning** ou un journal de bord de mes contributions.

## 🔗 Ressources
- [Next.js](https://nextjs.org/)
- [NX Monorepo](https://nx.dev/)
- [Laravel](https://laravel.com/)
- [TailwindCSS](https://tailwindcss.com/)
- [Orval](https://orval.dev/)

> _Auteur : Lucas Maroy — Stage RTBF 2025_
