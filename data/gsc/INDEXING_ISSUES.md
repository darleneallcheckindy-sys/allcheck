# Sitemap & Indexing Health

Status: **Done — real GSC Coverage/Indexing data received, now with actual
URL-level examples.** Two major new findings this pass: a publicly
crawlable staging environment, and a 404'd Greenwood location page that
directly explains the Greenwood ranking decline flagged in
`RANKING_CHANGES.md`.

## Headline finding: 62 of ~149 known pages are NOT indexed right now

Real Coverage report data (`Chart.csv`, `Critical_issues.csv`), most recent
date (2026-09-04): **62 pages not indexed, 87 indexed** (~149 known pages
total, so ~42% of the site isn't in Google's index at all). The five
exclusion reasons sum exactly to 62, so this is internally consistent, real
data.

## NEW — the staging site is publicly exposed and being crawled

Among the "Crawled – currently not indexed" examples, **at least 9 URLs
under `/staging/`** appear: `/staging/indoor-air-quality-testing/` (and its
no-slash twin), `/staging/new-construction-phased`,
`/staging/mold-and-mildew-testing/`, `/staging/be-an-informed-buyer/`,
`/staging/news/`, `/staging/limited-warranty` (and its slash twin),
`/staging/sample-inspection-agreement`, plus a staging PDF
(`/staging/wp-content/uploads/2024/11/prepare_inspection.pdf`, found in the
404 list — meaning that specific staging asset is gone, but the staging
*environment itself* is still live and crawlable elsewhere).

**This is likely the single biggest driver of the 33 "crawled — not
indexed" pages**, ahead of the ordinary trailing-slash duplicates: an entire
parallel copy of site content sitting at `/staging/*`, publicly reachable,
and being crawled as duplicate content. Google correctly declines to index
these, but they still cost crawl budget and add real duplicate-content
noise across the site, which can suppress indexing confidence sitewide, not
just for the staging URLs themselves.

**Recommend to developer, immediately:** block `/staging/` entirely via
`robots.txt` (`Disallow: /staging/`), add `noindex` at the server/template
level for anything under that path, and ideally put the staging environment
behind HTTP auth or a non-public subdomain so it's never crawlable at all.
This is now co-priority with the www/non-www fix — see
`TECHNICAL_URL_CLEANUP.md`.

## NEW — `/greenwood-indiana/` 404s (explains the Greenwood decline)

The 404 examples include **`https://allcheck.biz/greenwood-indiana/`**,
last crawled Jul 10, 2026. This matches the exact URL pattern used by the
other working location pages (`/avon-indiana/` is confirmed live with real
GSC data). **This directly explains the Greenwood decline cluster** flagged
in `RANKING_CHANGES.md` — three Greenwood queries all dropped 5-7 positions
in the same window, and now we know why: the location page those queries
should be able to rely on isn't resolving. Cross-check against
`complete-home-inspection-greenwood-indiana/`, which *does* have real GSC
data (481 impressions) — so Greenwood's *service* page still exists, but a
dedicated `/greenwood-indiana/` city-hub page (parallel to Avon's) appears
to be missing or broken. **Recommend confirming with the developer whether
this page ever existed or was recently removed/renamed**, and restoring it
or 301-ing it to the correct current Greenwood page.

## Other real, actionable URL-level findings

### 404s with real consequences (not just harmless cleanup)
- **`https://allcheck.biz/_information/warranty.htm`** — a legacy URL the
  original audit found carrying 1 real backlink. Now confirmed 404. Modest
  but real, quantifiable link equity being lost for no reason. **Recommend a
  301 to `/services/end-of-builders-warranty/`** (the closest current
  equivalent). Separately, `TECHNICAL_URL_CLEANUP.md` flags
  `_information/articles/keep_basement_web.pdf` as the legacy path carrying
  the much larger 30-backlink figure — that one was **not** among this
  export's 8 shown 404 examples, so its current status is still unconfirmed
  and worth checking directly.
- **`https://allcheck.biz/complete-home-inspection/fishers-indiana/`**
  (single trailing slash, the "Pattern B" Fishers URL debated in
  `TECHNICAL_URL_CLEANUP.md`) — confirmed 404. **This resolves the
  Fishers ambiguity: Pattern A (`/complete-home-inspection-fishers-indiana/`)
  is the only real page; no redirect decision needed there, just confirm the
  404 doesn't need fixing (it's already correctly gone).**
- `http://www.allcheck.biz/component/k2/item/1-lorem-ipsum-is-simply-dummy-text.html?amp=`,
  `/wp-content/themes/Avada-Child-Theme/*`, `/wp-admin/*`,
  `/allcheck-inspections-draft/` — legacy/technical/test paths, expected to
  404, no action needed.

### Noindex — mostly normal, one real content discovery
Of the 9 noindex'd pages, **8 are WordPress `/feed/` RSS endpoints**
(auto-generated per page/category — normal, not a problem) plus one author
archive: **`/author/arnoldv/`**. This confirms a real author account exists
on the site under the name "arnoldv" — worth asking the client whether this
is an inspector, an admin, or a content contributor, since it's directly
relevant to the E-E-A-T/author-bio work planned for Priority 3
(`MASTER_TODO.md`). Do not assume who this is — confirm before using it
anywhere.

**Also notable:** two of the feed URLs reveal real existing content —
`/faq-items/do-i-need-mold-testing/feed/` and
`/faq-items/will-you-get-on-the-roof/feed/` confirm AllCheck already has a
dedicated FAQ content type (`/faq-items/*`) with real individual Q&A pages.
This matters directly for `HOMEPAGE_BATCH.md`'s FAQ section — **before
publishing the newly drafted homepage FAQs, check whether these existing
`/faq-items/*` pieces already cover the same questions**, and reuse/link to
the real existing content instead of duplicating it with fresh copy. The
current `/faq/` page (35 impressions, position 16.63) apparently only links
to these items rather than surfacing them, per the original audit finding —
this is a real, fixable content-reuse opportunity, not just a rewrite.

### Crawled-not-indexed — expands the trailing-slash duplicate list
Beyond the staging cluster above, real non-slash duplicates confirmed for
pages **not previously flagged**: `/glossary-of-terms`, `/new-construction-phased`,
`/agents`, `/limited-warranty`, `/services` (bare) — each has a slash-ed
twin already receiving real traffic in `top_pages_28d.csv`. Added to
`TECHNICAL_URL_CLEANUP.md`.

Also confirmed: `/complete-home-inspection/carmel-indiana/` (Pattern B for
Carmel) is real and crawled (unlike Fishers' Pattern B, which 404s) — so the
Carmel duplicate-pattern decision in `TECHNICAL_URL_CLEANUP.md` still needs
resolving, it isn't a moot point the way Fishers turned out to be.

Real URL-parameter duplication: several RSS/social-share parameter variants
of real pages are being crawled as distinct URLs —
`?utm_source=rss&utm_medium=rss&utm_campaign=...` (on investor-services,
is-your-home-ready-for-summer, light-commercial-inspection),
`?source=post_page...`, and `?trk=organization_guest_main-feed-card-text`
(both the http and https homepage). This is the same root cause as the
www/non-www and trailing-slash issues: **canonical tags are not reliably
telling Google to collapse these variants**, consistent with only 3 pages
sitewide showing a working canonical relationship.

Legacy duplicate PDFs: `http://www.allcheck.biz/pdf/siding_web.pdf` and
`http://www.allcheck.biz/pdf/squeaky_floors_web.pdf` are a different, older
URL structure for PDFs that also exist at
`allcheck.biz/wp-content/uploads/2024/11/*_web.pdf` (confirmed in
`top_pages_28d.csv`). Low priority, but real duplicate content.

Possible duplicate content page: `/our-standards/` (crawled-not-indexed)
vs. `/standards-of-practice/` (real page, 355 impressions) — worth a
developer check on whether `/our-standards/` is an orphaned older version.

## Trend over time (real, from Chart.csv, June 11 – Sept 4)

Indexing health has been **improving**, not worsening: "Not indexed" dropped
from 114 (mid-June) to 62 (current), while "Indexed" grew from 81 to 87. This
is a positive baseline signal, but 62 un-indexed pages — now with real,
identified causes — is still worth acting on deliberately.

## Search Appearance (real GSC export — empty)

The Search Appearance export came back with zero rows — AllCheck currently
has no special search-appearance types (rich results, FAQ snippets, review
stars, etc.) showing in Google. Implementing valid, matching FAQ schema in
Homepage Batch 1 (reusing the real `/faq-items/*` content noted above) is
the most direct way to start populating this category.

## Urgent — confirmed by real GSC Pages export (carried forward, still top priority)

`Pages.csv` shows `http://www.allcheck.biz/` and `https://allcheck.biz/`
as two separate entries with very different average positions (3.71 vs
29.95) and impression volumes (2,487 vs 8,719) — see `CANNIBALIZATION.md`
for full detail. The same www split appears on `/contact-us/` too. This and
the staging-site exposure above are now the two co-top-priority technical
fixes.

## Confirmed (from audit crawl, verifiable facts — not GSC)

- [x] XML sitemap present: `https://allcheck.biz/sitemap.xml`
- [x] Secondary sitemap present: `https://allcheck.biz/sitemap.rss`
- [x] `robots.txt` present at `http://allcheck.biz/robots.txt`
- [x] `robots.txt` does not block any major search engine
- [x] `robots.txt` does not block any major AI crawler — **note: it also
      does not currently block `/staging/`, which it should**
- [x] No `noindex` meta tag on homepage
- [x] No `noindex` HTTP header on homepage
- [x] Canonical tag present on homepage: `https://allcheck.biz/`
- [x] SSL enabled, HTTPS redirect working (on the URL the audit crawled)

## Important pages to confirm are indexed

- [ ] Homepage
- [ ] All 7 Priority 2 service pages (`complete-home-inspection`,
      `environmental-testing-2`, `radon-testing`, `termite-inspection`,
      the canonical 4-point-inspection URL, `new-construction-phased`,
      `end-of-builders-warranty`)
- [ ] All confirmed location pages (Avon, Carmel, Fishers, Greenwood,
      Noblesville, Central Indiana) — **Greenwood confirmed broken, see
      above**
- [ ] `/about-us/`
- [ ] `/faq/`

## Action needed

- [x] GSC Coverage/Indexing report received and processed with real URL
      examples.
- [ ] **Waiting on Developer:** block `/staging/` via robots.txt + noindex +
      access control (new top priority).
- [ ] **Waiting on Developer:** restore or redirect `/greenwood-indiana/`.
- [ ] **Waiting on Developer:** 301 `/_information/warranty.htm` to
      `/services/end-of-builders-warranty/`.
- [ ] **Waiting on Developer:** separately check whether
      `/_information/articles/keep_basement_web.pdf` (30 backlinks) 404s —
      not confirmed by this export's examples.
- [ ] **Waiting on Client:** confirm who "arnoldv" is before any E-E-A-T
      content references this account.
