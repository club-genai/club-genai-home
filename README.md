# Club GenAI Home

[![Deploy to GitHub Pages](https://github.com/t0sa/club-genai-home/actions/workflows/deploy.yml/badge.svg)](https://github.com/t0sa/club-genai-home/actions/workflows/deploy.yml)

Site vitrine du **[Club GenAI Bordeaux](https://www.meetup.com/groupe-meetup-bordeaux-developpement-web/)** — communauté autour de l'IA générative. Meetups, projets open source et veille GenAI.

**→ [t0sa.github.io/club-genai-home](https://t0sa.github.io/club-genai-home/)**

---

## Stack

| Couche | Technologie |
|--------|-------------|
| Framework | [Astro 4](https://astro.build) — génération statique |
| Style | [Tailwind CSS v3](https://tailwindcss.com) — palette Anthropic-inspired, dark mode |
| Hosting | GitHub Pages via GitHub Actions |
| Données | Fichiers JSON dans `src/data/`, mis à jour automatiquement |

## Fonctionnalités

- **Actualités** — lien du prochain meetup, configurable dans `src/data/config.json`
- **Projets GitHub** — repos `club-genai-*` récupérés via l'API GitHub, affichage paginé
- **Veille GenAI** — articles OpenAI, Google DeepMind, Meta AI + repos GitHub trending, récupérés à chaque déploiement
- **Dark mode** — toggle lune/soleil, persistance localStorage, anti-FOUC

## Développement local

```bash
git clone https://github.com/t0sa/club-genai-home.git
cd club-genai-home
npm install
npm run dev        # http://localhost:4321
```

```bash
npm run build      # build statique → dist/
npm test           # tests unitaires (node:test)
```

## Mettre à jour le contenu

### Lien meetup

Éditer `src/data/config.json` directement sur GitHub ou en local :

```json
{
  "meetup_url": "https://www.meetup.com/.../events/12345",
  "meetup_label": "Meetup GenAI #12 — Agents & RAG",
  "meetup_date": "2026-05-15",
  "meetup_location": "SFEIR Bordeaux"
}
```

Un push sur `main` déclenche le rebuild automatiquement.

### Données (projets + veille)

Les données (projets + veille) sont récupérées automatiquement **à chaque déploiement** par `deploy.yml`. Pour forcer un refresh, déclenche un déploiement :

```bash
gh workflow run deploy.yml
```

## Structure

```
src/
  data/           ← JSON mis à jour par GitHub Actions
  components/     ← Nav, Hero, Actualites, ProjectList, VeilleGenAI, Footer, ThemeToggle
  layouts/        ← Base.astro (anti-FOUC, dark mode)
  pages/          ← index.astro
.github/
  scripts/        ← fetch-projects.js, fetch-veille.js
  workflows/      ← deploy.yml
docs/
  solutions/      ← solutions documentées (bugs, best practices)
  plans/          ← plans d'implémentation
```

## Licence

MIT
