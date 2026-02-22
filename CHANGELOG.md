# Changelog

## 1.1.0 — 2026-02-22: Deployment and Polish

### Added
- `/release-notes` page with Bootstrap 5 accordion-style changelog
- `src/data/release-notes.json` for managing changelog entries (11th data file)
- Release notes link in site footer
- Google Analytics 4 integration (GA4 tag IDs: G-P33EBDLD11, GT-PHCDW4R4)
- GitHub Actions CI/CD pipeline deploying to Azure Static Web Apps
- Azure Static Web App resource (Free tier, eastus2 region)

### Fixed
- Bootstrap 5 JS not loading due to incorrect CDN integrity hash — removed integrity attributes
- Chapter Updates accordion: only 2023 expanded by default (2022 was incorrectly set to expanded)
- Oversized images throughout site — added max-width constraints (295px for articles, 100px for modal thumbnails)
- Events section calendar was full-width — changed to half-width (col-md-6/col-md-6) layout
- Navbar links not centered — switched from `ms-auto` to `mx-auto`
- Timeline images and contact form textarea sizing
- Azure workflow had bad `app_location` ("C:/Program Files/Git/") — fixed to "/"

### Changed
- Replaced Microsoft Clarity analytics placeholder with Google Analytics 4
- Events section uses responsive grid instead of table-based layout

---

## 1.0.0 — Initial Astro Migration

### Added
- Astro 4.x static site generator
- Bootstrap 5 (CDN) replacing Bootstrap 3
- Font Awesome 6 Free (CDN) replacing Font Awesome 4
- 13 Astro components: Navbar, Header, About, TimelineItem, Events, NewsSection, NewsAccordion, NewsModal, ChapterUpdatesModal, Membership, Officers, Contact, Footer
- 10 JSON data files for all content (officers, timeline, news recaps, chapter updates, events, membership, aviation/space links, header slides, site config)
- Vanilla JS for navbar scroll effect and Bootstrap tooltip initialization
- Azure Static Web Apps deployment config (staticwebapp.config.json)
- GitHub Actions CI/CD workflow
- Formspree contact form placeholder (replaces PHP)

### Removed
- jQuery 1.x dependency
- Bootstrap 3
- Font Awesome 4
- Google Analytics (Universal Analytics)
- PHP contact form backend
- IE8/9 polyfills (html5shiv, respond.js)
- jQuery easing plugin
- jqBootstrapValidation plugin

### Changed
- All content extracted from monolithic 2163-line HTML into JSON data files
- Document links converted from `http://www.sersawe.org/documents/` to `/documents/`
- BS3 classes migrated to BS5 equivalents
- Carousel, accordion, modal, and tooltip markup updated for BS5
