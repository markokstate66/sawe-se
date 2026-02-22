# Work Log

## Session 2 — 2026-02-22: Deployment, Fixes, and Go-Live

### Completed
- [x] Fixed Bootstrap 5 accordion/modal/tooltip not working (removed bad CDN integrity hashes from Layout.astro)
- [x] Fixed Chapter Updates accordion — set only 2023 as expanded, all others collapsed
- [x] Constrained oversized images: news articles 295px, accordion images 295px, modal thumbnails 100px
- [x] Changed Events section to half-width layout (col-md-6 events + col-md-6 calendar)
- [x] Centered navbar links with `mx-auto`
- [x] Fixed timeline images and contact form textarea sizing
- [x] Replaced Microsoft Clarity placeholder with Google Analytics 4 (GA4)
  - Tag IDs: G-P33EBDLD11, GT-PHCDW4R4
- [x] Created GitHub repo: markokstate66/sawe-se
- [x] Created Azure resource group: rg-sawe-se (eastus2, Summit Technology Group LLC subscription)
- [x] Created Azure Static Web App: sawe-se-site (Free tier)
- [x] Fixed auto-generated workflow (bad `app_location` path)
- [x] Set deployment token as GitHub secret
- [x] Committed and pushed 248 files — first successful deployment
- [x] Added `/release-notes` page with Bootstrap 5 accordion changelog
- [x] Added release notes link in footer
- [x] Created `src/data/release-notes.json` for managing changelog entries
- [x] Updated WORKLOG.md, CHANGELOG.md, and CLAUDE.md

### Pending
- [ ] Replace Formspree `YOUR_FORM_ID` with actual form ID in Contact.astro
- [ ] Update copyright year in site-config.json (currently says 2023)
- [ ] Set up custom domain (sersawe.org → Azure SWA)
- [ ] Visual QA — compare each section against original site
- [ ] Mobile responsive testing at all breakpoints
- [ ] Verify all 82 PDF document links on live site

---

## Session 1 — Initial Migration

### Completed
- [x] Scaffolded Astro 4.x project
- [x] Copied 82 PDFs to `public/documents/`
- [x] Copied all images to `public/img/`
- [x] Created `Layout.astro` with BS5, FA6, Google Fonts CDN links
- [x] Extracted all content from `index.html` into 10 JSON data files
- [x] Built all 13 Astro components
- [x] Migrated CSS from BS3 to BS5 (agency.css)
- [x] Added vanilla JS for navbar scroll + tooltip init
- [x] Created Azure SWA config and GitHub Actions workflow
- [x] Verified `npm run build` succeeds
