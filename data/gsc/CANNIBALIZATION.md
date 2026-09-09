# Cannibalization Check

Status: **Real, GSC-confirmed page-level findings below** (from your real
`Pages.csv` export), now with real query data too. The Queries export
confirms `home inspectors indianapolis`, `home inspection indianapolis`, and
`allcheck inspections reviews` are all real, meaningful queries in their own
right (see `PROTECT_KEYWORDS.md`, `opportunities_4_20.csv`) — but a plain
Queries export reports totals across *all* pages combined for each query, so
it cannot by itself confirm whether one URL or several are splitting that
query's impressions. That still needs a query+page crosstab export (see
`STEP_1_GSC_BASELINE.md`). Do not consolidate any pages yet, per the rule
below — this file only flags.

## Confirmed page-level duplicates (both sides actively receiving impressions in GSC)

| Query/Page pair | Page 1 | Page 2 | Issue | Recommended Primary Page |
|---|---|---|---|---|
| Homepage | `http://www.allcheck.biz/` — 2,487 impr, 62 clicks, **position 3.71** | `https://allcheck.biz/` — 8,719 impr, 59 clicks, **position 29.95** | Same page, split across the www and non-www host. The www variant has a dramatically better average position, strongly suggesting AllCheck's strongest branded queries are currently attributed to the *wrong* (non-canonical) URL. This is the single highest-priority technical fix identified in Step 1 — see below. | `https://allcheck.biz/` (matches the declared canonical tag) — but the fix is a 301 from www→non-www, not a content change |
| Contact page | `https://allcheck.biz/contact-us/` — 712 impr | `https://www.allcheck.biz/contact-us` — 219 impr | Same www-split pattern as the homepage, confirming this is a sitewide redirect issue, not a homepage-only quirk. | `https://allcheck.biz/contact-us/` |
| Complete Home Inspection (core service page, non-location) | `https://allcheck.biz/complete-home-inspection/` — 114 impr, position 41.37 | `https://allcheck.biz/services/complete-home-inspection/` — 781 impr, position 37.17 | **New finding, not in the original site crawl.** A third URL also exists and is receiving impressions: `https://allcheck.biz/wiki/complete-home-inspection/` — 77 impr, position 16.64 (notably the *best*-positioned of the three). Three separate URLs all carrying some signal for the same core service. | Needs Queries export to know which URL is capturing which query before choosing — do not assume `/services/complete-home-inspection/` is the winner just because it matches the sitewide URL pattern; the wiki page's better position is worth investigating first |
| Environmental Testing | `https://allcheck.biz/environmental-testing/` — 46 impr, position 39.37 | `https://allcheck.biz/services/environmental-testing-2/` — 9 impr, position 63.44 | Confirms the `-2` slug (flagged as suspicious in `TECHNICAL_URL_CLEANUP.md`) is a live, indexed duplicate actively splitting weak signal even further, not just an orphaned/trashed page. | `https://allcheck.biz/environmental-testing/` currently holds more impressions and a much better position — recommend this as primary pending Queries confirmation, opposite of the original crawl-based guess |

## Structural duplicates seen in the original audit crawl, NOT confirmed as live cannibalization by this GSC export

These city-page URL pattern pairs were flagged in `TECHNICAL_URL_CLEANUP.md`
from the original site crawl, but this `Pages.csv` export shows **only one**
pattern per city actually receiving GSC impressions — the alternate pattern
doesn't appear in the export at all, meaning it likely isn't indexed or is
getting effectively zero impressions right now:

| City | Pattern with real GSC impressions | Alternate pattern (crawl-only, 0 GSC data seen) |
|---|---|---|
| Carmel | `/complete-home-inspection-carmel-indiana/` — 3,326 impr, position 13.6 | `/complete-home-inspection/carmel-indiana/` — not in this export |
| Fishers | `/complete-home-inspection-fishers-indiana/` — 2,708 impr, position 13.58 | `/complete-home-inspection/fishers-indiana//` (malformed) — not in this export |
| Noblesville | `/complete-home-inspection-noblesville-indiana/` — 1,526 impr, position 14.44 | `/complete-home-inspection/noblesville-indiana/` — not in this export |
| Central Indiana | `/complete-home-inspection-central-indiana/` — 684 impr, position 12.19 | `/complete-home-inspection/central-indiana/` — not in this export |

This is good news for these four — the risk is lower than originally flagged,
since only one URL per city appears to be carrying live search signal right
now. Still recommend the developer confirm the alternate URLs 404 or already
redirect (per `TECHNICAL_URL_CLEANUP.md`), just not as urgently as the
homepage www/non-www issue.

## 4-Point Inspection — real data update

Only `https://allcheck.biz/4-point-inspection/` (the bare, legacy-style path)
appears in this export — 8 impressions, position 55.38. Neither
`/service/4-point-inspection/` nor `/services/4-point-inspection/` shows any
GSC signal in this period. Position 55 is poor regardless of which URL wins,
so this stays a technical consolidation task (per `TECHNICAL_URL_CLEANUP.md`)
rather than an urgent ranking-protection issue.

## Rule for this step

Do not consolidate any of the above pages yet. This file only flags.
Consolidation (canonical + 301) decisions happen in
`TECHNICAL_URL_CLEANUP.md` and should wait for the Queries export to confirm
exactly which URL should keep which query's ranking signal before anything
is redirected — especially for the Complete Home Inspection three-way split
and the Environmental Testing pair, where the "obvious" URL (matching the
sitewide `/services/` pattern) is not necessarily the one actually holding
the better position.

## Action needed

- [ ] **Waiting on Client:** the Queries export, to confirm which exact
      search terms are split across each pair above — this converts these
      page-level findings into confirmed query-level cannibalization.
- [x] Homepage www/non-www split — confirmed via real GSC page data. Escalate
      to top priority in `TECHNICAL_URL_CLEANUP.md`; do not wait for the
      Queries export to start planning this fix, since it's already
      unambiguous at the page level.
