# CTR Opportunities

Status: **Real page-level findings below**, from your `Pages.csv` export.
Query-level CTR analysis (matching CTR against expected CTR for a specific
query's actual position) still needs the Queries export — a page's overall
average position blends every query it ranks for, so these are directional,
not definitive, findings. Per the original instruction, CTR is compared
against position first — not assumed to be a title problem by default.

## Highest-priority finding: not a title problem, a canonicalization problem

**`http://www.allcheck.biz/`** — average position **3.71** (excellent — top
of page one), but only **2.49% CTR** on 2,487 impressions. At a genuine
position of 3-4, typical CTR benchmarks run well above 10%. This looks like a
severe underperformance — but the far more likely explanation is the
www/non-www split confirmed in `CANNIBALIZATION.md`: this URL is not even the
canonical one, so **do not rewrite the homepage title/meta based on this
number.** Fix the redirect first (`TECHNICAL_URL_CLEANUP.md`), then re-pull
GSC data in a few weeks to see the corrected picture before touching any
copy.

## Genuine content/snippet candidates (position is good, cause is not an obvious technical artifact)

| Page | Position | Impressions | Clicks | CTR | Read |
|---|---:|---:|---:|---|---|
| `https://allcheck.biz/about-us/` | 5.29 | 528 | 6 | 1.14% | Strong position, weak CTR. Worth revisiting the title/meta once the E-E-A-T content upgrade (Priority 3, `MASTER_TODO.md`) is done — a generic "About Us" title/snippet at position 5 is a plausible, ordinary CTR problem, not a technical artifact. |
| `https://allcheck.biz/agents/` | 10.01 | 552 | 0 | 0% | Right at the page-one/two boundary with meaningful impressions and zero clicks. Worth a title/meta look once this page is in a batch. |
| `https://allcheck.biz/avon-indiana/` | 11.38 | 1,047 | 1 | 0.1% | Meaningful impression volume, borderline page-one position, essentially no clicks. Candidate for the location-page batch (Priority 3). |

## Likely position problems, not CTR problems (do not prioritize a title rewrite here)

These pages show 0% CTR but their average position is deep enough (20+) that
low CTR is the expected outcome of poor visibility, not a snippet issue:
`radon-testing/` (23.99), `mold-and-mildew-testing/` (35.92),
`services/complete-home-inspection/` (37.17), `water-testing/` (40.19),
`termite-inspection/` (33.98). These need ranking improvement (content depth,
internal links, schema — per their eventual page batches), not a meta
description edit.

## What still needs the Queries export

- Confirming whether `about-us`, `agents`, and `avon-indiana`'s weak CTR is
  concentrated on one or two specific high-value queries (worth a targeted
  title fix) or spread thinly across many low-value queries (not worth
  prioritizing).
- The full "impressions are meaningful + position is good + clicks are
  disproportionately low" scan really wants query-level data, since a page's
  blended average position can hide a query ranking #2 and another ranking
  #40 averaging out to a misleading-looking #20.

## Action needed

- [ ] **Waiting on Developer:** fix the www→non-www 301 before evaluating
      homepage CTR further.
- [ ] **Waiting on Client:** Queries export to sharpen the about-us/agents/
      avon-indiana findings above.
