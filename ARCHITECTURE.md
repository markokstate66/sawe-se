# SAWE Southeast Region Website — Architecture

## Overview

Single-page static site built with **Astro 4.x**, styled with **Bootstrap 5** (CDN), and deployed to **Azure Static Web Apps**.

## Tech Stack

| Layer | Choice |
|---|---|
| Static site generator | Astro 4.x |
| CSS framework | Bootstrap 5 (CDN) |
| Icons | Font Awesome 6 Free (CDN) |
| Analytics | Microsoft Clarity (placeholder) |
| Contact form | Formspree (replaces PHP) |
| Calendar | Google Calendar embed |
| PayPal | Client-side encrypted forms (preserved) |
| Hosting | Azure Static Web Apps (free tier) |
| JS | Vanilla JS only (scroll listener + tooltip init) |

## Directory Structure

```
sawe-se/
├── public/
│   ├── documents/          # 82 PDFs
│   └── img/                # Images (about, events, header-slides, logos, news, team, thumbnails)
├── src/
│   ├── components/         # 13 Astro components
│   ├── data/               # 10 JSON data files
│   ├── layouts/            # Base Layout with CDN links and JS
│   ├── pages/              # index.astro (single page)
│   └── styles/             # agency.css (migrated theme)
├── astro.config.mjs
├── package.json
├── staticwebapp.config.json
└── .github/workflows/azure-static-web-apps.yml
```

## Data Architecture

All content is stored in JSON files under `src/data/`, making it easy to update without touching component markup.

## Key Migration Decisions

- **BS3 → BS5**: All `data-toggle` → `data-bs-toggle`, `.item` → `.carousel-item`, `.in` → `.show`, etc.
- **jQuery removed**: Replaced with CSS `scroll-behavior: smooth` and vanilla JS for navbar scroll effect and tooltip init.
- **FA4 → FA6**: `fa fa-*` → `fa-solid fa-*`, `fa-linkedin` → `fa-brands fa-linkedin-in`, `fa-shopping-cart` → `fa-cart-shopping`.
- **Google Analytics → Clarity**: Deprecated UA tracking replaced with Clarity placeholder.
- **PHP contact form → Formspree**: Static-site compatible form backend.
