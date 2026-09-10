# Master SEO / AEO / GEO To-Do

## Priority 1 — Do first

### GSC analysis
Status: Waiting on Client (no GSC access in this environment) — see `GSC_ANALYSIS.md`.
- [ ] Complete last 28 days vs previous 28 days analysis — Waiting on Client
- [ ] Export top queries — Waiting on Client
- [ ] Export top pages — Waiting on Client
- [x] Identify queries ranking positions 4–20 — done from third-party audit data (`home inspectors in indianapolis` #11, `indianapolis home inspectors` #9); needs live GSC confirmation
- [ ] Identify high-impression / low-CTR opportunities — Waiting on Client (needs GSC CTR)
- [ ] Check ranking gains and losses — Waiting on Client
- [ ] Check decay — Waiting on Client
- [x] Check cannibalization — In Progress: one candidate flagged (duplicate location-page URL patterns), see `GSC_ANALYSIS.md` and `TECHNICAL_URL_CLEANUP.md`
- [x] Review sitemap/indexing health — Done, see `GSC_ANALYSIS.md`

### Batch 1 — Homepage
Status: QA / Review — full recommendation set drafted in `HOMEPAGE_BATCH.md`; implementation requires developer/CMS access this session does not have.
- [ ] Remove duplicate H1 tags — Waiting on Developer (recommendation drafted)
- [x] Build proper H2/H3 hierarchy — drafted in `HOMEPAGE_BATCH.md`
- [ ] Remove duplicate semantic headings / responsive duplicate headings — Waiting on Developer
- [x] Validate and protect existing title tag using GSC — validated against audit data; keep unchanged
- [x] Improve meta description only if data supports it — drafted (167 → 154 chars)
- [x] Map primary and secondary keyword intent — see `HOMEPAGE_BATCH.md` and `GSC_ANALYSIS.md`
- [x] Improve opening copy for Indianapolis / Central Indiana relevance — drafted
- [ ] Verify and publish consistent NAP — Waiting on Client (address confirmation), see `LOCAL_SEO_FOUNDATION.md`
- [x] Validate LocalBusiness / HomeAndConstructionBusiness schema — JSON-LD drafted in `LOCAL_SEO_FOUNDATION.md`
- [x] Add visible FAQ/Q&A section — 6 FAQs + FAQPage schema drafted
- [x] Strengthen trust / E-E-A-T signals — drafted; named-inspector credentials flagged Waiting on Client
- [x] Audit all homepage internal links — see `TECHNICAL_URL_CLEANUP.md`
- [x] Fix homepage image alt text — alt text drafted for all 12 real images missing it
- [ ] Fix obvious homepage performance contributors — Waiting on Developer (JS audit flagged as highest-leverage fix)
- [ ] Complete final desktop/mobile QA — pending live implementation

### Local / technical foundation
Status: **Ready for Developer** — see `LOCAL_SEO_FOUNDATION.md` and
`TECHNICAL_URL_CLEANUP.md` for full findings; the three most critical items
(www/non-www split, public staging site, `/greenwood-indiana/` 404) are now
packaged as a standalone handoff ticket at
`tasks/PRIORITY_1_TECHNICAL_DEVELOPER_TICKET.md`, ready to hand to a
developer as-is. **No live changes have been made to allcheck.biz** — this
status change reflects that the ticket is ready to be worked, not that the
fixes are implemented.
- [ ] Verify business address and phone against GBP — Waiting on Client (phone/email independently confirmed via audit crawl; address not re-verified)
- [x] Make NAP consistent sitewide — NAP block and placement spec drafted, pending client confirmation + developer implementation
- [x] Fix malformed Fishers URL/path — identified exact broken link (`omplete-home-inspection` typo + double trailing slash), Waiting on Developer
- [x] Determine canonical 4-point inspection URL — recommend `/services/4-point-inspection/` (matches sitewide pattern), Waiting on Developer to implement redirects
- [x] Clean trailing-slash / duplicate URL variants — full list documented in `TECHNICAL_URL_CLEANUP.md`, Waiting on Developer
- [x] Verify legacy HTTP/WWW URLs 301 correctly — **Ready for Developer**, see `tasks/PRIORITY_1_TECHNICAL_DEVELOPER_TICKET.md` Issue 1 for the exact redirect map and validation steps
- [x] Lock down publicly crawlable staging site (`/staging/*`) — **Ready for Developer**, see `tasks/PRIORITY_1_TECHNICAL_DEVELOPER_TICKET.md` Issue 2
- [x] Restore or redirect 404'd `/greenwood-indiana/` — **Ready for Developer**, see `tasks/PRIORITY_1_TECHNICAL_DEVELOPER_TICKET.md` Issue 3

## Priority 2 — Core money pages

- [ ] Complete Home Inspection full page batch
- [ ] Environmental Testing hub full page batch
- [ ] Radon Testing full page batch
- [ ] Termite Inspection full page batch
- [ ] 4-Point Inspection consolidation + optimization
- [ ] New Construction Phased Inspection full page batch
- [ ] 11-Month / Builder Warranty Inspection full page batch

## Priority 3 — Supporting services / local / authority

- [ ] Water Testing
- [ ] Septic System Testing
- [ ] Re-Inspection
- [ ] Home Maintenance Inspection
- [ ] Investor Services
- [ ] Light Commercial Inspection
- [ ] About Us / inspector E-E-A-T
- [ ] Avon location page
- [ ] Carmel location page
- [ ] Fishers location page
- [ ] Greenwood location page
- [ ] Noblesville location page
- [ ] Additional location pages based on GSC opportunity

## Ongoing — run in parallel

- [ ] Keep following up on new AllCheck website blogs
- [ ] Target homeowner questions, service searches, and Indianapolis/Central Indiana topics
- [ ] Continue 3-platform external blog strategy
- [ ] Continue Substack distribution
- [ ] Continue Medium distribution
- [ ] Confirm / maintain third external blog platform
- [ ] Avoid exact duplicate external articles
- [ ] Add natural internal links from blogs to money pages
- [ ] Build question-based AEO content clusters

## Priority 4 — Sitewide growth / lower-priority enhancements

- [ ] Improve sitewide performance after page cleanup
- [ ] Final missing-alt sweep
- [ ] Implement `llms.txt`
- [ ] Improve backlink quality
- [ ] Build Indianapolis / Indiana local PR and citations
- [ ] Grow YouTube educational content
- [ ] Install Meta Pixel only when paid retargeting is planned
- [ ] Decide whether an X/Twitter presence is worthwhile
- [ ] Review plain-text email exposure / spam protection

## Session Log

### Session 1 — Priority 1 execution

**Completed:**
- GSC analysis step documented; live pull blocked, interim baseline built from third-party audit data (`GSC_ANALYSIS.md`)
- Homepage batch: full H1/H2/H3 structure, title/meta review, opening copy, 6 FAQs + FAQPage schema, E-E-A-T copy, image alt text for all 12 real images, performance guidance drafted (`HOMEPAGE_BATCH.md`)
- Local SEO foundation: NAP block, HomeAndConstructionBusiness JSON-LD, service-area wording, verified social profile list (`LOCAL_SEO_FOUNDATION.md`)
- Technical URL cleanup: full duplicate/malformed/triplicate URL map with canonical recommendations, sourced from the audit's actual crawl (`TECHNICAL_URL_CLEANUP.md`)

**Blockers:**
- No live GSC/Search Console access in this environment — Waiting on Client
- No network access to allcheck.biz from this environment — nothing above could be re-verified against the live site; all recommendations are sourced from the Digicorns audit crawl and existing repo task files, and are clearly flagged where they need client or developer confirmation
- No CMS/developer access — nothing in this repo can be implemented directly; every deliverable above is written for developer handoff

**Pages changed (in this repo, as planning/content deliverables):** none — no live site code exists in this repository. Content/spec deliverables created: `GSC_ANALYSIS.md`, `LOCAL_SEO_FOUNDATION.md`, `TECHNICAL_URL_CLEANUP.md`; `HOMEPAGE_BATCH.md` and this file updated.

**URLs changed or redirected:** none implemented (no dev access). Recommended redirect map is in `TECHNICAL_URL_CLEANUP.md`.

**Keywords protected/targeted:** Protected — `home inspection indianapolis` (#1), `all check inspections`/`allcheck inspections` (#1), `allcheck` (#2): no title/H1 rewrite recommended. Targeted — `home inspectors in indianapolis` (#11) and `indianapolis home inspectors` (#9) via natural FAQ/H2/H3 placement, not forced exact-match duplication.

**Next recommended task:** Once GSC access and developer/CMS access are available, implement the Homepage batch deliverable and the local schema/NAP fix together (they share the same schema edit), then move to Priority 2 starting with Complete Home Inspection per `PAGE_BATCH_WORKFLOW.md`. Do not start Priority 2 content work before Priority 1's technical/local items are at least implemented or explicitly deferred by the client, per the "don't start a new page batch with unresolved applicable tasks" rule.

### Session 2 — Real GSC data integration + technical developer ticket

**Completed:**
- Full real GSC Performance and Coverage/Indexing data processed (Queries, Pages, Devices, Countries, Search Appearance, Coverage) — see `data/gsc/`. Corrected the original third-party audit's keyword positions against real data.
- Identified three critical technical issues from real GSC evidence: www/non-www ranking split, publicly crawlable staging site, and a 404'd `/greenwood-indiana/` page that explains a real ranking decline.
- Packaged the three critical issues into a standalone developer handoff: `tasks/PRIORITY_1_TECHNICAL_DEVELOPER_TICKET.md` — includes exact redirect mapping, safe staging-removal sequencing, a Greenwood restore-vs-redirect decision rule, implementation order, validation checklist, and an explicit "Needs Confirmation" list.

**Blockers:** unchanged — no CMS/developer/live-site access in this environment. The ticket above is written and ready but **no live changes have been made to allcheck.biz.**

**Next recommended task:** Hand `tasks/PRIORITY_1_TECHNICAL_DEVELOPER_TICKET.md` to a developer for implementation. In parallel (no CMS access needed), review and finalize the Homepage Batch 1 copy/SEO recommendations in `HOMEPAGE_BATCH.md` against the real GSC data now available.
