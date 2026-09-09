# AllCheck GSC Baseline Analysis

Property: sc-domain:allcheck.biz
Current period: Last 28 settled days
Comparison period: Previous 28 days

Goal:
Establish the current organic-search baseline before changing any page.
Identify ranking opportunities, pages to protect, CTR problems, declines,
cannibalization, and indexing issues.

## Status: BLOCKED on live GSC data — read this first

This session has **no way to pull live Google Search Console data**:

1. No Search Console MCP/connector is attached to this Claude workspace
   (checked via `ListConnectors` — only Google Drive is connected).
2. No GSC export (CSV, Sheet, or otherwise) exists in the connected Google
   Drive. I searched Drive directly and reviewed every AllCheck-related file
   there, including **"AllCheck SEO AEO GEO Internal Progress Tracker"**
   (your own working tracker) and **"AllCheck Dashboard."**
3. Your own tracker confirms this independently: it lists "Verify Google
   Search Console property connection" as **Done** ("Connected as
   sc-domain:allcheck.biz"), but the very next row, "Complete 28-day vs
   previous 28-day GSC analysis," is marked **Not Started** with the note
   "Live GSC pending." Every GSC-dependent row after it (opportunity
   keywords, CTR opportunities, ranking health) is also **Not Started**.

So this isn't just a this-session limitation — the live pull hasn't happened
anywhere yet. Per `CLAUDE.md` ("Do not invent scores, credentials, awards,
addresses, or rankings. Verify before publishing"), I have **not** fabricated
clicks, impressions, or CTR numbers anywhere in this file set. Every field
that requires real GSC data is marked `PENDING` / "Needs Live GSC Export."

**To unblock this step, one of the following is needed:**
- Attach a Search Console connector/MCP to this Claude Code workspace with
  access to `sc-domain:allcheck.biz`, or
- Export the GSC Performance report yourself (Search results → last 28 days
  vs. previous 28 days, split by Query, Page, Device, Country) and the
  Coverage/Sitemaps report, and share the export files/CSVs here.

Everything below is either (a) a scaffold ready to receive real data in the
exact shape you asked for, or (b) built from data that genuinely is
verifiable right now — the third-party Digicorns audit's crawl of the live
site (URLs, schema, headings, backlinks) and your own Drive tracker. Those
two sources are cited inline wherever used, and are never GSC substitutes.

## Main 28-day vs. previous-28-day totals

| Metric | Current 28 Days | Previous 28 Days | Change |
|---|---|---|---|
| Clicks | PENDING | PENDING | PENDING |
| Impressions | PENDING | PENDING | PENDING |
| CTR | PENDING | PENDING | PENDING |
| Avg. Position | PENDING | PENDING | PENDING |

No interpretation attempted, per instruction — these four numbers need a
real GSC pull before anything else in this step can be finalized.

## Files produced in this step

| File | Status |
|---|---|
| `top_queries_28d.csv` | Scaffolded with 10 known query terms (audit-sourced, not GSC); needs full top-100 GSC export |
| `top_pages_28d.csv` | Scaffolded with known site URLs; needs full top-100 GSC export |
| `PROTECT_KEYWORDS.md` | Positions confirmed via audit + your own tracker; clicks/impressions pending GSC |
| `opportunities_4_20.csv` | 2 known position 4–20 queries (audit-sourced); needs GSC to find the rest |
| `CTR_OPPORTUNITIES.md` | Blocked — needs GSC |
| `RANKING_CHANGES.md` | Blocked — needs GSC (requires two time-boxed exports to compare) |
| `CANNIBALIZATION.md` | Partially done — real duplicate-URL structural candidates flagged from the site crawl; GSC needed to confirm actual query-level overlap |
| `INDEXING_ISSUES.md` | Partially done — sitemap/robots/canonical facts confirmed from crawl; GSC Coverage report needed for the rest |

## Key Findings

### Protect
- `home inspection indianapolis` — position 1 (audit-sourced; ~720/mo
  searches, ~219 est. traffic). Do not rewrite title/H1/opening copy without
  GSC evidence it's needed.
- `all check inspections` / `allcheck inspections` — position 1 (branded)
- `allcheck` — position 2 (branded)
- `allcheck inspections reviews` — position 3 (branded/reputation)
- Full list will expand once the real top-100 query export exists — the
  audit only sampled 10 queries total, so there are almost certainly more
  positions 1–3 terms not yet visible to us. See `PROTECT_KEYWORDS.md`.

### Quick Wins
- **`home inspectors in indianapolis` — position 11.** Same ~720/mo search
  volume as the #1-ranking term. Highest-confidence opportunity identified so
  far: one word-order variant away from a term AllCheck already owns.
- `indianapolis home inspectors` — position 9, same phrase family.
- Both currently attributed to the homepage per the audit, but this needs
  GSC page-attribution to confirm before we treat it as settled — see
  `opportunities_4_20.csv` and the Cannibalization section below.
- The real positions-4–20 list (audit only sampled a handful of queries) is
  pending the full GSC export.

### CTR Opportunities
- Cannot be identified without real GSC data. See `CTR_OPPORTUNITIES.md`.

### Declines
- Cannot be identified without a real current-vs-previous GSC comparison.
  See `RANKING_CHANGES.md`.

### Cannibalization
- Not yet confirmed at the query level (needs GSC), but the site's own crawl
  independently shows **structural** duplication that is a strong precondition
  for cannibalization:
  - Two live URL patterns per city for Carmel, Central Indiana, Fishers, and
    Noblesville "complete home inspection" pages
  - Three live URLs for 4-Point Inspection
  - See `CANNIBALIZATION.md` and `TECHNICAL_URL_CLEANUP.md` for full detail.

### Indexing / Technical Findings
- Sitemap (`sitemap.xml`, `sitemap.rss`) and `robots.txt` both present and
  not blocking search engines or AI crawlers — confirmed via audit crawl.
- No noindex tag/header on the homepage; canonical tag correctly set.
- Duplicate/malformed URL variants confirmed structurally (see
  `INDEXING_ISSUES.md`); actual GSC Coverage status of each still pending.

### Recommended Page Order

This cannot be finalized with confidence until live GSC page-level data
exists — a page order built only on the third-party audit's homepage-focused
sample risks missing where the real opportunity actually sits. Provisional
order, unchanged from the existing task files, pending your review:

1. Homepage
2. Complete Home Inspection
3. Environmental Testing
4. Radon Testing
5. Termite Inspection
6. 4-Point Inspection (after URL consolidation)
7. New Construction Phased Inspection
8. End of Builder's Warranty / 11-Month Warranty

## Stop point

Per instruction, stopping here. No homepage edits have been made or will be
made until you've reviewed `STEP_1_GSC_BASELINE.md`, `top_queries_28d.csv`,
`top_pages_28d.csv`, and `opportunities_4_20.csv`, and confirmed which
homepage keywords to protect, which to push, and whether the title/meta
should be touched at all — especially since all of that currently rests on a
third-party audit sample, not a real GSC export.
