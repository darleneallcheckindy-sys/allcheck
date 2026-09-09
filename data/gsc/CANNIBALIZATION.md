# Cannibalization Check

Status: **Partially blocked.** True cannibalization confirmation (multiple
URLs receiving meaningful impressions for the same query) requires live GSC
query-by-page data, which is not available in this session. However, the
site's own crawl (from the Digicorns audit) independently surfaces real
**duplicate indexable URLs** for the same city + service pair, which is a
strong structural precondition for cannibalization even before GSC confirms
it. Flagging these now per the instruction to flag, not consolidate, at this
stage.

| Query | Page 1 | Page 2 | Issue | Recommended Primary Page |
|---|---|---|---|---|
| complete home inspection carmel (indiana) | `https://allcheck.biz/complete-home-inspection-carmel-indiana/` | `https://allcheck.biz/complete-home-inspection/carmel-indiana/` | Two live, indexable URLs for the same city/service intent — both found in the site's own internal-link crawl. GSC query-level confirmation still needed. | TBD — needs GSC data on which URL currently holds impressions/position before picking a winner (see `TECHNICAL_URL_CLEANUP.md`) |
| complete home inspection central indiana | `https://allcheck.biz/complete-home-inspection-central-indiana/` | `https://allcheck.biz/complete-home-inspection/central-indiana/` | Same duplicate-pattern issue. | TBD — needs GSC data |
| complete home inspection fishers (indiana) | `https://allcheck.biz/complete-home-inspection-fishers-indiana/` | `https://allcheck.biz/complete-home-inspection/fishers-indiana//` (malformed, double trailing slash) | Same duplicate-pattern issue, plus the second URL is malformed. | TBD — needs GSC data |
| complete home inspection noblesville (indiana) | `https://allcheck.biz/complete-home-inspection-noblesville-indiana/` | `https://allcheck.biz/complete-home-inspection/noblesville-indiana/` | Same duplicate-pattern issue. | TBD — needs GSC data |
| 4-point inspection indianapolis | `https://allcheck.biz/4-point-inspection/` | `https://allcheck.biz/service/4-point-inspection/` and `https://allcheck.biz/services/4-point-inspection/` (three total live paths) | Three live URLs for one service/intent. | TBD — needs GSC data; recommend `/services/4-point-inspection/` as it matches the sitewide pattern (see `TECHNICAL_URL_CLEANUP.md`), but confirm against GSC before redirecting so we don't 301 away from the URL actually holding rankings |
| home inspectors in indianapolis / indianapolis home inspectors | Homepage (per audit) | Unconfirmed — could be a second page also targeting this phrase | Not yet confirmed as cannibalization; two very similar query variants both land in the audit's top-query sample at positions 9 and 11. Needs GSC page-attribution to confirm both queries land on the homepage and not on two different pages. | TBD — needs GSC data |

## Rule for this step

Do not consolidate any of the above pages yet. This file only flags
candidates. Consolidation (canonical + 301) decisions are made in
`TECHNICAL_URL_CLEANUP.md` and should wait for GSC confirmation of which URL
currently holds the ranking/impressions, so we redirect the loser into the
winner rather than guessing.

## Action needed

- [ ] **Waiting on Client:** GSC query-to-page export to confirm which of
      each duplicate pair is actually receiving search impressions.
