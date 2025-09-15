# stage-rtbf-entreprise

> **⚠️ Ce dépôt ne contient pas le code source original pour des raisons de confidentialité.**  
> Il documente l’architecture, les technologies et mes contributions au projet réalisé lors de mon stage de 6 mois à la RTBF.

---

## 📝 Contexte du projet
Plateforme web destinée à diffuser des contenus et services numériques de la RTBF.  
Objectif : offrir une expérience unifiée, rapide et responsive sur plusieurs “apps” (grand public et entreprise).

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

### Structure simplifiée du monorepo (frontend)

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
- Développement de composants UI réutilisables (React/Next.js + Tailwind CSS).
- Intégration et typage automatique d’APIs REST/GraphQL via Orval.
- Optimisation des performances front-end (lazy loading, réduction bundle, cache).
- Gestion des métadonnées dans le backend Laravel.
- Intégration de trackers de fréquentation (Gemius / CIM Internet).
- Collaboration avec les équipes backend, frontend et UX designers.
- Participation aux revues de code, CI/CD et déploiements Kubernetes.

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
