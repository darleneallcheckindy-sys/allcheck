# Batch 1 — Homepage

URL: `https://allcheck.biz/`

## Goal

Improve homepage SEO/AEO/GEO/local visibility while protecting strong existing Indianapolis rankings.

## Known audit findings

- more than one H1 detected (audit shows 3 H1 tags: one empty, one
  `✓HOME INSPECTORS IN INDIANAPOLIS YOU CAN TRUST`, one empty)
- 36 H2s and no H3-H6 structure in audit
- repeated headings / service names detected (see exact duplicate list below)
- title is already strong and should not be changed aggressively
- meta description slightly long (167 chars; target 120–160)
- local address not clearly detected
- LocalBusiness schema incomplete / not detected (Organization +
  HomeAndConstructionBusiness identity schema exists, but has no address)
- visible Q&A content lacking (FAQ nav link exists, no visible answers)
- trust/authority signals can be stronger (604-review rating shown, no
  certifications/awards/author credentials surfaced)
- internal URL inconsistencies exist elsewhere on site (see `TECHNICAL_URL_CLEANUP.md`)
- site has missing alt attributes (18 of 108 sitewide)
- performance score is 60 (server response 1.17s, full load 3.5s, scripts 5.3s, 2.69MB page weight)

Live re-verification note: this session has no network access to allcheck.biz
and no GSC access, so the above is carried from the Digicorns audit crawl,
not re-checked live. Treat the deliverable below as the recommended fix set
for developer implementation, pending the confirmations flagged inline.

## Tasks

### Search data first
- [ ] Pull homepage GSC queries — **Waiting on Client** (see `GSC_ANALYSIS.md`)
- [x] Confirm top-ranking homepage terms — done from audit data: `home inspection indianapolis` (#1), `all check inspections`/`allcheck inspections` (#1), `allcheck` (#2). Live GSC confirmation still outstanding.
- [x] Identify position 4–20 homepage opportunities — `home inspectors in indianapolis` (#11) and `indianapolis home inspectors` (#9), see `GSC_ANALYSIS.md`
- [ ] Identify high-impression / low-CTR homepage terms — **Waiting on Client** (needs GSC CTR data)

### Semantic structure
- [x] Keep exactly one H1 — recommendation below
- [x] Recommended concept: `Home Inspectors in Indianapolis You Can Trust` (already live in the one non-empty H1 — keep verbatim, it's working and protects current #1 rankings)
- [x] Convert major sections to H2 — structure below
- [x] Convert individual service headings to H3 where appropriate — structure below
- [ ] Remove duplicate hidden/responsive semantic headings — **Waiting on Developer** (see notes below; this is a template/builder-level fix, not a content fix)

### Metadata
- [x] Protect current title unless GSC supports a change — keep `Home Inspectors Indianapolis | AllCheck Inspections` (51 chars, optimal length, ranks #1 for its core term)
- [x] Review meta description against live CTR data — drafted replacement below (live CTR confirmation still outstanding, pending GSC)

### Content
- [x] Clarify Indianapolis + Central Indiana service area near top of page — copy below
- [x] Reinforce verified differentiators naturally — copy below
- [x] Preserve "within 24 hours" report wording — used in copy and FAQ below
- [x] Avoid generic SEO filler — reviewed against `SKILL.md` writing rules

### Local SEO
- [ ] Verify GBP NAP — **Waiting on Client** (see `LOCAL_SEO_FOUNDATION.md`)
- [x] Display consistent NAP — NAP block and placement spec drafted in `LOCAL_SEO_FOUNDATION.md`
- [x] Validate LocalBusiness/HomeAndConstructionBusiness schema — JSON-LD drafted in `LOCAL_SEO_FOUNDATION.md`

### AEO/GEO
- [x] Add 4–6 visible homeowner FAQs — 6 drafted below
- [x] Cover inspection scope
- [x] Cover duration
- [x] Cover buyer attendance
- [x] Cover report timing
- [x] Cover service area
- [x] Cover add-on/environmental testing
- [x] Add FAQ schema only if valid and supported — FAQPage JSON-LD drafted below (developer should only publish this if every visible answer text matches the schema text exactly, per Google's FAQ rich-result guidelines)

### E-E-A-T
- [x] Surface 18+ years experience — copy below
- [ ] Surface inspector expertise/credentials only if verified — **Waiting on Client**: audit backlink data independently surfaces a NACHI-certified-inspector profile and a homeinspector.org profile for the name "Jason Satterthwaite" linking to allcheck.biz. This is a real signal worth pursuing for bios/E-E-A-T (Priority 3), but it must be confirmed with the client as the correct current inspector name/title before it is published anywhere — do not publish an unverified name. A second, separate identity was also found via the real GSC Coverage report: an author account at `/author/arnoldv/` (see `data/gsc/INDEXING_ISSUES.md`). Do not assume this is the same person or an inspector at all — confirm who "arnoldv" is before using it anywhere.
- [x] Use Home Inspector Institute context accurately — referenced generically per `ALLCHECK_BRAND.md`, no specific claims invented
- [x] Surface strong review proof without overclaiming — see note below on the 604-review figure

### Links/images/performance
- [ ] Click-test every service card and CTA — **Waiting on Developer** (needs live site access)
- [x] Replace malformed/noncanonical internal URLs — full list in `TECHNICAL_URL_CLEANUP.md`; homepage service cards should point to the canonical `/services/<slug>/` pattern once confirmed
- [x] Review homepage image alt text — alt text drafted below for every real (non-placeholder) image missing one
- [ ] Check large images — **Waiting on Developer**; audit shows 0.63MB total images, 1.25MB JS is the larger contributor to the 2.69MB page weight and 5.3s script-complete time — flag JS/script audit to developer as the higher-impact performance fix, not images
- [x] Check duplicate hidden sections — flagged below (same root cause as duplicate H2s)
- [ ] Check sliders/video/animations that add unnecessary load — **Waiting on Developer** (needs live site access to inspect)

### Final QA
- [ ] One H1 confirmed — pending developer implementation
- [ ] H2/H3 hierarchy confirmed — pending developer implementation
- [ ] Mobile checked — pending live QA pass after implementation
- [ ] Desktop checked — pending live QA pass after implementation
- [ ] Links checked — pending live QA pass after implementation
- [ ] NAP checked — pending client confirmation + implementation
- [ ] Schema checked — pending implementation, validate with Google's Rich Results Test once live
- [ ] FAQs checked — pending implementation
- [ ] CTA checked — pending live QA pass after implementation
- [ ] GSC baseline recorded for post-change monitoring — pending GSC access

---

## Deliverable: recommended homepage structure

### H1 (keep — do not change)

```
Home Inspectors in Indianapolis You Can Trust
```

Developer note: the audit shows this exact text rendering with a leading `✓`
character baked into the H1 text node itself (`✓HOME INSPECTORS IN
INDIANAPOLIS YOU CAN TRUST`), plus two additional **empty** H1 tags elsewhere
on the page. Fix: (1) strip the stray `✓` character out of the H1 text (it's
almost certainly a logo/icon glyph that leaked into the heading rather than
staying in an adjacent icon element), (2) find and remove or demote the two
empty H1 elements — on Avada/Fusion-builder sites this is typically a
title-heading module left in an empty state, or a responsive-duplicate column
rendered twice (once per breakpoint) with the same module set to H1. This is
a template-level fix — flagging as **Waiting on Developer**.

### H2 / H3 tree (recommended)

```
H2: A Complete Home Inspection Delivers Clarity and Confidence
H2: Services We Offer
  H3: Complete Home Inspection
  H3: Environmental Testing
  H3: Re-Inspection
  H3: New Construction (Phased)
  H3: End of Builder's Warranty
  H3: Home Maintenance Inspection
  H3: Investor Services
  H3: Light Commercial Inspection
H2: Highly Qualified, Experienced, and Professional Inspectors
H2: Know What's in Your Home
H2: Areas We Serve
H2: Home Inspection Resources
  H3: How Much Does a Home Inspection Cost in Indianapolis? (2026 Pricing Guide)
  H3: Electrical Safety Tips Every Homeowner Needs to Know
  H3: Top Energy-Saving Upgrades for a More Efficient Home
  H3: Latest AllCheck News
H2: Frequently Asked Questions
H2: What Homeowners Are Saying
H2: Schedule Your Inspection
```

This removes the exact duplicates the audit found (every one of "Services We
Offer," "Complete Home Inspection," "Environmental Testing," "Re-Inspection,"
"New Construction (Phased)," "End of Builder's Warranty," "Know What's in
Your Home," and all three article titles appeared **twice** in the crawl).
That is almost always a responsive-duplicate pattern (the same block rendered
once for desktop and once for mobile, both indexable) rather than two
different pieces of content — flagging the actual de-dupe as **Waiting on
Developer**, since this session cannot inspect the live template to confirm
which instance is the "real" one vs. the responsive duplicate.

"Areas We Serve" is a new section, added per the source strategy doc and to
support internal linking into the six location pages (see
`LOCAL_SEO_FOUNDATION.md`) — it does not exist as a distinct H2 in the
current audit and needs client sign-off that this is a wanted addition before
a developer builds it, since it's new content, not a fix to existing content.

### Title tag (no change)

```
Home Inspectors Indianapolis | AllCheck Inspections
```
51 characters — already optimal length and currently the #1-ranking page for
its core term. Do not touch without GSC data showing a specific problem.

### Meta description (revise — current is 167 characters, over the 120–160 target)

Current (too long, 167 chars):
> "Home inspectors in Indianapolis providing clear, thorough, and unbiased inspections for buyers and sellers across Central Indiana. Trusted, professional, and reliable."

Recommended replacement (154 characters):
> "Home inspectors in Indianapolis providing clear, thorough inspections for buyers and sellers across Central Indiana. Reports delivered within 24 hours."

This trims length, drops generic trust adjectives ("Trusted, professional,
and reliable") in favor of one concrete, verifiable differentiator (24-hour
report turnaround) per the brand's "prefer concrete observations" writing
rule — and per the wording rule, never "same-day report."

### Opening copy (top of page, above/near the hero)

> AllCheck Inspections has spent 18+ years helping buyers, sellers, and
> homeowners across Indianapolis and Central Indiana understand exactly what
> they're getting into — before it becomes a surprise. Every inspection is
> built around clarity: a licensed inspector walks the property with you,
> explains what's found in plain language, and delivers a full report within
> 24 hours.

This keeps the "knowledgeable neighbor + licensed professional" voice, uses
"within 24 hours" correctly, and puts "Indianapolis and Central Indiana" in
the first two sentences without repeating the H1's exact phrase mechanically.

### FAQ section (visible Q&A — add near the bottom of the homepage, above the footer)

**Before publishing the drafted FAQs below, check for reuse first.** The
real GSC Coverage report (see `data/gsc/INDEXING_ISSUES.md`) confirms
AllCheck already has a dedicated FAQ content type at `/faq-items/*` with
real individual Q&A pages (e.g. "do-i-need-mold-testing",
"will-you-get-on-the-roof") — the current `/faq/` page apparently only links
to these rather than surfacing them, per the original audit finding. Check
whether any of the drafted questions below already have an existing,
client-approved answer at `/faq-items/*` and reuse that exact wording where
it overlaps, rather than publishing a fresh, possibly-inconsistent answer to
the same question in two places on the site.

```
### What does a home inspection in Indianapolis include?
A full inspection covers the home's major systems and structure — roof,
foundation, electrical, plumbing, HVAC, attic, and more — so you know the
real condition of the property before you buy, sell, or maintain it.

### How long does a home inspection take?
Most inspections take a few hours. Larger homes, older homes, and homes with
more systems to check usually take longer, since the inspector is covering
more ground.

### Should I attend my home inspection?
Yes, when possible. Walking through the home with your inspector lets you
see issues firsthand and ask questions on the spot, rather than reading about
them later in a report.

### How soon will I get my inspection report?
AllCheck delivers every inspection report within 24 hours, so you have the
information you need while you're still making decisions about the property.

### What areas does AllCheck serve?
AllCheck Inspections serves Indianapolis and Central Indiana, including Avon,
Carmel, Fishers, Greenwood, and Noblesville.

### Can AllCheck test for radon, termites, or other issues at the same time?
Yes. AllCheck offers environmental testing alongside a home inspection,
including radon, termite, water, mold, and septic testing where applicable,
so you can address everything in one visit instead of scheduling separate
appointments.
```

Recommended FAQPage JSON-LD (developer: only publish if the visible on-page
text matches this exactly, per Google's FAQ structured data guidelines):

```json
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [
    {
      "@type": "Question",
      "name": "What does a home inspection in Indianapolis include?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "A full inspection covers the home's major systems and structure — roof, foundation, electrical, plumbing, HVAC, attic, and more — so you know the real condition of the property before you buy, sell, or maintain it."
      }
    },
    {
      "@type": "Question",
      "name": "How long does a home inspection take?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "Most inspections take a few hours. Larger homes, older homes, and homes with more systems to check usually take longer, since the inspector is covering more ground."
      }
    },
    {
      "@type": "Question",
      "name": "Should I attend my home inspection?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "Yes, when possible. Walking through the home with your inspector lets you see issues firsthand and ask questions on the spot, rather than reading about them later in a report."
      }
    },
    {
      "@type": "Question",
      "name": "How soon will I get my inspection report?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "AllCheck delivers every inspection report within 24 hours, so you have the information you need while you're still making decisions about the property."
      }
    },
    {
      "@type": "Question",
      "name": "What areas does AllCheck serve?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "AllCheck Inspections serves Indianapolis and Central Indiana, including Avon, Carmel, Fishers, Greenwood, and Noblesville."
      }
    },
    {
      "@type": "Question",
      "name": "Can AllCheck test for radon, termites, or other issues at the same time?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "Yes. AllCheck offers environmental testing alongside a home inspection, including radon, termite, water, mold, and septic testing where applicable, so you can address everything in one visit instead of scheduling separate appointments."
      }
    }
  ]
}
```

### E-E-A-T / trust content

> AllCheck Inspections has been inspecting homes across Indianapolis and
> Central Indiana for 18+ years. AllCheck also operates its own inspection
> training program, giving its team a level of hands-on, ongoing education
> most independent inspectors don't have access to.

Do not add a specific named inspector's certifications or bio to the homepage
yet — see the Waiting on Client item above regarding the "Jason Satterthwaite"
NACHI/homeinspector.org backlink signal. That belongs in a dedicated
About/inspector bio (Priority 3), not invented into homepage copy.

On the "604 reviews" figure: do not hardcode this number into new copy or
schema — it will be stale within weeks. If the homepage displays a review
count/rating, it should pull live from whatever plugin/integration already
connects to Google reviews, not a hand-typed figure.

### Image alt text (real files with real filenames, missing alt per audit)

| File | Recommended alt text |
|---|---|
| `.../2025/12/report.png` | Sample AllCheck Inspections home inspection report |
| `.../2025/12/payment-methods.png` | Accepted payment methods for AllCheck Inspections |
| `.../2025/12/sample-1.png` | Sample page from an AllCheck Inspections home inspection report |
| `.../2025/12/agents-2.png` | Real estate agents partnering with AllCheck Inspections |
| `.../2025/12/water-testing.jpg` | AllCheck Inspections water testing service in Indianapolis |
| `.../2024/05/informed-buyer1.png` | Homebuyer reviewing an AllCheck Inspections report |
| `.../2024/05/informed-seller.png` | Home seller preparing for an AllCheck Inspections pre-listing inspection |
| `.../2025/06/electrical-inspection.jpg` (both instances) | AllCheck inspector examining a home's electrical panel |
| `.../2025/05/Energy-Saving.jpg` (both instances) | Energy-saving upgrades identified during an AllCheck home inspection |
| `.../2024/05/logo3.png` | AllCheck Inspections logo |
| `.../2024/12/smaller-logo-2.png` | AllCheck Inspections logo |

The remaining 6 of the 18 flagged images are inline SVG/base64 data-URI
placeholders (not real content photos) — these are very likely
lazy-load/skeleton placeholders. Recommend `alt=""` (marks them decorative)
rather than inventing descriptive text for a placeholder graphic; developer
should confirm what these actually render as before finalizing.

### Performance — highest-leverage fix for developer

Audit shows 1.25MB of the 2.69MB page weight is JavaScript (vs. 0.63MB
images), and "All Page Scripts Complete" is the slowest metric at 5.3s.
**Recommendation: prioritize a JS/script audit (unused builder scripts,
render-blocking scripts) over image compression** — images are already a
smaller share of the problem. Also flagged by the audit: inline styles used
throughout (Avada/Fusion builder inline `style` attributes) — not a quick
content fix, logged here for the developer's technical backlog, not blocking
this content batch.
