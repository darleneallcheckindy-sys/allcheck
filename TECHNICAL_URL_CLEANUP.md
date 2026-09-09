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
that ranking signal may be split away from the canonical URL sitewide. **Move
the www→non-www (and any remaining http→https) 301 redirect fix to the very
top of this file's priority, ahead of the trailing-slash and location-page
cleanups below.**

## Confirmed duplicate / inconsistent URL pairs (both seen live in crawl)

| Canonical (recommended) | Duplicate/variant also found | Fix |
|---|---|---|
| `https://allcheck.biz/contact-us/` | `https://allcheck.biz/contact-us` (no trailing slash) | 301 the non-slash version to the slash version; update any internal links pointing to the non-slash form |
| `https://allcheck.biz/radon-testing/` | `https://allcheck.biz/radon-testing` | Same — 301 non-slash → slash |
| `https://allcheck.biz/indoor-air-quality-testing/` | `https://allcheck.biz/indoor-air-quality-testing` | Same |
| `https://allcheck.biz/terms-of-service/` | `https://allcheck.biz/terms-of-service` | Same |

## Confirmed duplicate location-page URL *patterns* (same city, two different URL structures both indexed)

The site is running two different location-URL conventions simultaneously.
Pick **one** pattern and 301 the other into it — recommend the
`/complete-home-inspection/<city>-indiana/` pattern since it nests location
pages under the service, which is cleaner for topical/service-area clarity,
but confirm with whichever pattern currently holds the stronger rankings in
GSC before finalizing (see `GSC_ANALYSIS.md` — do not pick blind).

| City | Pattern A (found live) | Pattern B (found live) |
|---|---|---|
| Carmel | `/complete-home-inspection-carmel-indiana/` | `/complete-home-inspection/carmel-indiana/` |
| Central Indiana | `/complete-home-inspection-central-indiana/` | `/complete-home-inspection/central-indiana/` |
| Fishers | `/complete-home-inspection-fishers-indiana/` | `/complete-home-inspection/fishers-indiana//` **(malformed — trailing double slash, see below)** |
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
- `http://www.allcheck.biz/_information/warranty.htm` (1 backlink)
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
| contact-us / radon-testing / indoor-air-quality-testing / terms-of-service trailing-slash dupes | Waiting on Developer |
| Location-page URL pattern consolidation (Carmel/Central Indiana/Fishers/Noblesville) | Waiting on Client input (pick pattern) + Developer (implement) — see note above re: checking GSC first |
| Malformed `omplete-home-inspection` typo link | Waiting on Developer |
| Fishers double-trailing-slash | Waiting on Developer |
| 4-Point Inspection triplicate URLs | Waiting on Developer — canonical recommendation given above |
| Environmental Testing `-2` slug | Waiting on Developer (needs history check) |
| Legacy Joomla URLs with backlinks | Waiting on Developer |
| www / http variant redirects | Waiting on Developer (unverifiable from this session) |
