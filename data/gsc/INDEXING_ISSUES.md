# Sitemap & Indexing Health

Status: **Partially complete, with one urgent GSC-confirmed finding.**
Crawl-verifiable facts below are confirmed from the Digicorns audit. True GSC
Coverage-report data (indexed vs. submitted counts, exclusion reasons,
"Discovered — not indexed," etc.) is still **Blocked — Needs Live GSC
Export** (Coverage report specifically was not among the files provided).

## Search Appearance (real GSC export — empty)

The Search Appearance export came back with zero rows — AllCheck currently
has no special search-appearance types (rich results, FAQ snippets, review
stars, etc.) showing in Google. This is expected given no FAQ schema exists
yet (see `HOMEPAGE_BATCH.md`) — implementing valid, matching FAQ schema in
Homepage Batch 1 is the most direct way to start populating this category.

## Urgent — confirmed by real GSC Pages export

`Pages.csv` shows `http://www.allcheck.biz/` and `https://allcheck.biz/`
as two separate entries with very different average positions (3.71 vs
29.95) and impression volumes (2,487 vs 8,719) — see `CANNIBALIZATION.md`
for full detail. This means Google is not treating the www→non-www
redirect as fully consolidated (or it isn't 301ing at all), despite the
canonical tag correctly declaring `https://allcheck.biz/`. The same www
split appears on `/contact-us/` too, so this is sitewide, not homepage-only.
**Recommend this move to the top of the technical priority list** — ahead of
the trailing-slash and location-page cleanups — since it may be actively
splitting the site's strongest ranking signal away from the canonical URL.

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
