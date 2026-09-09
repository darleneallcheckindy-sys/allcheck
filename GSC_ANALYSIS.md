# GSC Analysis — 28-Day Comparison

Status: **Waiting on Client** (live GSC pull) — see "Access needed" below.

## Why this is blocked

This session has no Google Search Console API/OAuth connector attached, and no
outbound network access to allcheck.biz or Google's APIs. A true 28-day vs.
prior-28-day GSC comparison (clicks, impressions, CTR, average position, top
queries, top landing pages, device split, country split) **cannot be pulled
from this environment**. Do not treat any ranking/traffic figures below as
live GSC data — they are sourced from the third-party Digicorns SEO audit of
allcheck.biz (see `66285dc1-report__allcheck.pdf`, uploaded to this session)
and are third-party rank-tracker estimates, not first-party Search Console
numbers.

### Exact access needed to complete this step

- [ ] Add Search Console access for `allcheck.biz` (or its `sc-domain:`
      property) for the Google account this session/agent can use, **or**
- [ ] Export and share: Performance report (Search results), last 28 days vs.
      previous 28 days, split by Query, Page, Device, and Country, plus
      Coverage/Indexing report and Sitemaps status.
- [ ] Confirm the exact GSC property type in use (domain property vs.
      URL-prefix `https://allcheck.biz/`) since this affects www/non-www and
      http/https aggregation.

Mark this item "Waiting on Client" until one of the above is provided. Once
GSC access exists, re-run this file's checklist with real data before any
further homepage or service-page copy changes that could affect rankings —
per `CLAUDE.md` rule 5 ("inspect current GSC performance if available") and
rule 6 ("protect existing rankings").

## Interim baseline (third-party audit data, not GSC — for directional use only)

Audit date context: report contains references to "2026" content dates, so
this is a recent snapshot, but it is a crawler/rank-tracker estimate
(Digicorns), not Search Console truth. Treat positions/volumes as directional
only.

### Traffic (audit estimate)
- Google Organic (est. monthly visits to homepage): 410
- Paid: 0
- AI Overviews: 0

### Top organic keywords (audit estimate, homepage-driven)

| Keyword | Position | Est. monthly searches | Est. traffic |
|---|---|---|---|
| home inspection indianapolis | 1 | 720 | 219 |
| all check inspections | 1 | 210 | 64 |
| allcheck inspections | 1 | 210 | 64 |
| allcheck | 2 | 110 | 18 |
| allcheck inspections reviews | 3 | 70 | 7 |
| indianapolis home inspectors | 9 | 720 | 11 |
| **home inspectors in indianapolis** | **11** | **720** | **7** |
| inspect check | 20 | 1,000 | 2 |
| inspect all | 32 | 1,300 | 3 |
| check a | 76 | 880 | 2 |

### Position distribution (audit estimate, sitewide)

| Position band | # keywords |
|---|---|
| 1 | 3 |
| 2–3 | 2 |
| 4–10 | 3 |
| 11–20 | 6 |
| 21–30 | 7 |
| 31–100 | 42 |

### Striking-distance opportunity (positions 4–20) — highest priority to protect/push

1. **"home inspectors in indianapolis" — position 11.** Same 720/mo search
   volume as the #1 term "home inspection indianapolis." This is the single
   highest-value opportunity identified: it is one word-order variant away
   from a term AllCheck already owns. Do not rewrite the page to force this
   phrase in place of existing winning phrasing — instead work the phrase
   naturally into an H2/H3, FAQ answer, and image alt text on the homepage
   (see `HOMEPAGE_BATCH.md`), since forcing exact-match duplication risks
   cannibalizing the #1 ranking term.
2. "indianapolis home inspectors" — position 9, same phrase family, already
   near page 1. Reinforce via the same natural placements above rather than a
   separate push.
3. Full list of positions 4–20 by exact query, plus true CTR and page-level
   data, requires live GSC — flagged above as Waiting on Client.

### Rankings already strong — protect, do not rewrite (rule 6)

- `home inspection indianapolis` — #1 — **do not change title/H1 aggressively**
- `all check inspections` / `allcheck inspections` — #1
- `allcheck` — #2

### Cannibalization check

Not verifiable without live GSC query/page data. Visually flag one likely risk
from the audit's own crawl: duplicate URL patterns for the same city (e.g.
`/complete-home-inspection-carmel-indiana/` **and**
`/complete-home-inspection/carmel-indiana/` both exist — see
`TECHNICAL_URL_CLEANUP.md`). Two indexed URLs for the same city/service pair
is a plausible cannibalization/duplicate-content risk and should be confirmed
against GSC query-page data once available, then resolved via canonical +
redirect.

### Decay check

Not verifiable without historical GSC trend data. Revisit once GSC access is
granted.

### Sitemap / indexing health (from audit crawl, verifiable facts)

- [x] XML sitemap present: `https://allcheck.biz/sitemap.xml` and
      `https://allcheck.biz/sitemap.rss`
- [x] `robots.txt` present at `http://allcheck.biz/robots.txt`, does not block
      major search engines or major AI crawlers
- [x] No noindex tag or header on homepage
- [x] Canonical tag present on homepage: `https://allcheck.biz/`
- [ ] Actual Indexed vs. Submitted counts, and any Coverage errors — requires
      GSC (Waiting on Client)

## Tracker status

| Task | Status |
|---|---|
| 28-day vs. prior 28-day GSC pull | Waiting on Client (need GSC access) |
| Top queries / top pages export | Waiting on Client |
| Position 4–20 opportunity list | In Progress — seeded from audit data above, needs GSC confirmation |
| High-impression/low-CTR queries | Waiting on Client (no CTR data available outside GSC) |
| Ranking gains/losses | Waiting on Client |
| Cannibalization check | In Progress — one candidate flagged above |
| Decaying content check | Waiting on Client |
| Sitemap/indexing health | Done (verifiable facts recorded above) |
