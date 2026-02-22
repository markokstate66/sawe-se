# SAWE Southeast Region Website — Architecture

See [CLAUDE.md](./CLAUDE.md) for full architecture documentation, deployment details, build commands, and key decisions.

## Quick Reference

- **Stack**: Astro 4.x + Bootstrap 5 (CDN) + Font Awesome 6 (CDN) + vanilla JS
- **Hosting**: Azure Static Web Apps (Free tier)
- **CI/CD**: GitHub Actions — push to master auto-deploys
- **Content**: 11 JSON data files in `src/data/` — edit JSON, push, done
- **Components**: 13 Astro components in `src/components/`
- **Pages**: `/` (main single-page site), `/release-notes` (changelog)
- **Analytics**: Google Analytics 4
