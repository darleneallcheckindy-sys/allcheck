# Protect Keywords

Status: **Done — real GSC query data.** This replaces the earlier
audit-based version entirely. Read the correction note below before acting
on anything from the original Digicorns audit or the earlier draft of this
file.

## Important correction — the original audit's positions do not match real GSC

The third-party audit claimed `home inspection indianapolis` at #1 and
`allcheck` (bare) at #2. **Real GSC data shows neither is true right now:**

| Query | Audit claimed | Real GSC (current 28d) | Real GSC (previous 28d) |
|---|---:|---:|---:|
| `home inspection indianapolis` | #1 | **6.36** | 7.14 |
| `allcheck` (bare) | #2 | **12.20** | 14.14 |

Conversely, two terms the audit rated as opportunities are already doing
**better** than claimed:
| Query | Audit claimed | Real GSC (current 28d) | Real GSC (previous 28d) |
|---|---:|---:|---:|
| `indianapolis home inspectors` | #9 | **3.29** | 6.76 |
| `home inspectors in indianapolis` | #11 | **4.64** | 4.00 |

**Do not use the original audit's positions for any decision going forward.**
It was either stale or a third-party rank-tracker estimate that doesn't match
Search Console truth. Everything below uses only the real export.

## Keywords to Protect (real GSC data, position ≤ 3, meaningful impressions)

Filtered to impressions ≥ 15 in the current period to exclude single-impression
noise.

| Query | Position | Clicks | Impressions | Ranking Page | Notes |
|---|---:|---:|---:|---|---|
| allcheck inspections | 1.23 | 34 | 130 | Needs query+page crosstab to confirm (likely homepage) | Genuinely protected branded term — real clicks, real volume. Prev. period: pos 1.32, 33 clicks — stable. |
| all check inspections | 1.20 | 26 | 50 | Needs query+page crosstab | Genuinely protected. Prev.: pos 1.07, 37 clicks — position held, clicks down slightly (37→26); watch, not urgent. |
| pre purchase inspection | 1.68 | 0 | 25 | Needs crosstab | Position 1 average but 0 clicks on 25 impressions — see `CTR_OPPORTUNITIES.md`, this is a real anomaly. |
| radon testing near me | 1.00 | 0 | 273 | Needs crosstab | **Flag, don't treat as a normal protect item** — position exactly 1.0 with 273 impressions and 0 clicks is unusual; likely a local-pack/map-result artifact rather than a normal organic listing. See `CTR_OPPORTUNITIES.md` anomaly section. Newly appearing this period (0 impressions previous period). |
| radon inspection near me | 1.00 | 0 | 146 | Needs crosstab | Same anomaly pattern as above. |

## Keywords near-protect (position 4–5, meaningful volume, worth watching closely rather than pushing hard)

| Query | Position | Clicks | Impressions | Notes |
|---|---:|---:|---:|---|
| home inspectors indianapolis | 4.37 | 6 | 226 | Improved from 5.35 → 4.37. Real opportunity, also in `opportunities_4_20.csv`. |
| allcheck inspections reviews | 4.28 | 1 | 111 | Slipped from 3.61 → 4.28 (declined). Branded/reputation term worth watching — see `RANKING_CHANGES.md`. |
| home inspectors in indianapolis | 4.64 | 0 | 11 | Slipped slightly from 4.00 → 4.64. Low volume but exactly the phrase called out as a target in earlier planning — now confirmed near page-one top, not page two as originally believed. |

## Rule

If a keyword already performs strongly (position 1–3, meaningful volume), we
do not aggressively rewrite its ranking page's title, H1, or core opening
copy. Given the correction above, the *only* terms that currently qualify
with real confirmed volume are `allcheck inspections` and
`all check inspections` — both clearly branded. **Do not treat
`home inspection indianapolis` as untouchable anymore** — real data shows it
sitting at position 6.36, which is an opportunity to improve, not a ranking
to protect from change. This changes the calculus for Homepage Batch 1
meaningfully — see `STEP_1_GSC_BASELINE.md`.

## Still outstanding

- [ ] A query+page crosstab export (GSC Performance report with both Query
      and Page dimensions applied together) to confirm exactly which URL is
      ranking for each protected term — right now we're inferring "probably
      the homepage" for the branded terms, not confirming it.
