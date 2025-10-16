# stage-rtbf-entreprise

> **⚠️ This repository does not contain the original source code for confidentiality reasons.**
> It documents the architecture, technologies, and my contributions to the project carried out during my 6-month internship at RTBF.

## 🌐 Live Website

👉 [Visit the website](https://www.rtbf.be/et-vous)

## 📝 Project Context

As part of my **paid internship at RTBF**, I contributed to the launch of the new version of the **Entreprise** website (“RTBF et vous”), replacing an outdated version.
The goal was twofold:

* **Modernize** the interface to align it with RTBF’s current brand identity.
* **Unify** the technologies with those used by the main RTBF news site (RTBF Actus) by leveraging the same tools and standards.

The **RTBF et vous** website is a platform that goes beyond standard programming. It is designed to create a direct and transparent link between the public broadcaster and its various audiences.

It is structured into several sections:

* **Public**: discover behind the scenes, visit studios, participate in shows, and contact the mediation service for questions or complaints.
* **Education**: a dedicated area for teachers and students, including archives consultation, bringing RTBF professionals into classrooms, and internship opportunities.
* **Pros**: information for businesses and professionals, partnerships, sponsorships, news, and a press area for journalists.
* **Who we are?**: presentation of RTBF’s commitments, history, locations, governance, and key publications.

Additional pages dedicated to **jobs** and **contact** complete the site, making it a showcase of RTBF’s societal, educational, and professional roles, alongside its public service mission.

## 🛠️ Technologies & Architecture

### Frontend

* **Framework**: [Next.js 15](https://nextjs.org/) + [TypeScript](https://www.typescriptlang.org/)
* **UI**: TailwindCSS v4 + reusable React components
* **API client**: Orval (automatic client generation from OpenAPI)
* **Monorepo**: [NX](https://nx.dev/) (apps `one-site`, `entreprise`, shared libraries `libs/ui`, `libs/api`…)

### Backend / API

* **Framework**: Laravel 11
* **Quality & testing**: PestPHP, Laravel Pint
* **OpenAPI / Postman**: automatic generation and update of API documentation
* **Monitoring**: Prometheus Client PHP
* **Database**: MySQL/MariaDB
* **Infrastructure**: Kubernetes (Lens)

# Project Architecture

This document describes the overall architecture of the OAOS project (Frontend) developed at RTBF.

![Architecture diagram](https://mermaid.ink/img/pako\:eNqFVdty2jAQ_RWNnpIpGLAxFz90JoG-ddI25KkhD8JeHAUjeSQ5hWbyQfmO_lhXvnAxhvgFJJ9zdrVnV36joYyABjRWLH0mD9O5IPjcPM4pS9OEh8xwKXRnTp9Iu_2V3BYv8o0Smu9PcD_hi5P9Ke6nLFyxGJwXLQW50qHiqdHkbtO5g41pETChc12jfUOa0aEUSx47C6YrMks4LjR5mBWMgqOzRZG-zazYss9tkXEPtaSAtuYG9ukdAFwEgDAKUsV1M8Q70GiDCx1yNdmmCrS-boL3jxTPEUBEJyeoghxI9spjsKL0qHSTpuReZgZULXoFXdiqZwu0r9MMCHNbYtCo9tP-XtaLEF76dkYQLMJsk1zxgfHkDxcRee2fEVwiXKD7Tmnxi27GxTZPJV8gNGUHTPgiAWyey2U8cBxLNqeH0qyqp22MhG3x4I7RG3L1Pf9PFAu5ADKb3deT3zFtx4QJR4vbDQLFm8sJ7rvjIIBb9mPl9HH46q01N5TrFE8oTvyoQOHej2ZAdK5FKoB1NDM8OSfwmYUVrm7hJ74dDGLdOZdV9Tl2rhZ3h2p06RzYTriQpr2UmYguAe1sM2V4mNSvij3GR8zjo-M4Osli_fR0Auzv1Fg5iU0h_Z1eI6qpgPYO3mtMirvZlivjOJhT0DwWZLbVBtbkC5kZqbYLKVfHnV7S3LwNLW-SV1GTH-qVJci7BxYa8isDtW1kenmLKshvF2VY_O9DB6S8QVokb6tGoi1uxAxDv0DZmwSHccVFfDRMtIVfKx7RwKgMWnQNas3skr5ZCH44nmENcxoQq6VWtofekZMy8VvKdUVTMoufabBkicZVlmJYmHKGZdxDMBioCXaEoUHP87u5CA3e6IYGbc_zne5gPB66va476A1HLbqlgTscOP1h3_dHuOmP-v57i_7Nw_acwcjzB-PhaDT23FG3673_B7YnI5c)

### Monorepo Structure (Frontend)

```text
applications/
├─ apps/
│  ├─ one-site/
│  │  ├─ app/                     # App Router (Next 15 routing)
│  │  │  ├─ layout.tsx            # Root SSR Layout: injects <ClientLayout>…</ClientLayout>
│  │  │  └─ client-layout.tsx     # Client layout: auth, consent, tracking, providers
│  │  ├─ public/                  # Public assets
│  │  ├─ pages/                   # Pages Router
│  │  ├─ scripts/                 # Client-specific scripts for one-site
│  │  ├─ styles/                  # Tailwind v4, fonts
│  │  ├─ next.config.js
│  │  └─ project.json             # Nx target (build, dev, etc.)
│  ├─ entreprise/
│  │  ├─ app/
│  │  │  ├─ layout.tsx
│  │  │  ├─ client-layout.tsx
│  │  │  ├─ not-found.tsx
│  │  │  ├─ article/
│  │  │  │  └─ page.tsx
│  │  │  └─ [[...slugs]]/
│  │  │     └─ page.tsx
│  │  ├─ components/
│  │  ├─ styles/
│  │  ├─ public/
│  │  ├─ utils/
│  │  ├─ next.config.js
│  │  └─ project.json
│  ├─ one-site-e2e/               # E2E tests (Cypress)
│  └─ entreprise-e2e/
├─ libs/
│  ├─ ui/                         # Design System + Storybook
│  ├─ api/                        # Orval clients + React Query hooks + types
│  ├─ core/                       # Shared (scripts, utils)
│  └─ datalayer/                  # Tracking (schemas, helpers)
├─ package.json                   # Nx/Next/Storybook, Orval, etc.
└─ tsconfig.base.json             # TypeScript aliases for the monorepo
```

## 🚀 My Role & Contributions

* Development of **reusable UI components** (React/Next.js + Tailwind CSS + Orval API integration).
* **Front-end performance optimization** (lazy loading, bundle size reduction, caching, reducing JS payload).
* Management of **metadata in the Laravel backend**, using Postman to configure and test across different environments (local, UAT, production).
* Integration of **audience tracking** (Gemius / CIM Internet).
* **Collaboration** with backend, frontend, and UX design teams.
* Contribution to **CI/CD pipelines (GitLab)** to automate testing and deployments.
* **Agile (Scrum)**: participation in daily meetings, code reviews, and sprint planning.

## 📂 About This Repository

This repository **does not contain the original source code**, but instead:

* **Technical documentation** (README, architecture diagrams…).
* Key **technical decisions** and the stack used.
* **Screenshots** or **architecture diagrams** (see `/images` folder).
* A **timeline** or log of my contributions.

## 🔗 Resources

* [Next.js](https://nextjs.org/)
* [NX Monorepo](https://nx.dev/)
* [Laravel](https://laravel.com/)
* [TailwindCSS](https://tailwindcss.com/)
* [Orval](https://orval.dev/)

> *Author: Lucas Maroy — RTBF Internship 2025*
