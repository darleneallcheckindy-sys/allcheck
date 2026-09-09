# Ranking Changes — Current 28 Days vs. Previous 28 Days

Status: **Done — real GSC comparison data received.** Filtered to
"meaningful" rows (≥15 impressions in whichever period is being measured) to
exclude single-impression noise. Full underlying numbers are in
`top_queries_28d.csv` and `opportunities_4_20.csv`.

## Sitewide totals (see `STEP_1_GSC_BASELINE.md` for full detail)

Clicks fell 149 vs. 197 previous (-24%) while impressions rose 26,618 vs.
18,732 previous (+42%) and average position got measurably worse (21.6 vs.
18.8 previous). **More visibility, worse average placement, fewer clicks —
that's the real sitewide story of this comparison window**, and it's worth
treating as the headline finding of Step 1, not a footnote.

## Declined — commercially relevant, real signal (not noise)

| Query | Previous Position | Current Position | Impressions (prev→curr) |
|---|---:|---:|---|
| allcheck inspections reviews | 3.61 | 4.28 | 93 → 111 |
| allcheck property inspections | 7.25 | 13.37 | 20 → 19 |
| home inspection greenwood in | 16.94 | 23.86 | 62 → 58 |
| home inspections greenwood in | 17.97 | 24.18 | 59 → 61 |
| home inspector greenwood in | 17.70 | 23.49 | 63 → 59 |
| home inspection indianapolis | 7.14 | 6.36 | *(improved, listed for context — see correction in PROTECT_KEYWORDS.md)* |

The Greenwood cluster is worth a second look together — three related
Greenwood queries all declined by 5-7 positions in the same window. That's
consistent enough across three variants of the same city+intent to be a real
pattern (e.g., something changed on the Greenwood page, or a competitor
moved), not coincidence. Recommend checking `complete-home-inspection-greenwood-indiana/`
specifically when that page comes up in a batch.

## Improved — real gains worth protecting going forward

| Query | Previous Position | Current Position | Impressions (prev→curr) |
|---|---:|---:|---|
| home inspection avon, in | 20.18 | 9.45 | 22 → 146 |
| home inspectors avon in | 17.44 | 10.46 | 18 → 72 |
| home inspector avon in | 21.21 | 10.53 | 24 → 75 |
| home inspection avon in | 21.78 | 9.78 | 51 → 74 |
| indianapolis home inspectors | 6.76 | 3.29 | 25 → 24 |
| home inspectors indianapolis | 5.35 | 4.37 | 286 → 226 |

**The Avon cluster is the clearest real win in the whole dataset** — four
different Avon-area query variants all jumped roughly 10+ positions in the
same window, with impressions climbing sharply too (22→146 on the top one).
Something is working for Avon specifically right now. Worth understanding
what changed there before touching that page in a way that could undo it —
check `avon-indiana/` page history/edits if any were made recently.

## Newly ranking (0 impressions previous period → meaningful now)

46 queries newly appeared this period with ≥15 impressions. Two patterns
stand out:
1. The `radon testing near me` / `radon inspection near me` anomaly cluster
   (see `CTR_OPPORTUNITIES.md`) — brand new, position ~1, zero clicks.
2. A wave of very small/rural Indiana town names newly appearing
   (`home inspections avon, in`, `home inspection spiceland, in`,
   `home inspection roann, in`, `home inspector warsaw, in`, `home inspector
   walkerton, in`, `home inspectors atlanta, in`, several `water quality
   testing <small town>, in` queries) — see the note in
   `STEP_1_GSC_BASELINE.md` about this cluster; it's unusual enough in volume
   and specificity to flag for you directly rather than assume it's simply
   organic long-tail growth.

## Lost (meaningful previous impressions → 0 now)

| Query | Previous Position | Previous Impressions |
|---|---:|---:|
| power pro genius reviews | 3.03 | 69 |
| stopwatt reviews | 3.00 | 40 |
| digital inspections | 1.00 | 23 |
| radon testing blocher, in | 29.28 | 18 |
| home inspections fredericksburg, in | 38.50 | 16 |
| radon testing campbellsburg, in | 42.94 | 16 |
| radon testing clifford, in | 35.07 | 15 |
| complete home inspectors fond du lac | 54.47 | 15 |

The first three ("power pro genius reviews," "stopwatt reviews," "digital
inspections") are **not obviously related to AllCheck's actual services** —
these look like they may have been mismatched/irrelevant impressions in the
prior period rather than a real loss worth chasing. Not flagging these as a
concern. The rest are low-value, low-position long-tail losses — not
significant.

## Action needed

- [ ] Investigate the Greenwood decline cluster when that location page
      comes up in Priority 3.
- [ ] Understand what changed for the Avon page/cluster before editing it,
      so we don't accidentally undo a real gain.
- [ ] Manual SERP check on the "near me" anomaly cluster (see
      `CTR_OPPORTUNITIES.md`).
