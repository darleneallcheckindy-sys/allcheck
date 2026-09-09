# AllCheck GSC Baseline Analysis

Property: sc-domain:allcheck.biz
Current period: Last 28 settled days
Comparison period: Previous 28 days

Goal:
Establish the current organic-search baseline before changing any page.
Identify ranking opportunities, pages to protect, CTR problems, declines,
cannibalization, and indexing issues.

## Status: Step 1 is essentially complete

You've now provided real GSC exports with full current + previous 28-day
comparison for **Countries, Devices, Pages, and Queries** (1,360 real
queries), plus **Search Appearance** and the **Coverage/Indexing report**
(Chart, Critical issues, Metadata, Noncritical issues). That covers every
major Performance and Indexing report tab. All numbers below are computed
directly from your files and cross-validated against each other (device
totals, country totals, the daily chart, and the indexing issue counts all
agree with their respective grand totals).

**One gap remains: the query + page crosstab.** You tried pulling this for
`home inspection indianapolis` and `home inspectors indianapolis` and both
came back "no data" — that's unexpected, since both queries have real
clicks/impressions in the plain Queries export, so a page must be receiving
them. Two likely causes, worth a quick recheck:
1. **Exact-match filtering.** If you filtered the query as an exact string
   match, small formatting differences (extra space, different case — GSC
   is usually case-insensitive but the filter UI can be finicky) can return
   zero rows. Try "Queries containing" instead of an exact match first, then
   narrow down.
2. **Wrong report/filter combination.** The reliable path in GSC: open
   Performance → Search results, click **+ New** → **Query** → "Exact query"
   → paste the term (or "Query contains" for a looser match) → Apply. Then,
   with that filter active, click the **Pages** tab (not Queries) — it will
   show the pages receiving impressions for that filtered query. If that
   still shows nothing, the query's data may be too sparse to show a page
   breakdown at all (GSC sometimes withholds low-volume combinations).

This isn't blocking — we have enough real signal without it. If it doesn't
work on a retry, we can proceed on the working assumption that these terms
map to the homepage (most plausible given the phrasing) and confirm later
once a redirect/schema fix is live and new data comes in.

## The single most important correction in this step

**The original third-party Digicorns audit's keyword positions do not match
real GSC data**, in both directions. This changes the protect/push decision
materially — see `PROTECT_KEYWORDS.md` for the full table, but the headline:

| Query | Audit claimed | Real GSC (current) |
|---|---:|---:|
| `home inspection indianapolis` | #1 | **6.36** |
| `allcheck` (bare) | #2 | **12.20** |
| `indianapolis home inspectors` | #9 | **3.29** |
| `home inspectors in indianapolis` | #11 | **4.64** |

**Do not carry forward the audit's "protect the #1 homepage title" guidance
as-is.** The only terms with real, confirmed, meaningful protect-level
performance are the clearly branded `allcheck inspections` (pos 1.23, 34
clicks) and `all check inspections` (pos 1.20, 26 clicks). `home inspection
indianapolis` is actually an opportunity now, not a ranking to protect from
change.

## Main 28-day vs. previous-28-day totals (real, verified)

| Metric | Current 28 Days | Previous 28 Days | Change |
|---|---:|---:|---|
| Clicks | **149** | **197** | **-48 (-24.4%)** |
| Impressions | **26,618** | **18,732** | **+7,886 (+42.1%)** |
| CTR | **0.56%** | **1.05%** | **-0.49pp (roughly halved)** |
| Avg. Position | **21.64** | **18.80** | **+2.84 (worse)** |

Verified two independent ways (Devices.csv totals and the underlying daily
Chart.csv from the first export both agree with this). No interpretation
beyond stating the pattern, per instruction — but this is worth sitting with
before Homepage Batch 1 starts: **impressions grew sharply while clicks
fell and average position got worse.** That combination usually means the
site started showing up for a much wider (and less well-matched) set of
searches without ranking well for most of them — see the "small Indiana
towns" cluster below, which is the most likely driver.

## Device performance (real, with comparison)

| Device | Clicks (curr→prev) | Impressions (curr→prev) | CTR (curr→prev) | Position (curr→prev) |
|---|---|---|---|---|
| Mobile | 78 → 105 | 2,720 → 2,931 | 2.87% → 3.58% | 9.9 → 8.41 |
| Desktop | 71 → 90 | 23,864 → 15,749 | 0.30% → 0.57% | 23.0 → 20.75 |
| Tablet | 0 → 2 | 34 → 52 | 0% → 3.85% | 7.06 → 15.54 |

Every metric moved the same direction on both Mobile and Desktop: more
impressions, fewer clicks, worse position. This confirms the sitewide
pattern above isn't a one-device fluke — it's real and broad-based.

## Country performance (real, with comparison)

United States still dominates (142 of 149 clicks, 25,480 of 26,618
impressions) — no anomaly. Philippines and a few others show small volume,
nothing worth flagging as an optimization issue, consistent with the prior
review.

## An unusual pattern worth flagging directly, not burying in a sub-file

Both `RANKING_CHANGES.md` and the query export show a large wave (dozens) of
very specific small/rural Indiana town queries — `home inspection walkerton,
in`, `radon testing south whitley, in`, `mold detection lagro, in`, `water
quality testing hartford city, in`, and many more — most brand new this
period, most at positions 10-50, virtually all at 0% CTR. This is the biggest
single contributor to the impressions-up/clicks-down pattern above.

Two honest possibilities, and I can't tell which from this data alone:
1. **Real organic demand** — Central Indiana genuinely has homeowners in a
   lot of small unincorporated communities searching these exact phrases,
   and Google is now surfacing AllCheck for them (plausibly because of
   the location pages already on the site).
2. **Something else generating this pattern** — worth asking: has anything
   changed recently around location-page generation, an SEO tool/plugin, or
   syndicated content that might auto-target long-tail town names? I have no
   way to check this from GSC data alone.

**I'm flagging this for you rather than guessing.** It doesn't need to block
Homepage Batch 1, but it's worth a direct answer before Priority 3's location
page work: is AllCheck deliberately targeting this volume of small-town
queries, or is this an unexpected side effect of something?

## Key Findings

### Protect
Real, meaningful protect-level terms: `allcheck inspections` (pos 1.23, 34
clicks) and `all check inspections` (pos 1.20, 26 clicks) — both clearly
branded, both stable. Full detail and the audit-correction table in
`PROTECT_KEYWORDS.md`. **`home inspection indianapolis` is no longer a
protect item** — see correction above.

### Quick Wins
`opportunities_4_20.csv` now has 98 real queries at position 4-20 with
meaningful impressions. Top real, commercially relevant ones:
- **`home inspectors indianapolis`** — position 4.37 (improved from 5.35),
  226 impressions, only 6 clicks (2.65% CTR). Best single opportunity in the
  dataset — near page-one top, real volume, clearly underperforming on
  clicks.
- **`home inspection indianapolis`** — position 6.36, 94 impressions, 1
  click. Given the audit-correction above, this deserves real homepage
  attention, not protection-only treatment.
- `allcheck inspections reviews` — position 4.28 (declined from 3.61), 111
  impressions, 1 click — branded/reputation term worth reinforcing.
- The Avon cluster (4 query variants, all improved 10+ positions — see
  `RANKING_CHANGES.md`) is a real, recent win worth understanding before
  editing that page.

### CTR Opportunities
Real findings in `CTR_OPPORTUNITIES.md`, split into two groups: a
"position ~1, zero clicks" anomaly cluster (`radon testing near me`,
`radon inspection near me`, `mold inspection near me`, `lead testing near
me`) that likely reflects a SERP feature (map pack/AI Overview) sitting above
the organic result rather than a title problem — and a smaller set of
genuine content/snippet candidates (`about-us/`, `home inspectors
indianapolis`, `home inspection indianapolis`, `allcheck inspections
reviews`).

### Declines
Real declines in `RANKING_CHANGES.md`. Two patterns worth naming directly:
1. `allcheck inspections reviews` slipped 3.61 → 4.28 (branded/reputation
   term, worth watching).
2. The **Greenwood cluster** — three separate Greenwood query variants all
   declined 5-7 positions in the same window. Consistent enough to be a real
   signal, not noise — check the Greenwood location page's recent history
   when it comes up in Priority 3.

### Cannibalization
Page-level findings from the prior GSC pull still stand and are now the
highest-confidence part of this analysis (see `CANNIBALIZATION.md`): the
www/non-www homepage split (position 3.71 vs. 29.95) remains the top
technical priority. Query-level cannibalization (confirming whether, e.g.,
`home inspectors indianapolis` and `home inspection indianapolis` are split
across two different pages) still needs the query+page crosstab.

### Indexing / Technical Findings
**Real Coverage data now in: 62 of ~149 known pages (42%) are not indexed**,
with over half of those (33) due to Google crawling them and choosing not to
index them — usually a thin/duplicate-content signal. This is now a
headline technical finding, not a minor note — see `INDEXING_ISSUES.md` for
the full breakdown. Combined with the www/non-www split (still the top
priority) and the confirmed lack of working canonical tags on most duplicate
URL pairs (only 3 pages show a working canonical relationship, far fewer
than the number of duplicate pairs on the site), this points at one root
cause worth stating plainly: **AllCheck likely has more duplicate/near-
duplicate URLs live than previously visible, and Google is responding by
simply not indexing the weaker copies rather than merging their signal.**
Fixing the URL consolidation in `TECHNICAL_URL_CLEANUP.md` should directly
improve this indexing number, not just clean up appearances.

### Recommended Page Order

Updated given the real data:

1. **Homepage www/non-www technical fix** (still first — this is now doubly
   justified: both the page-level split and the corrected query positions
   suggest ranking signal and click potential are currently being lost)
2. Homepage content/AEO/GEO batch — now with a real, corrected keyword
   target set: push `home inspectors indianapolis` and `home inspection
   indianapolis` (both genuine opportunities, not protect-only), reinforce
   `allcheck inspections` / `all check inspections` (real protect terms)
3. Complete Home Inspection (after resolving its own 3-way URL split)
4. Environmental Testing (after resolving its 2-way URL split)
5. Radon Testing — note the "near me" anomaly cluster above touches this
   page's query set; investigate before assuming a content fix is needed
6. Termite Inspection
7. 4-Point Inspection (after URL consolidation)
8. New Construction Phased Inspection
9. End of Builder's Warranty / 11-Month Warranty
10. **Avon and Greenwood location pages** — moved up in priority relative to
    other locations given the real, opposite-direction signals found this
    step (Avon improving fast, Greenwood declining) — both deserve a look
    before the others

## Stop point

Per instruction, stopping here — no homepage edits made. Still outstanding
before Homepage Batch 1 is fully locked in: the query+page crosstab export
(to confirm exact page attribution for the top opportunity terms), and your
read on the small-town query pattern above. Also — you mentioned another
attachment is coming; let me know what it is once you're able to send it and
I'll fold it in.
