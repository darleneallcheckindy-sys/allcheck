# Ranking Changes — Current 28 Days vs. Previous 28 Days

Status: **Blocked — Needs Live GSC Export.**

Identifying newly ranking, improved, declined, and lost queries requires two
time-boxed GSC exports (current 28 days and previous 28 days) compared
query-by-query. This session has no GSC access and no historical export to
compare — the single third-party audit snapshot used elsewhere in this repo
is a single point in time, not a comparison, so it cannot populate this file
at all. Populating this with guessed trend direction would violate the
"do not invent rankings" rule.

## What this file will contain once GSC access exists

| Query | Position (Previous 28d) | Position (Current 28d) | Change | Clicks Change | Impressions Change | Notes |
|---|---:|---:|---:|---:|---:|---|

Categorized into:
- **Newly ranking** — queries with no prior-period data
- **Improved** — position moved up
- **Declined** — position moved down (flag anything commercially important)
- **Lost** — previously ranking, now absent

Special attention: any commercially important keyword (see
`PROTECT_KEYWORDS.md` and `opportunities_4_20.csv`) that lost clicks or
dropped several positions should be called out at the top of this file, not
buried in a full table.

## Action needed

- [ ] **Waiting on Client:** GSC access or a current-28d + previous-28d
      Performance export to complete this comparison.
