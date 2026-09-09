# Sitemap & Indexing Health

Status: **Done — real GSC Coverage/Indexing data received.**

## Headline finding: 62 of ~149 known pages are NOT indexed right now

Real Coverage report data (`Chart.csv`, `Critical_issues.csv`), most recent
date (2026-09-04): **62 pages not indexed, 87 indexed** (~149 known pages
total, so ~42% of the site isn't in Google's index at all). The five
exclusion reasons sum exactly to 62, so this is internally consistent, real
data:

| Reason | Source | Pages | Read |
|---|---|---:|---|
| Crawled - currently not indexed | Google systems | **33** | Google visited these pages and chose not to index them — typically a thin/duplicate/low-value-content signal. This is over half of all excluded pages and the single biggest issue on the site. Directly consistent with the duplicate-URL problem already flagged in `TECHNICAL_URL_CLEANUP.md` and `CANNIBALIZATION.md` — Google may be seeing near-duplicate location/service pages and declining to index the weaker copies. |
| Excluded by 'noindex' tag | Website | 9 | **Needs the actual URL list** — if any of these are pages that should be indexed (a service or location page accidentally noindexed), that's an urgent fix. A count alone can't tell us that. |
| Page with redirect | Website | 9 | Expected if these are the known duplicate-URL redirects already in place — but needs the URL list to confirm they're the *intended* redirects and not something unrelated. |
| Not found (404) | Website | 8 | **Needs the URL list** — cross-check against the legacy Joomla URLs with real backlinks flagged in `TECHNICAL_URL_CLEANUP.md` (e.g. `/component/k2/item/...`, `/_information/warranty.htm`). If any of those 8 are the same URLs, that's real link equity being lost to a 404 instead of a 301. |
| Alternate page with proper canonical tag | Website | 3 | Only 3 pages currently resolve correctly via canonical tag. Given how many duplicate URL *pairs* exist sitewide (contact-us, radon-testing, environmental-testing, the location-page pattern pairs, the 4-point triplicate), this number should be much higher if canonicalization were working properly — **this confirms most of those duplicate pairs do NOT have working canonical tags**, reinforcing the urgency in `TECHNICAL_URL_CLEANUP.md`. |

## Trend over time (real, from Chart.csv, June 11 – Sept 4)

Indexing health has been **improving**, not worsening: "Not indexed" dropped
from 114 (mid-June) to 62 (current), while "Indexed" grew from 81 to 87. The
drops happened in visible steps (e.g. 92→76 around Aug 22, 76→62 around Aug
29) rather than gradually, suggesting periodic re-crawls picked up fixes
already made. This is a positive baseline signal, but 62 un-indexed pages is
still a real, substantial problem worth acting on, not something to treat as
resolved.

## What's still needed to act on this

The counts above tell us *how many* and *why*, but not *which* pages. GSC
lets you click into each reason row to see the actual URL list — please
export those for at least these two (most actionable):
- [ ] **Waiting on Client:** URL list for "Excluded by 'noindex' tag" (9
      pages) — confirms nothing important is accidentally hidden from Google.
- [ ] **Waiting on Client:** URL list for "Not found (404)" (8 pages) — to
      cross-check against the legacy Joomla backlink URLs.
- [ ] Lower priority: URL list for "Crawled - currently not indexed" (33
      pages) — useful for confirming which specific pages Google considers
      too thin/duplicate, but likely overlaps heavily with pages already
      flagged in `TECHNICAL_URL_CLEANUP.md`.

## Search Appearance (real GSC export — empty)

The Search Appearance export came back with zero rows — AllCheck currently
has no special search-appearance types (rich results, FAQ snippets, review
stars, etc.) showing in Google. This is expected given no FAQ schema exists
yet (see `HOMEPAGE_BATCH.md`) — implementing valid, matching FAQ schema in
Homepage Batch 1 is the most direct way to start populating this category.

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

- [x] GSC Coverage/Indexing report received and processed — see headline
      finding above. Superseded the earlier "blocked" status.
- [ ] **Waiting on Client:** URL lists for the noindex (9) and 404 (8)
      buckets specifically — see above.
