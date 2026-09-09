# Technical URL Cleanup

Status: **Waiting on Developer** for implementation (redirects/canonical tags
require server/CMS access this session does not have). Recommendations below
are built from the actual internal-link crawl in the Digicorns audit of
allcheck.biz, not assumptions.

Do not implement any of these as guesses — every row below cites the exact
URLs found live in the crawl. Where only one variant appears in the crawl,
that is noted so the developer can spot-check the other rather than being
told it doesn't exist.

## Priority order (per CLAUDE.md / audit) — UPDATED after real GSC data

Original order: duplicate H1s → heading hierarchy → page speed → missing alt
text → LocalBusiness schema → address/NAP → meta description → URL cleanup.

**Escalation:** real GSC data (`data/gsc/Pages.csv` export, see
`data/gsc/CANNIBALIZATION.md` and `data/gsc/INDEXING_ISSUES.md`) confirms
`http://www.allcheck.biz/` and `https://allcheck.biz/` are being tracked by
Google as two different pages with very different average positions (3.71 vs
29.95) — and the same www split shows up on `/contact-us/` too. This is no
longer a theoretical crawl-based concern; it's live, GSC-confirmed evidence
that ranking signal may be split away from the canonical URL sitewide.

**Second escalation, equally urgent:** the real GSC Coverage report (see
`data/gsc/INDEXING_ISSUES.md`) shows a **publicly crawlable staging site**
at `/staging/*` duplicating real content, and a **404'd Greenwood location
page** (`/greenwood-indiana/`) that directly explains a real ranking decline
already seen in `data/gsc/RANKING_CHANGES.md`.

**Updated top priority order, all co-equal urgent (not sequential — a
developer could take these in parallel):**
1. www→non-www 301 (and any remaining http→https)
2. Block/deindex `/staging/*` entirely
3. Restore or redirect `/greenwood-indiana/`

Then the trailing-slash and location-page-pattern cleanups below.

## NEW — publicly crawlable staging site (co-top-priority)

The real GSC Coverage report shows at least 9 URLs under `/staging/` being
crawled as live, indexable duplicate content: `/staging/indoor-air-quality-testing/`
(and no-slash twin), `/staging/new-construction-phased`,
`/staging/mold-and-mildew-testing/`, `/staging/be-an-informed-buyer/`,
`/staging/news/`, `/staging/limited-warranty` (and slash twin),
`/staging/sample-inspection-agreement`. Full detail in
`data/gsc/INDEXING_ISSUES.md`.

**Fix:** `Disallow: /staging/` in `robots.txt`, server-level `noindex` for
that path, and ideally HTTP auth or a non-public subdomain so it's never
crawlable. This is likely the single largest contributor to the site's 33
"crawled — currently not indexed" pages — bigger than any individual
trailing-slash duplicate below.

## NEW — `/greenwood-indiana/` 404 (explains a real ranking decline)

`https://allcheck.biz/greenwood-indiana/` — the location-hub URL matching
the pattern of the working `/avon-indiana/` page — returns 404 (last
crawled Jul 10, 2026). This is the most likely cause of the Greenwood
decline cluster in `data/gsc/RANKING_CHANGES.md` (three Greenwood queries
all dropped 5-7 positions in the same window). Note:
`/complete-home-inspection-greenwood-indiana/` (the *service*+city page)
still exists and has real traffic — it's specifically the city-hub page
that's missing/broken.

**Fix:** confirm with developer whether this page existed before and was
removed/renamed; restore it or 301 it to whichever page should now serve
that intent.

## Confirmed duplicate / inconsistent URL pairs (both seen live in crawl, now expanded with real Coverage-report evidence)

| Canonical (recommended) | Duplicate/variant also found | Fix |
|---|---|---|
| `https://allcheck.biz/contact-us/` | `https://allcheck.biz/contact-us` (no trailing slash) | 301 the non-slash version to the slash version; update any internal links pointing to the non-slash form |
| `https://allcheck.biz/radon-testing/` | `https://allcheck.biz/radon-testing` | Same — 301 non-slash → slash |
| `https://allcheck.biz/indoor-air-quality-testing/` | `https://allcheck.biz/indoor-air-quality-testing` | Same |
| `https://allcheck.biz/terms-of-service/` | `https://allcheck.biz/terms-of-service` | Same |
| `https://allcheck.biz/glossary-of-terms/` | `https://allcheck.biz/glossary-of-terms` | Same — confirmed via real Coverage report, not previously flagged |
| `https://allcheck.biz/new-construction-phased/` | `https://allcheck.biz/new-construction-phased` | Same — confirmed via real Coverage report |
| `https://allcheck.biz/agents/` | `https://allcheck.biz/agents` | Same — confirmed via real Coverage report |
| `https://allcheck.biz/limited-warranty/` | `https://allcheck.biz/limited-warranty` | Same — confirmed via real Coverage report |
| `https://allcheck.biz/services/` | `https://allcheck.biz/services` | Same — confirmed via real Coverage report |

Also confirmed via the real Coverage report: URL-parameter duplicates of
real pages are being crawled as separate URLs (RSS/social-share tracking
params like `?utm_source=rss&...`, `?source=post_page...`,
`?trk=organization_guest_main-feed-card-text`). Same root cause as the
above — canonical tags aren't reliably collapsing these back to the clean
URL. Fix at the template/canonical-tag level rather than one redirect at a
time.

## Confirmed duplicate location-page URL *patterns* (same city, two different URL structures both indexed)

The site is running two different location-URL conventions simultaneously.
Pick **one** pattern and 301 the other into it — recommend the
`/complete-home-inspection/<city>-indiana/` pattern since it nests location
pages under the service, which is cleaner for topical/service-area clarity,
but confirm with whichever pattern currently holds the stronger rankings in
GSC before finalizing (see `GSC_ANALYSIS.md` — do not pick blind).

| City | Pattern A (found live) | Pattern B (found live) |
|---|---|---|
| Carmel | `/complete-home-inspection-carmel-indiana/` | `/complete-home-inspection/carmel-indiana/` — **confirmed real and being crawled** (shows in the "crawled — not indexed" bucket, unlike Fishers' equivalent which 404s), so this decision is still genuinely open, not resolved by the 404 check |
| Central Indiana | `/complete-home-inspection-central-indiana/` | `/complete-home-inspection/central-indiana/` |
| Fishers | `/complete-home-inspection-fishers-indiana/` | **RESOLVED** — the single-slash version (`/complete-home-inspection/fishers-indiana/`) is confirmed 404 via the real Coverage report. Pattern A is the only real page for Fishers; no redirect decision needed here, just confirm this 404 doesn't need restoring (it's correctly gone). The malformed double-slash variant below is a separate, still-open issue. |
| Noblesville | `/complete-home-inspection-noblesville-indiana/` | `/complete-home-inspection/noblesville-indiana/` |
| Greenwood | `/complete-home-inspection-greenwood-indiana/` | not seen in this crawl — developer should confirm whether a Pattern B page exists or 404s before redirecting |

**This is a likely cannibalization source** flagged in `GSC_ANALYSIS.md` —
two indexable URLs per city competing for the same "complete home inspection
+ [city]" intent. Resolve with a canonical tag + 301, not just a canonical
tag alone, so link equity and crawl budget consolidate.

## Broken / malformed URLs found live in the crawl

1. **`https://allcheck.biz/omplete-home-inspection/fishers-indiana//`** — a
   typo'd internal link (missing the leading "c" in "complete") *and* a
   double trailing slash. This is not a real page; it's a broken `href`
   somewhere in the site (menu, footer, or a service card) pointing to a
   non-existent/malformed path. **Action:** find the source link (likely in
   the Fishers-area navigation or a related-services block) and fix the
   `href` to the canonical Fishers URL chosen above. Do not just redirect
   this one path — the broken link itself needs to be corrected at the
   source, or it will keep generating fresh 404s/soft-redirects as it's
   re-crawled.
2. **`https://allcheck.biz/complete-home-inspection/fishers-indiana//`** —
   double trailing slash on an otherwise valid pattern-B path. Fix the
   template/link so it emits a single trailing slash.

## Confirmed triplicate URL problem: 4-Point Inspection

Three different live paths were found for what should be one page:

- `https://allcheck.biz/4-point-inspection/` (bare — legacy path style)
- `https://allcheck.biz/service/4-point-inspection/` (singular "service")
- `https://allcheck.biz/services/4-point-inspection/` (plural "services" —
  matches the pattern used by every other service page, e.g.
  `/services/complete-home-inspection/`, `/services/reinspection/`,
  `/services/home-maintenance-inspection/`, `/services/investor-services/`,
  `/services/light-commercial-inspection/`, `/services/new-construction-phased/`,
  `/services/environmental-testing-2/`, `/services/end-of-builders-warranty/`)

**Recommended canonical: `https://allcheck.biz/services/4-point-inspection/`**
— it matches every other service page's structure, so it's the consistent
choice. 301 the other two into it. This matches Priority 2's "4-Point
Inspection consolidation" task — do that page's content work only after this
redirect consolidation is live, so link equity and any analytics history land
on the surviving URL first.

## Suspicious duplicate-slug pattern: Environmental Testing

Live URL is `https://allcheck.biz/services/environmental-testing-2/` — the
`-2` suffix is a classic WordPress signal that a page named
`environmental-testing` already existed (in trash, draft, or was deleted)
when this one was created, so WordPress auto-appended `-2` to the slug.

**Action for developer:** check whether `/services/environmental-testing/`
(no suffix) exists as a trashed/draft/redirected page. If it once existed and
has backlinks or old rankings, 301 it to `/services/environmental-testing-2/`
(or, better, rename the live page to drop the `-2` suffix entirely and 301
the old `-2` URL to the clean slug — cleaner for AllCheck's own long-term
URLs, but only do this if GSC shows the `-2` URL is not already the one
holding current rankings; check `GSC_ANALYSIS.md` first).

## Legacy CMS URLs still receiving backlinks (link-equity risk)

The audit's backlink data shows real referring links still pointing at old
paths from what appears to be a prior Joomla-based site:

- `http://www.allcheck.biz/component/k2/item/2-where-does-it-come-from.htm...` (2 backlinks)
- `http://www.allcheck.biz/component/k2/item/1-lorem-ipsum-is-simply-dumm...` (1 backlink)
- `http://allcheck.biz/component/k2/item/2-where-does-it-come-from.html` (1 backlink)
- `http://www.allcheck.biz/_information/articles/keep_basement_web.pdf` (30 backlinks — meaningful equity)
- `http://www.allcheck.biz/_information/warranty.htm` (1 backlink per the
  original audit — **confirmed via the real Coverage report to currently
  404** (shown as `https://allcheck.biz/_information/warranty.htm` in the
  real 404 examples). Modest backlink count, but free, real equity — 301 to
  `/services/end-of-builders-warranty/`.)
- `http://www.allcheck.biz/inspections/complete-home-inspection.html` (1 backlink)

**Action:** confirm whether these currently 404 or already redirect. The
`keep_basement_web.pdf` legacy path alone carries 30 backlinks and should not
be left as a dead link — 301 it to the closest live equivalent content (or
recreate that resource) rather than losing that link equity. This is squarely
a **Waiting on Developer** item since it requires server/host access to check
current redirect status.

## Domain/protocol variants (www / http / https)

- Canonical tag on the homepage correctly declares `https://allcheck.biz/`.
- The audit's own backlink data shows `http://www.allcheck.biz/` carrying 230
  backlinks (the single largest link target in the whole backlink profile)
  and `https://www.allcheck.biz/` carrying 2 more — both must 301 to
  `https://allcheck.biz/` (non-www) or all of that link equity is at risk of
  being wasted or, worse, split/cannibalized.
- **This session cannot verify live redirect behavior** (no network access to
  allcheck.biz from this environment). Flag as **Waiting on Developer**:
  confirm `http://allcheck.biz/`, `https://www.allcheck.biz/`, and
  `http://www.allcheck.biz/` all issue a single-hop 301 to
  `https://allcheck.biz/`.

## Tracker status

| Item | Status |
|---|---|
| **Staging site publicly crawlable (`/staging/*`)** | **Waiting on Developer — new top priority** |
| **`/greenwood-indiana/` 404 (explains real ranking decline)** | **Waiting on Developer — new top priority** |
| www / http variant redirects | Waiting on Developer — top priority, GSC-confirmed |
| contact-us / radon-testing / indoor-air-quality-testing / terms-of-service / glossary-of-terms / new-construction-phased / agents / limited-warranty / services trailing-slash dupes | Waiting on Developer — list expanded via real Coverage report |
| URL-parameter duplicates (RSS/social-share tracking params) | Waiting on Developer — same root cause as trailing-slash dupes (unreliable canonical tags) |
| Location-page URL pattern consolidation — Carmel, Central Indiana, Noblesville still open; **Fishers resolved** (Pattern B confirmed 404, no action needed) | Waiting on Client input (pick pattern) + Developer (implement) |
| Malformed `omplete-home-inspection` typo link | Waiting on Developer |
| Fishers double-trailing-slash (`/complete-home-inspection/fishers-indiana//`) | Waiting on Developer |
| 4-Point Inspection triplicate URLs | Waiting on Developer — canonical recommendation given above |
| Environmental Testing `-2` slug | Waiting on Developer (needs history check) |
| `/_information/warranty.htm` 404 (1 backlink) | Waiting on Developer — 301 target identified |
| `/_information/articles/keep_basement_web.pdf` (30 backlinks) status | Waiting on Developer — not yet confirmed 404 or live |
| Legacy Joomla URLs (component/k2/item/...) | Waiting on Developer |
| Legacy duplicate PDF paths (`/pdf/*.pdf` vs `/wp-content/uploads/.../*_web.pdf`) | Waiting on Developer — low priority |
| `/our-standards/` possible duplicate of `/standards-of-practice/` | Waiting on Developer to confirm |
