# CLAUDE.md — SAWE Southeast Region Website

## Project Overview

SAWE (Society of Allied Weight Engineers) Southeast Region chapter website. Migrated from a legacy 2163-line single-page HTML site (Bootstrap 3, jQuery, Font Awesome 4) to a modern Astro 4.x static site.

**Live URL**: https://lively-moss-0fc93df10.1.azurestaticapps.net
**Repo**: https://github.com/markokstate66/sawe-se

## Tech Stack

| Layer | Choice |
|---|---|
| Static site generator | Astro 4.x |
| CSS framework | Bootstrap 5.3.3 (CDN — no integrity hash) |
| Icons | Font Awesome 6.5.1 Free (CDN) |
| Analytics | Google Analytics 4 (G-P33EBDLD11, GT-PHCDW4R4) |
| Contact form | Formspree (placeholder — `YOUR_FORM_ID` not yet set) |
| Calendar | Google Calendar embed iframe |
| PayPal | Client-side encrypted cart form (preserved from original) |
| Hosting | Azure Static Web Apps (Free tier) |
| CI/CD | GitHub Actions → Azure SWA auto-deploy on push to master |
| JS | Vanilla JS only — no jQuery, no bundler |

## Architecture

### Directory Structure

```
sawe-se/
├── public/
│   ├── documents/              # 82 PDFs (~37MB)
│   └── img/                    # 129 images (~74MB)
│       ├── about/
│       ├── events/
│       ├── header-slides/
│       ├── logos/
│       ├── news/
│       ├── team/
│       └── thumbnails/
├── src/
│   ├── components/             # 13 Astro components
│   │   ├── Navbar.astro        # Fixed-top nav, centered links, PayPal cart
│   │   ├── Header.astro        # BS5 carousel, logo, welcome text, notice banner
│   │   ├── About.astro         # Timeline section wrapper
│   │   ├── TimelineItem.astro  # Individual timeline entry (reusable)
│   │   ├── Events.astro        # Event cards (col-md-6) + calendar iframe (col-md-6)
│   │   ├── NewsSection.astro   # Meeting recap accordion + 3 portfolio items triggering modals
│   │   ├── NewsAccordion.astro # BS5 accordion — 2023 expanded, others collapsed
│   │   ├── NewsModal.astro     # Reusable modal for Aviation/Space link lists
│   │   ├── ChapterUpdatesModal.astro  # Modal with nested accordion of meeting minutes
│   │   ├── Membership.astro    # 3 icon cards (E-Store, Blog, Join/Renew)
│   │   ├── Officers.astro      # Team cards with BS5 tooltips, email/linkedin buttons
│   │   ├── Contact.astro       # Formspree form (placeholder ID)
│   │   └── Footer.astro        # Copyright, webmaster email, release notes link
│   ├── data/                   # 11 JSON data files (all editable content)
│   │   ├── site-config.json    # Title, copyright, webmaster email, notice, PayPal, calendar URL
│   │   ├── officers.json       # 5 officers: name, role, photo, email, linkedin, tooltip
│   │   ├── timeline.json       # 3 entries: year, heading, image, body, inverted
│   │   ├── header-slides.json  # 4 carousel slides (3 active, 1 inactive)
│   │   ├── events.json         # Active events + Google Calendar embed URL
│   │   ├── membership.json     # 3 items with FA6 icon classes
│   │   ├── aviation-links.json # 5 aviation news links
│   │   ├── space-links.json    # 4 space news links
│   │   ├── news-recaps.json    # Year groups (2018–2023), each with articles
│   │   ├── chapter-updates.json # Year groups (2017–2023) of meeting minutes docs
│   │   └── release-notes.json  # Changelog entries for /release-notes page
│   ├── layouts/
│   │   └── Layout.astro        # Base HTML: BS5/FA6 CDN, Google Fonts, GA4, vanilla JS
│   ├── pages/
│   │   ├── index.astro         # Main single-page site (assembles all components + modals)
│   │   └── release-notes.astro # /release-notes changelog page
│   └── styles/
│       └── agency.css          # Migrated theme CSS (~500 lines)
├── astro.config.mjs            # site: 'https://www.sersawe.org'
├── package.json                # Only dependency: astro ^4.16.0
├── staticwebapp.config.json    # Navigation fallback, PDF headers, security headers
├── .github/workflows/
│   └── azure-static-web-apps-lively-moss-0fc93df10.yml
├── CHANGELOG.md
├── WORKLOG.md
└── ARCHITECTURE.md
```

### Data-Driven Content

All site content lives in `src/data/*.json`. To update content (officers, events, news, etc.), edit the JSON files and push — no component changes needed.

**Accordion pattern**: JSON entries with `"expanded": true/false` control which accordion items are open by default. Convention: only the most recent year should be `expanded: true`.

**Release notes pattern**: Prepend new entries to `release-notes.json` array with `"expanded": true`, set previous entry to `false`.

### Pages

- `/` — Single-page site with all sections (Navbar → Header → About → Events → News → Membership → Officers → Contact → Footer + 3 Modals)
- `/release-notes` — Accordion-style changelog

## Deployment

### Azure Static Web Apps
- **Resource**: sawe-se-site (Free tier)
- **Resource Group**: rg-sawe-se (eastus2)
- **Subscription**: Summit Technology Group LLC
- **Default hostname**: lively-moss-0fc93df10.1.azurestaticapps.net

### CI/CD Pipeline
- Push to `master` branch triggers GitHub Actions workflow
- Workflow: `.github/workflows/azure-static-web-apps-lively-moss-0fc93df10.yml`
- Secret: `AZURE_STATIC_WEB_APPS_API_TOKEN_LIVELY_MOSS_0FC93DF10`
- Build config: `app_location: "/"`, `output_location: "dist"`
- Typical build time: ~1m15s

## Build Commands

```bash
npm install          # Install dependencies
npm run dev          # Local dev server (http://localhost:4321)
npm run build        # Production build → dist/
npm run preview      # Preview production build locally
```

## Key Decisions and Gotchas

### Bootstrap 5 CDN — No Integrity Hashes
The BS5 CDN links in Layout.astro do NOT use `integrity` attributes. An incorrect hash was silently blocking all Bootstrap JS (accordions, modals, tooltips, carousel). If adding integrity hashes back, verify them carefully.

### BS3 → BS5 Class Mapping
| BS3 | BS5 |
|---|---|
| `data-toggle` | `data-bs-toggle` |
| `data-target` | `data-bs-target` |
| `data-dismiss` | `data-bs-dismiss` |
| `data-parent` | `data-bs-parent` |
| `data-ride` | `data-bs-ride` |
| `.item` | `.carousel-item` |
| `.in` | `.show` |
| `img-responsive` | `img-fluid` |
| `img-circle` | `rounded-circle` |
| `sr-only` | `visually-hidden` |
| `col-lg-offset-*` | `offset-lg-*` |
| `navbar-default` | `navbar-dark bg-dark` |
| `navbar-fixed-top` | `fixed-top` |

### FA4 → FA6 Icon Mapping
| FA4 | FA6 |
|---|---|
| `fa fa-*` | `fa-solid fa-*` |
| `fa-linkedin` | `fa-brands fa-linkedin-in` |
| `fa-shopping-cart` | `fa-cart-shopping` |

### Image Size Constraints (in agency.css)
- `.news-article-row img` — max-width: 295px
- `.accordion-body img` — max-width: 295px
- `.portfolio-modal .table img` — max-width: 100px
- Event images — inline max-width: 295px

### Theme Colors
- Primary/Accent: `#fed136` (gold)
- Dark: `#222`
- Muted text: `#777`
- Light background: `#eee`

## Pending Items
- [ ] Formspree form ID — replace `YOUR_FORM_ID` in Contact.astro
- [ ] Copyright year — update "2023" in site-config.json
- [ ] Custom domain — point sersawe.org DNS to Azure SWA
- [ ] Visual QA against original site
- [ ] Mobile responsive testing
- [ ] Verify all 82 PDF document links on live site
