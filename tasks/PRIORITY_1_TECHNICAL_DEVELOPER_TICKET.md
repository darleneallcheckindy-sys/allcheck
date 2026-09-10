# Priority 1 Technical SEO Developer Ticket

Project: AllCheck Inspections
Domain: https://allcheck.biz/
Priority: Critical
Status: Ready for Developer
Source: Real GSC analysis + technical review

## Objective

Resolve the highest-impact technical SEO issues currently affecting indexing,
ranking consistency, canonical consolidation, and location-page performance.

---

## Issue 1: WWW vs Non-WWW Split

### Current problem
Google is tracking `http://www.allcheck.biz/` and `https://allcheck.biz/` as
two separate, independently-ranked pages instead of treating one as the
canonical URL and the other as a redirect. The same split has also been
confirmed on at least one other page (`/contact-us/`), so this is a sitewide
host-level issue, not a one-page anomaly.

### Evidence
Real GSC Performance export (`data/gsc/top_pages_28d.csv`, current 28-day
period):

| URL | Clicks | Impressions | Avg. Position |
|---|---:|---:|---:|
| `http://www.allcheck.biz/` | 62 | 2,487 | 3.71 |
| `https://allcheck.biz/` | 59 | 8,719 | 29.95 |
| `https://allcheck.biz/contact-us/` | 0 | 712 | 13.75 |
| `https://www.allcheck.biz/contact-us` | 0 | 219 | 11.67 |

The homepage's declared canonical tag correctly points to
`https://allcheck.biz/`, yet the www variant is the one holding the strong
average position (3.71 vs 29.95). This means the site's real ranking
strength is not landing on the URL the canonical tag claims is authoritative.
Separately, the original third-party audit's backlink data shows
`http://www.allcheck.biz/` carrying 230 backlinks — the single largest link
target in the site's entire backlink profile — and `https://www.allcheck.biz/`
carrying 2 more, so this also represents real, at-risk link equity, not just
a ranking-report artifact.

Full detail: `TECHNICAL_URL_CLEANUP.md`, `data/gsc/CANNIBALIZATION.md`,
`data/gsc/INDEXING_ISSUES.md`.

### SEO impact
- Ranking signal for the homepage (and likely other pages) is split across
  two URLs Google treats as distinct, which can suppress the position either
  URL could achieve on its own.
- 230+ backlinks pointing at the non-canonical host are not consolidating
  onto the canonical URL.
- Any page-level fix elsewhere on the site (content, schema, FAQs) will be
  working against this split until it's resolved — this is why it's
  sequenced first.

### Required Fix
1. Confirm the preferred canonical host.
2. Force all alternate host variants to 301 redirect to the canonical host.
3. Preserve full URL path and query string where appropriate.
4. Update internal links to use the canonical host only.
5. Update sitemap URLs to canonical host only.
6. Confirm canonical tags also point to the canonical host.
7. Check that robots.txt does not conflict with the preferred host.
8. Re-test representative URLs after deployment.

**Only use this mapping if `https://allcheck.biz/` is confirmed as the
preferred canonical version** — this is the site's own declared canonical
tag and the pattern the rest of the URL structure already assumes, but it
must be confirmed, not assumed, before implementation (see "Needs
Confirmation" section below).

| Source URL Pattern | Destination Pattern | Redirect Type |
|---|---|---|
| `https://www.allcheck.biz/*` | `https://allcheck.biz/*` | 301 |
| `http://allcheck.biz/*` | `https://allcheck.biz/*` | 301 |
| `http://www.allcheck.biz/*` | `https://allcheck.biz/*` | 301 |

### Validation steps
- Request each of the four host/protocol combinations for at least 10
  representative URLs (homepage, `/contact-us/`, 2-3 service pages, 1-2
  location pages) and confirm each resolves in a single 301 hop to the
  canonical `https://allcheck.biz/...` URL.
- Confirm no redirect chains (e.g. `http://www.` → `https://www.` →
  `https://` counts as a chain, not a single hop) and no redirect loops.
- Confirm the canonical `<link rel="canonical">` tag on each tested page
  matches the URL it now resolves to.
- Re-pull GSC Pages data 2-4 weeks post-deploy and confirm the www and
  non-www entries for the same page have merged into one entry with
  combined (not split) impressions/clicks.

### Rollback/precaution notes
- Do not remove the existing canonical tags while implementing redirects —
  they should already agree with the redirect destination; if they don't,
  fix the mismatch as part of this same change, not separately.
- Implement and test on a staging/preview environment first if available —
  see Issue 2, this ticket does not assume the current staging setup is
  safe to test against as-is.
- If a CDN or reverse proxy sits in front of the origin server (see "Needs
  Confirmation" below), redirects may need to be configured at that layer
  instead of (or in addition to) the CMS/server level — confirm this before
  implementing only a CMS-level redirect that the CDN could bypass or cache
  incorrectly.

---

## Issue 2: Public Staging URLs Being Crawled

### Current problem
A staging copy of the site is publicly reachable at `/staging/*` and is
being crawled by Google as live, duplicate content.

### Evidence
Real GSC Coverage report ("Crawled – currently not indexed" category)
includes at least 9 confirmed `/staging/*` URLs:
- `/staging/indoor-air-quality-testing/` (and a no-slash variant)
- `/staging/new-construction-phased`
- `/staging/mold-and-mildew-testing/`
- `/staging/be-an-informed-buyer/`
- `/staging/news/`
- `/staging/limited-warranty` (and a slash variant)
- `/staging/sample-inspection-agreement`

A staging asset was also found in the "Not found (404)" category
(`/staging/wp-content/uploads/2024/11/prepare_inspection.pdf`), confirming
the staging environment itself has been live and crawlable for some time,
not just briefly exposed.

Full detail: `data/gsc/INDEXING_ISSUES.md`.

### SEO impact
- This is very likely the single largest contributor to the 33 pages in the
  "Crawled – currently not indexed" bucket (out of 62 total non-indexed
  pages, ~42% of the known site) — Google is correctly declining to index
  duplicate staging content, but the duplication itself still consumes
  crawl budget and adds sitewide duplicate-content noise that can suppress
  indexing confidence for production pages too.
- Any staging content that duplicates production content dilutes which URL
  Google considers authoritative for that content.

### Required Fix
1. Identify all publicly accessible `/staging/*` URLs.
2. Remove staging URLs from XML sitemaps.
3. Remove internal links pointing to staging URLs.
4. Ensure staging pages do not canonicalize incorrectly to staging URLs
   (i.e. a staging page must not declare itself as its own canonical if a
   production equivalent exists — and must not omit a canonical entirely).
5. Prevent future staging pages from becoming indexable by default (fix at
   the environment/template level, not per-page).
6. Prefer authentication or server-level restriction for staging over
   relying on `robots.txt`/`noindex` alone.
7. If indexing controls are used, confirm they do not block Google before
   removal is processed.
8. Request reprocessing/re-crawl of production URLs after deployment.

**Important — do not treat `robots.txt Disallow: /staging/` as a sufficient
fix on its own.** If any of these staging URLs are already indexed or
already known to Google (the evidence above shows Google has been crawling
them for some time), blocking crawl access via `robots.txt` before those
pages carry a `noindex` tag or a redirect can actually prevent Google from
ever seeing the removal signal — a blocked page's existing index entry can
become stuck rather than cleared, because Google can no longer crawl it to
discover it should be dropped. The safer sequence is: add `noindex` (and/or
redirect duplicate staging pages to nothing, or 404/410 them) first, allow
Google to recrawl and process that signal, and only then apply `robots.txt`
blocking and/or authentication as the long-term prevention layer.

### Validation steps
- Confirm every previously-identified `/staging/*` URL either 404s, 410s,
  requires authentication, or is blocked by `robots.txt` (only after the
  noindex/removal signal has had time to process, per the sequencing note
  above).
- Confirm the XML sitemap contains zero `/staging/` URLs.
- Search the site's rendered HTML/templates for any remaining internal
  links pointing to `/staging/*` paths.
- Re-check the GSC Coverage report 2-6 weeks post-deploy and confirm the
  "Crawled – currently not indexed" count has dropped meaningfully from 33.

### Rollback/precaution notes
- Do not delete the staging environment's content outright if it's still
  needed for development/preview — the fix is to make it non-public and
  non-indexable, not necessarily to destroy it.
- Coordinate with whoever uses staging for QA/preview before restricting
  access, so their workflow isn't broken by the same change that fixes SEO
  exposure.

---

## Issue 3: `/greenwood-indiana/` Returns 404

### Current problem
`https://allcheck.biz/greenwood-indiana/` — a URL matching the pattern of
the working `/avon-indiana/` location-hub page — currently returns a 404.

### Evidence
Real GSC Coverage report, "Not found (404)" category, last crawled Jul 10,
2026. Separately, `data/gsc/RANKING_CHANGES.md` documents a real ranking
decline across three distinct Greenwood-related queries (all dropped 5-7
average positions in the same comparison window) with no other explanation
found in the data until this 404 was confirmed. Note that
`https://allcheck.biz/complete-home-inspection-greenwood-indiana/` (the
service+city page, distinct from the city-hub page) still exists and
carries real traffic (481 impressions, current 28-day period) — it is
specifically the city-hub page that is missing or broken, not Greenwood
content generally.

Full detail: `TECHNICAL_URL_CLEANUP.md`, `data/gsc/RANKING_CHANGES.md`.

### SEO impact
- Direct, confirmed cause of a real ranking decline already observed in
  live GSC data for Greenwood-area queries.
- Any internal links, external backlinks, or bookmarked/shared links
  pointing at this URL currently dead-end.
- Google's own crawler has already recorded this as a 404 (first noted
  well before the last-crawled date above per the report's "first detected"
  data), meaning this is not a brand-new or transient issue.

### Decision Rule

If a valid Greenwood location page should exist:
- Restore the page at `/greenwood-indiana/`
- Preserve the same URL if it already has history/backlinks
- Re-add internal links
- Include it in sitemap
- Request indexing

If Greenwood content now belongs at another canonical URL:
- 301 `/greenwood-indiana/` to the correct Greenwood page
- Update all internal links
- Remove dead URL from sitemap
- Request recrawl

**Do not redirect the 404 to the homepage unless there is no relevant
replacement page.** A generic homepage redirect discards the specific local
intent this URL was built to capture and is very unlikely to recover the
Greenwood ranking decline documented above.

### Required Fix
1. Confirm with the developer/CMS owner whether `/greenwood-indiana/` ever
   existed as a live page, and if so, whether it was intentionally removed,
   accidentally deleted, or renamed.
2. Apply the Decision Rule above based on that finding.
3. Whichever path is chosen, ensure the resulting live URL is linked from
   the same places the working `/avon-indiana/` (and other working location
   hub pages) are linked from, so it receives equivalent internal-link
   support.

### Validation steps
- Confirm `/greenwood-indiana/` returns a 200 (if restored) or a single-hop
  301 to the correct replacement URL (if redirected) — not a 404, and not a
  redirect chain.
- Confirm the resulting live URL is included in the XML sitemap.
- Confirm internal links to Greenwood content across the site (footer,
  location-page navigation, "Areas We Serve" sections, relevant service
  pages) point to the resolved URL, not the dead one.
- Request indexing for the resolved URL in GSC after deployment.
- Monitor the three Greenwood queries documented in
  `data/gsc/RANKING_CHANGES.md` over the following weeks for position
  recovery.

### Rollback/precaution notes
- If restoring the original page, check whether any of its original content
  is recoverable (backups, cached versions, version history) rather than
  writing it from scratch, to preserve whatever was originally working for
  it.
- If choosing the redirect path instead, confirm the destination page
  actually covers Greenwood-specific intent (not just a generic service
  page) — redirecting local-intent traffic to non-local content risks the
  same suppression this fix is meant to resolve.

---

## Implementation Order

1. Confirm canonical host
2. Fix www/non-www redirect behavior
3. Lock down public staging environment
4. Remove staging URLs from sitemap/internal discovery
5. Recover or redirect `/greenwood-indiana/`
6. Update internal links and canonical tags
7. Regenerate/verify sitemap
8. Validate redirects and status codes
9. Request re-crawl/indexing where appropriate
10. Monitor GSC for 2-6 weeks

---

## Validation Checklist

- [ ] One canonical host resolves consistently
- [ ] Alternate host variants return 301
- [ ] No redirect chains
- [ ] No redirect loops
- [ ] Staging URLs are no longer discoverable/indexable
- [ ] Production pages remain crawlable
- [ ] `/greenwood-indiana/` no longer returns 404
- [ ] Canonical tags point to intended production URLs
- [ ] Sitemap contains canonical production URLs only
- [ ] Internal links use canonical URLs
- [ ] Key pages return 200
- [ ] GSC re-check scheduled after deployment

---

## Needs Confirmation Before Deployment

- Preferred canonical host: www or non-www (this ticket assumes non-www,
  `https://allcheck.biz/`, based on the existing canonical tag and URL
  structure — but this must be explicitly confirmed, not assumed, before
  any redirect is implemented)
- Server/CDN platform handling redirects
- Current staging setup (subdomain vs. subdirectory, what tooling manages
  it, who relies on it for QA/preview)
- Whether Greenwood should be restored or redirected
- Access to sitemap/SEO plugin settings
- Whether Cloudflare or another reverse proxy is in use

---

## Related repository files

- `TECHNICAL_URL_CLEANUP.md` — full technical findings, including additional
  lower-priority items not repeated in this ticket (trailing-slash
  duplicates, the 4-Point Inspection triplicate URLs, the Environmental
  Testing `-2` slug, legacy Joomla URLs, legacy duplicate PDF paths)
- `data/gsc/CANNIBALIZATION.md` — page-level duplicate/cannibalization
  evidence
- `data/gsc/INDEXING_ISSUES.md` — full Coverage report breakdown
- `data/gsc/RANKING_CHANGES.md` — the Greenwood decline evidence

No live changes have been made to allcheck.biz as part of producing this
ticket. This document is a handoff for developer implementation only.
