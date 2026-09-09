# Local SEO Foundation

Status: **QA / Review** (content drafted below; NAP needs final client
confirmation against the live Google Business Profile before publishing).

## 1. NAP (Name, Address, Phone)

```
AllCheck Inspections
4519 N Franklin Rd Ste A
Indianapolis, IN 46226
317-202-3020
inspect@allcheck.biz
```

Source notes:
- Address is carried over from prior audit/engagement notes referencing the
  Google Business Profile. **This session has no live GBP or website access,
  so the address has not been independently re-verified here.** Flag as
  **Waiting on Client**: confirm this is still the exact current GBP address
  (including "Ste A") before it is published anywhere on the site or in
  schema.
- Phone `317-202-3020` is corroborated independently by the site's own audit
  crawl (visible in the header on both mobile and tablet renders in the SEO
  audit screenshots) — treat phone as **confirmed**.
- Email `inspect@allcheck.biz` is corroborated independently by the audit
  crawl (found in page source, line 505) — treat as **confirmed**. Note: the
  audit flags this address as exposed in plain text (see
  `TECHNICAL_URL_CLEANUP.md` performance/technical notes) — recommend the
  developer obfuscate it or route it through a contact form instead of a
  plain `mailto:` string, without removing the practical ability to email.
- The audit could not detect a physical address anywhere in the rendered
  homepage content. **Action:** display the NAP block above in the site
  footer (and/or a dedicated Contact section) once confirmed, not just in
  hidden schema.

## 2. NAP consistency sitewide

- [ ] Confirm the same NAP block (once verified) appears identically — same
      abbreviations, same suite formatting — in: site footer, `/contact-us/`
      page, and any location pages. Do not use "Suite A" in one place and
      "Ste A" in another.
- [ ] Confirm the GBP listing itself uses the identical formatting (this is a
      two-way consistency check, not just site-side).
- Owner: **Client/Developer** — this session cannot access the GBP dashboard
  or the CMS to check current rendering.

## 3. Service area wording

Primary market: Indianapolis and Central Indiana.

Known confirmed location-page targets (from `ALLCHECK_BRAND.md` and the
audit's own internal-link crawl, which shows live pages for all of these):
Indianapolis, Avon, Carmel, Fishers, Greenwood, Noblesville.

Recommended standard service-area sentence for reuse across homepage, footer,
and schema `areaServed`:

> "AllCheck Inspections proudly serves Indianapolis and Central Indiana,
> including Avon, Carmel, Fishers, Greenwood, and Noblesville."

Do not expand this list beyond confirmed location pages without a client
confirmation that AllCheck actively serves and wants to rank in a new city —
adding unserved cities to schema/copy is a GEO/trust risk (inaccurate entity
claim), not just an SEO one.

## 4. LocalBusiness / HomeAndConstructionBusiness schema

The audit's GEO section confirms `Organization` + `HomeAndConstructionBusiness`
identity schema already exists on the homepage, but flags that it (or the
visible page) does not include a physical address — "Contact Transparency"
notes phone, email, social profiles and contact forms are present, but no
address. Recommended JSON-LD to give the developer (merge into the existing
schema block rather than adding a second, conflicting schema object — the
audit already found duplicate/legacy schema risk is a real failure mode on
WordPress+Avada sites when a new SEO plugin adds its own block):

```json
{
  "@context": "https://schema.org",
  "@type": "HomeAndConstructionBusiness",
  "name": "AllCheck Inspections",
  "url": "https://allcheck.biz/",
  "telephone": "+1-317-202-3020",
  "email": "inspect@allcheck.biz",
  "address": {
    "@type": "PostalAddress",
    "streetAddress": "4519 N Franklin Rd Ste A",
    "addressLocality": "Indianapolis",
    "addressRegion": "IN",
    "postalCode": "46226",
    "addressCountry": "US"
  },
  "areaServed": [
    "Indianapolis, IN",
    "Avon, IN",
    "Carmel, IN",
    "Fishers, IN",
    "Greenwood, IN",
    "Noblesville, IN"
  ],
  "sameAs": [
    "https://www.facebook.com/AllCheck/",
    "https://instagram.com/allcheck_Inspections",
    "https://www.linkedin.com/company/allcheck-inspections/",
    "https://www.youtube.com/@AllCheckInspections",
    "https://pin.it/3QqSqu0jA"
  ]
}
```

Notes:
- `sameAs` URLs above are taken directly from the audit's own link crawl of
  the live homepage (confirmed currently linked from the site), not invented.
- **Do not add `aggregateRating` by copying the audit's "604 reviews"
  snapshot verbatim into permanent schema** — that number will drift out of
  date immediately. If review schema is wanted, the developer should pull the
  live current count/rating from the GBP-connected review plugin at
  implementation time, or use a plugin that keeps it live. Flagging this as
  **Waiting on Developer**.
- Do not add a second competing `LocalBusiness`/`Organization` block — audit
  explicitly reads this as one schema block already; adding a plugin-generated
  duplicate is a common WordPress failure mode and would create conflicting
  schema (CLAUDE.md rule 6 territory — protect what's already working).

## 5. Social / entity connections (verified via audit crawl)

| Platform | URL found in crawl | Status |
|---|---|---|
| Facebook | facebook.com/AllCheck | Linked, confirmed |
| Instagram | instagram.com/allcheck_Inspections | Linked, confirmed |
| LinkedIn | linkedin.com/company/allcheck-inspections | Linked, confirmed |
| YouTube | youtube.com/@AllCheckInspections | Linked, confirmed (audit notes low subscriber count — Priority 4 growth item, not a Priority 1 blocker) |
| Pinterest | pin.it/3QqSqu0jA | Linked, confirmed |
| X/Twitter | none found | Not present — per the source strategy doc, treat as very low priority; do not build solely to satisfy an audit score |

## 6. Items requiring client/developer input before this batch can be marked Done

- [ ] **Waiting on Client** — confirm exact current NAP against live GBP
- [ ] **Waiting on Developer** — implement/merge the JSON-LD above without
      creating duplicate schema
- [ ] **Waiting on Developer** — display NAP block in footer/contact area
- [ ] **Waiting on Developer** — de-expose the plain-text email or route
      through a form
