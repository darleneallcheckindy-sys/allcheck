# Sitemap & Indexing Health

Status: **Partially complete.** Crawl-verifiable facts below are confirmed
from the Digicorns audit. True GSC Coverage-report data (indexed vs.
submitted counts, exclusion reasons, "Discovered — not indexed," etc.) is
**Blocked — Needs Live GSC Export**, since no Search Console access exists in
this session.

## Confirmed (from audit crawl, verifiable facts — not GSC)

- [x] XML sitemap present: `https://allcheck.biz/sitemap.xml`
- [x] Secondary sitemap present: `https://allcheck.biz/sitemap.rss`
- [x] `robots.txt` present at `http://allcheck.biz/robots.txt`
- [x] `robots.txt` does not block any major search engine
- [x] `robots.txt` does not block any major AI crawler
- [x] No `noindex` meta tag on homepage
- [x] No `noindex` HTTP header on homepage
- [x] Canonical tag present on homepage: `https://allcheck.biz/`
- [x] SSL enabled, HTTPS redirect working (on the URL the audit crawled)

## Known duplicate URL variants (crawl-confirmed — indexing risk)

See `TECHNICAL_URL_CLEANUP.md` for the full list and redirect recommendations.
Summary of what affects indexing specifically:
- `/contact-us` vs `/contact-us/`
- `/radon-testing` vs `/radon-testing/`
- `/indoor-air-quality-testing` vs `/indoor-air-quality-testing/`
- `/terms-of-service` vs `/terms-of-service/`
- Duplicate location-page URL patterns for Carmel, Central Indiana, Fishers,
  Noblesville (two different indexable URL structures per city)
- Triplicate 4-Point Inspection URLs (`/4-point-inspection/`,
  `/service/4-point-inspection/`, `/services/4-point-inspection/`)
- Malformed URL: `/omplete-home-inspection/fishers-indiana//` (typo + double
  trailing slash — likely a broken internal link, not itself a real
  indexed page, but worth checking in GSC's Coverage report in case Google
  discovered and attempted to crawl it)
- `/services/environmental-testing-2/` — the `-2` slug suggests a prior page
  at `/services/environmental-testing/` may exist in a redirected, trashed,
  or orphaned state; worth checking GSC Coverage for that exact URL

## Important pages to confirm are indexed (once GSC access exists)

- [ ] Homepage
- [ ] All 7 Priority 2 service pages (`complete-home-inspection`,
      `environmental-testing-2`, `radon-testing`, `termite-inspection`,
      the canonical 4-point-inspection URL, `new-construction-phased`,
      `end-of-builders-warranty`)
- [ ] All confirmed location pages (Avon, Carmel, Fishers, Greenwood,
      Noblesville, Central Indiana)
- [ ] `/about-us/`
- [ ] `/faq/`

## Action needed

- [ ] **Waiting on Client:** GSC Coverage/Indexing report export to confirm
      actual indexed status, any "Discovered — currently not indexed" pages,
      and canonical-URL mismatches Google has chosen on its own.
