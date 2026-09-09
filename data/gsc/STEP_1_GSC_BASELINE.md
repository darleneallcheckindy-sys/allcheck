# AllCheck GSC Baseline Analysis

Property: sc-domain:allcheck.biz
Current period: Last 28 settled days
Comparison period: Previous 28 days

Goal:
Establish the current organic-search baseline before changing any page.
Identify ranking opportunities, pages to protect, CTR problems, declines,
cannibalization, and indexing issues.

## Status: Partially unblocked — real GSC data received, two exports still missing

You provided five real GSC exports (`Chart.csv`, `Countries.csv`,
`Devices.csv`, `Filters.csv`, `Pages.csv`) for the current 28-day period.
These are used below and are treated as ground truth. I cross-validated them
against each other before using them: total clicks (149) and total
impressions (26,618) computed from the daily `Chart.csv` breakdown match the
`Devices.csv` totals exactly, and are consistent with `Countries.csv`. Where
that's true, I'm confident these numbers are accurate.

**Still missing — needed before Step 1 can be fully completed:**

1. **The Queries table export** (Query, Clicks, Impressions, CTR, Position).
   You sent Chart, Countries, Devices, Filters, and Pages — Queries was not
   among them. **This is the single most important missing file** — without
   it, `top_queries_28d.csv`, `PROTECT_KEYWORDS.md`, and
   `opportunities_4_20.csv` (the three files you specifically said you need
   to make the protect/push decision) cannot contain real query-level data.
   How to get it: in Search Console → Performance → Search results, the
   report defaults to the **Queries** tab. Click **Export** (top right) →
   Download CSV, the same way you did for Pages. Do this with no more than
   the default filters applied so it covers all queries, not a filtered
   subset.
2. **A previous-28-day comparison.** `Filters.csv` shows only "Last 28 days"
   with no comparison enabled. To get this: in the same Performance report,
   click the date-range control → **Compare** → "Compare last 28 days to
   previous period" → Apply, then re-export Queries and Pages. That single
   export will include current + previous + change columns for both, which
   is more useful than a second one-off pull.

Everything below uses only real numbers where they exist. Nothing is
invented — per `CLAUDE.md`, any field still needing the Queries export or the
comparison period is marked accordingly rather than guessed.

## Main 28-day vs. previous-28-day totals

| Metric | Current 28 Days | Previous 28 Days | Change |
|---|---|---|---|
| Clicks | **149** | PENDING (needs Compare export) | PENDING |
| Impressions | **26,618** | PENDING | PENDING |
| CTR | **0.56%** | PENDING | PENDING |
| Avg. Position | **~21.6** (impression-weighted, see note) | PENDING | PENDING |

Note on Avg. Position: GSC's own reported daily positions in `Chart.csv` and
device-level positions in `Devices.csv` were both used to independently
compute an impression-weighted average, and they agree (21.64 vs 21.64) —
so this figure is solid math on real numbers, not a guess. It is a sitewide
average across all queries and devices, and is heavily pulled down by a large
volume of low-ranking non-branded impressions (see Devices section below) —
it is not representative of how AllCheck's protected branded terms are
performing.

No further interpretation attempted on totals alone, per instruction.

## Device performance (real data, from `Devices.csv`)

| Device | Clicks | Impressions | CTR | Avg. Position |
|---|---:|---:|---|---:|
| Mobile | 78 | 2,720 | 2.87% | 9.9 |
| Desktop | 71 | 23,864 | 0.30% | 23.0 |
| Tablet | 0 | 34 | 0% | 7.06 |

**This is a real, notable finding.** Mobile carries far fewer impressions
(2,720 vs. 23,864) but a dramatically better average position (9.9 vs 23.0)
and 9.5x better CTR (2.87% vs 0.30%). Desktop dominates impression volume but
converts those impressions into clicks far worse. This needs investigation
during homepage/service-page QA — it may mean desktop is picking up a much
larger volume of poorly-matched, low-intent long-tail impressions that mobile
isn't seeing, or it may mean the desktop rendering itself underperforms.
Flagging for QA per the original Step 1 instructions rather than diagnosing
further without query-level data.

## Country performance (real data, from `Countries.csv`)

United States dominates as expected for a local Indianapolis business: 142 of
149 total clicks (95%) and 25,480 of 26,618 impressions (96%) are U.S. No
single non-U.S. country shows a meaningful click or impression volume worth
flagging as an anomaly (the next-largest, Philippines, is 4 clicks / 79
impressions). **No action needed here** — this checks out clean.

## Files produced/updated in this step

| File | Status |
|---|---|
| `top_queries_28d.csv` | **Still blocked** — no Queries export received; scaffold only |
| `top_pages_28d.csv` | **Done with real data** — full `Pages.csv` export (73 pages) incorporated |
| `PROTECT_KEYWORDS.md` | **Still blocked at query level** — no query data to confirm which queries to protect; page-level hint noted |
| `opportunities_4_20.csv` | **Still blocked at query level** — page-level 4–20-position candidates noted as hints, not confirmed opportunities |
| `CTR_OPPORTUNITIES.md` | **Done with real page-level data** — several genuine CTR opportunities identified from `Pages.csv` |
| `RANKING_CHANGES.md` | **Still blocked** — no previous-period export received |
| `CANNIBALIZATION.md` | **Upgraded to real, GSC-confirmed findings** — see below, this is now a serious, confirmed technical issue, not just a crawl hypothesis |
| `INDEXING_ISSUES.md` | Updated with the GSC-confirmed www/non-www split |

## Key Findings

### Protect
Cannot be finalized without query-level data — position 1–3 status is a
per-query fact, not a per-page fact. What we can say from the real page data:
- The homepage as tracked under `https://allcheck.biz/` (the correct
  canonical URL) has a **poor average position of 29.95** across 8,719
  impressions — this is concerning and cuts against the audit's claim of a
  #1 branded ranking, *unless* that #1 branded ranking is being attributed to
  the separate `http://www.allcheck.biz/` entry instead (see Cannibalization
  below, which is now the leading explanation).
- The `http://www.allcheck.biz/` entry — a non-canonical URL variant — shows
  a strong average position of **3.71** across 2,487 impressions. This is
  very likely where AllCheck's genuinely strong branded terms
  (`allcheck`, `allcheck inspections`, etc.) are currently being counted,
  because of the www/non-www split described below.
- **Until the Queries export exists, do not assume the previously-cited
  "#1 for home inspection indianapolis" is safe** — it's plausible that
  ranking signal is currently split across two URLs GSC treats as different
  pages, which is a real risk to that ranking, not just a reporting quirk.

### Quick Wins
Cannot be confirmed at the query level yet. Page-level candidates worth
watching once query data exists (meaningful impressions, page-one-adjacent
average position, essentially no clicks):
- `https://allcheck.biz/complete-home-inspection-carmel-indiana/` — 3,326
  impressions, position 13.6, only 1 click (0.03% CTR)
- `https://allcheck.biz/complete-home-inspection-fishers-indiana/` — 2,708
  impressions, position 13.58, 4 clicks (0.15% CTR)
- `https://allcheck.biz/complete-home-inspection-noblesville-indiana/` —
  1,526 impressions, position 14.44, 0 clicks
- `https://allcheck.biz/complete-home-inspection-central-indiana/` — 684
  impressions, position 12.19, 0 clicks
- `https://allcheck.biz/complete-home-inspection-greenwood-indiana/` — 481
  impressions, position 13.09, 3 clicks
- `https://allcheck.biz/pricing/` — 827 impressions, position 12.51, 9 clicks

These location pages collectively pull real impression volume (~8,700
impressions total) at page-two-adjacent positions with almost no clicks —
strong candidates for the "quickest page-two opportunities" category once we
can see which exact queries are driving them.

### CTR Opportunities
Real findings this time — see `CTR_OPPORTUNITIES.md` for full detail. Top
two:
1. **`http://www.allcheck.biz/`** — position 3.71 (excellent) but only
   2.49% CTR. At a true position ~3-4, expected CTR is typically well above
   10%. This is the single biggest red flag in the whole dataset — but the
   likely cause is the www/non-www split (see Cannibalization), not a title
   problem. Do not rewrite the title based on this number alone.
2. **`https://allcheck.biz/about-us/`** — position 5.29 (very good), only
   1.14% CTR. This one looks like a genuine title/snippet issue worth
   revisiting once E-E-A-T content is added (already planned per
   `MASTER_TODO.md` Priority 3), not a canonicalization artifact.

### Declines
Cannot be identified — no previous-period export received. See
`RANKING_CHANGES.md`.

### Cannibalization
**Upgraded from hypothesis to GSC-confirmed finding.** `Pages.csv` shows real
duplicate-URL pairs both actively receiving impressions:

- **Homepage:** `http://www.allcheck.biz/` (2,487 impr, position 3.71) vs.
  `https://allcheck.biz/` (8,719 impr, position 29.95) — same page, two GSC
  identities, wildly different reported performance. This is now the
  **highest-priority technical fix** on the whole site — see
  `CANNIBALIZATION.md` and `TECHNICAL_URL_CLEANUP.md`.
- **Contact page:** `https://allcheck.biz/contact-us/` (712 impr) vs.
  `https://www.allcheck.biz/contact-us` (219 impr) — same split pattern.
- **Complete Home Inspection (core service, non-location):** three separate
  URLs all receiving impressions — `https://allcheck.biz/complete-home-inspection/`
  (114 impr), `https://allcheck.biz/services/complete-home-inspection/`
  (781 impr), and `https://allcheck.biz/wiki/complete-home-inspection/`
  (77 impr). This is a new finding not visible in the original audit crawl.
- **Environmental Testing:** `https://allcheck.biz/environmental-testing/`
  (46 impr) vs. `https://allcheck.biz/services/environmental-testing-2/`
  (9 impr) — confirms the `-2` slug is a live duplicate, not just an orphaned
  page.

Per the rule, none of these are being consolidated yet — flagged only. Full
detail in `CANNIBALIZATION.md`.

### Indexing / Technical Findings
- The www/non-www split above is a Coverage/canonicalization problem, not
  just an internal-linking one — Google is actively serving impressions
  under the wrong host variant. This should move to the top of the
  `TECHNICAL_URL_CLEANUP.md` priority list.
- Sitemap, robots.txt, and canonical-tag facts from the original audit crawl
  still stand (see `INDEXING_ISSUES.md`) — no GSC Coverage report was
  provided, so indexed/excluded counts are still pending.

### Recommended Page Order

Still provisional — real page-level data changes the picture somewhat
(the location pages are carrying more real impression volume than expected,
and the homepage's own ranking health is now in question pending the www fix)
but query-level confirmation is needed before finalizing:

1. **Homepage www/non-www consolidation (technical fix, not a content
   batch)** — this should happen before or alongside Homepage Batch 1, since
   it may be actively suppressing the homepage's real performance
2. Homepage (content/AEO/GEO batch, as previously scoped)
3. Complete Home Inspection (also needs the 3-way URL consolidation above
   resolved first)
4. Environmental Testing (also needs the 2-way URL consolidation resolved
   first)
5. Radon Testing
6. Termite Inspection
7. 4-Point Inspection (after URL consolidation)
8. New Construction Phased Inspection
9. End of Builder's Warranty / 11-Month Warranty

## Stop point

Per instruction, stopping here. No homepage edits have been made. Before
Homepage Batch 1 can be approved with confidence, I still need:
- The **Queries** export (current period)
- The **Compare: previous period** export (Queries + Pages)

Once those two arrive, `top_queries_28d.csv`, `PROTECT_KEYWORDS.md`,
`opportunities_4_20.csv`, and `RANKING_CHANGES.md` can be completed with real
numbers, and the www/non-www finding above can be confirmed as query-level
cannibalization rather than a page-level pattern.
