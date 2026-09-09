# CTR Opportunities

Status: **Done — real query-level GSC data.** Per instruction, CTR is
compared against position first, not assumed to be a title problem by
default.

## Anomaly cluster: position ~1.0, meaningful impressions, ZERO clicks

This is the most unusual pattern in the dataset and needs investigation
before any title/meta work, not after:

| Query | Position | Impressions | Clicks | Prev. period impressions |
|---|---:|---:|---:|---:|
| radon testing near me | 1.00 | 273 | 0 | 0 (new) |
| radon inspection near me | 1.00 | 146 | 0 | 0 (new) |
| mold inspection near me | 1.00 | 91 | 0 | 5 |
| lead testing near me | 1.00 | 71 | 0 | 99 |
| pre purchase inspection | 1.68 | 25 | 0 | 27 (prev. pos 1.37) |

A page truly averaging position 1 with hundreds of impressions and
**literally zero clicks** is not typical organic behavior — at true position
1, CTR is normally 20-30%+. The most likely explanations, in order of
probability:
1. These queries are triggering a non-organic SERP feature (local pack /
   map pack, or an AI Overview) that shows above the organic result AllCheck
   holds — Google can still report an organic "position 1" in this table
   while the actual click goes to the map pack or the AI Overview instead.
2. These are very new queries (three of the five have 0 impressions the
   prior period) and Google may still be testing/fluctuating this ranking
   before it stabilizes.

**Recommend:** do not "fix" this with a title rewrite — a title change
can't out-compete a map pack or AI Overview sitting above it. Worth a manual
search from an Indianapolis-area IP/location for "radon testing near me" to
see what's actually outranking the organic click, once someone can do that
check outside this session (this session has no browser access to Google
search results).

## Genuine content/snippet CTR opportunities (real, not artifacts)

| Page/Query context | Position | Impressions | Clicks | CTR | Read |
|---|---:|---:|---:|---|---|
| Page: `http://www.allcheck.biz/` | 3.71 | 2,487 | 62 | 2.49% | Still likely a canonicalization artifact (see `CANNIBALIZATION.md`), not a pure title issue — fix the redirect first. |
| Page: `https://allcheck.biz/about-us/` | 5.29 | 528 | 6 | 1.14% | Real candidate — good position, weak CTR, not explained by a SERP-feature pattern like the anomaly cluster above. Revisit title/meta once E-E-A-T content lands (Priority 3). |
| Query: `home inspectors indianapolis` | 4.37 | 226 | 6 | 2.65% | Position improved (5.35→4.37) but CTR (2.65%) is well below typical page-one-top expectations (~8-15%). Strong candidate once we know which page ranks for it (needs crosstab). |
| Query: `home inspection indianapolis` | 6.36 | 94 | 1 | 1.06% | Weak CTR even for position 6; combined with the position correction in `PROTECT_KEYWORDS.md`, this term deserves real attention in Homepage Batch 1, not protection-only treatment. |
| Query: `allcheck inspections reviews` | 4.28 | 111 | 1 | 0.90% | Declined from 3.61; also weak CTR for a near-page-one-top branded/reputation term. |

## Position-driven, not CTR-driven (do not prioritize a title rewrite)

The large cluster of small-Indiana-town queries (`home inspection walkerton,
in`, `radon testing south whitley, in`, etc. — dozens of these, see
`opportunities_4_20.csv` and `RANKING_CHANGES.md`) mostly sit at positions
10-50 with 0% CTR. That's expected at those positions — the fix there is
ranking improvement (content, internal links, possibly dedicated pages),
not a snippet rewrite. See the note in `STEP_1_GSC_BASELINE.md` about this
whole cluster — it's unusual enough as a pattern to flag for you directly
before assuming it's simply "more content to write."

## What still needs the query+page crosstab

Confirming which exact URL ranks for `home inspectors indianapolis`,
`home inspection indianapolis`, and `allcheck inspections reviews` — a
page's title can't be fixed if we don't know which page it is.

## Action needed

- [ ] **Waiting on Developer:** fix the www→non-www 301 before evaluating
      homepage CTR further (unchanged from before).
- [ ] **Waiting on Client:** manual SERP check for "radon testing near me"
      and "radon inspection near me" to see what's outranking/covering the
      organic #1 spot (map pack, AI Overview, etc.) — this session has no
      browser access to check live Google search results.
- [ ] **Waiting on Client:** query+page crosstab export.
