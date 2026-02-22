# Changelog

## 1.0.0 — Initial Astro Migration

### Added
- Astro 4.x static site generator
- Bootstrap 5 (CDN) replacing Bootstrap 3
- Font Awesome 6 Free (CDN) replacing Font Awesome 4
- 13 Astro components: Navbar, Header, About, TimelineItem, Events, NewsSection, NewsAccordion, NewsModal, ChapterUpdatesModal, Membership, Officers, Contact, Footer
- 10 JSON data files for all content (officers, timeline, news recaps, chapter updates, events, membership, aviation/space links, header slides, site config)
- Vanilla JS for navbar scroll effect and Bootstrap tooltip initialization
- Azure Static Web Apps deployment config
- GitHub Actions CI/CD workflow
- Formspree contact form (replaces PHP)
- Microsoft Clarity analytics placeholder (replaces deprecated Google UA)

### Removed
- jQuery 1.x dependency
- Bootstrap 3
- Font Awesome 4
- Google Analytics (UA)
- PHP contact form backend
- IE8/9 polyfills (html5shiv, respond.js)
- jQuery easing plugin
- jqBootstrapValidation plugin

### Changed
- All content extracted from monolithic 2163-line HTML into JSON data files
- Document links converted from `http://www.sersawe.org/documents/` to `/documents/`
- BS3 classes migrated to BS5 equivalents
- Carousel, accordion, modal, and tooltip markup updated for BS5
