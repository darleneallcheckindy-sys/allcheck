# Row 11 - Duplicate H1 Audit

URL: https://allcheck.biz/
Task: Remove duplicate H1 tags

Goal:
Ensure the homepage outputs exactly one H1 while preserving the strongest
existing organic relevance and current visual design.

Important:
Do not change H2/H3 hierarchy in this task.
Do not rewrite unrelated homepage copy.
Do not make live changes unless CMS access exists.

## Data source disclosure — read before using this file

This session has **no live HTML capture, no rendered DOM access, and no CMS
access** to allcheck.biz (confirmed: no network egress to the live site from
this environment, checked again for this task). The only real source of
"every element currently outputting `<h1>`" is the third-party Digicorns SEO
audit's server-side HTML crawl (`66285dc1-report__allcheck.pdf`, provided
earlier in this session), which recorded exactly this H1 table:

| TAG | VALUE |
|---|---|
| H1 | *(blank)* |
| H1 | ✓HOME INSPECTORS IN INDIANAPOLIS YOU CAN TRUST |
| H1 | *(blank)* |

That crawl captures server-rendered HTML (what ships in the page source,
including any Avada responsive-duplicate markup that exists in the DOM
regardless of which breakpoint's CSS shows it), but it is a single crawl —
it cannot tell us which Avada module each H1 belongs to, whether an empty H1
is a logo wrapper vs. an unused Title element, or which one is
desktop-vs-mobile. Those specifics require either live CMS access (Avada
Builder) or a fresh rendered-HTML capture, neither of which exists in this
session. Everywhere below that depends on that missing detail is marked
**Needs CMS inspection** rather than guessed.

Per Step 1's instruction, real GSC data (not the old audit's ranking claims)
is used for the keyword-protection judgment in this file — see the
correction note in the Keyword Protection Check section.

## H1 Inventory

| # | H1 Text | Page Section | Visible? | Desktop/Mobile/Both | Source Element | Notes |
|---|---|---|---|---|---|---|
| 1 | *(empty — no text node)* | Unknown — position in DOM not captured by the audit crawl beyond "H1" tag order | Unknown — an empty heading renders no visible text but the element itself may still occupy layout space | Unknown — needs live inspection | Unknown — **Needs CMS inspection**. Common causes on Avada/WordPress homepages: (a) the site logo/header wrapped in an H1 for homepage-only SEO purposes, with no text fallback if the logo is image-only; (b) an Avada Title/Text element left with an empty title field; (c) a responsive-duplicate column (see Step 6) | Listed first in the crawl's H1 table, before the hero heading |
| 2 | `✓HOME INSPECTORS IN INDIANAPOLIS YOU CAN TRUST` | Hero section (the primary above-the-fold headline, based on wording and the fact this is the page's only H1 carrying real text) | Yes — visible | Unknown which specific breakpoint(s) render this exact node — **Needs CMS inspection** to confirm whether this is the shared hero heading or one of two duplicated hero headings | Hero Title/Text element (Avada) — inferred from content, not confirmed via CMS | Contains a stray leading `✓` character baked directly into the text node. This is almost certainly a checkmark/logo glyph that leaked into the heading text rather than staying in an adjacent icon element — see Step 5 |
| 3 | *(empty — no text node)* | Unknown, same caveats as #1 | Unknown | Unknown — needs live inspection | Unknown — **Needs CMS inspection** | Listed third in the crawl's H1 table, after the hero heading |

**Why there is more than one H1, to the extent this session can determine
it:** the page ships three H1-tagged elements in its server HTML. Only one
carries visible text (the hero headline). The other two are empty text
nodes tagged as H1 — which is a real, valid HTML tag in the DOM even though
nothing renders from them visually. The most likely explanations, in order
of plausibility for a WordPress + Avada site, are a homepage-only H1-wrapped
logo/header element (a known Avada/theme pattern) and/or a
responsive-duplicate section (the same module rendered twice — once per
breakpoint — with heading level left at H1 on both copies, only one of which
is visually shown at a given screen size via CSS). Both are template-level
issues, not content issues, and both require a developer to open the actual
Avada page in the CMS to confirm which explanation is correct — this cannot
be determined from a static crawl alone.

## Decision: which H1 stays

**Keep: `Home Inspectors in Indianapolis You Can Trust`** (the one
currently-visible H1, with the stray `✓` character removed from the text
node — see Step 5).

Reasoning, per Step 4's comparison criteria:
- **Actual homepage intent:** this is AllCheck's core "who we are, what we
  do, where" statement — it matches the page's actual purpose better than a
  blank heading could.
- **GSC query performance (real data, not the old audit):** see the
  Keyword Protection Check below — the phrase aligns closely with the
  single best real opportunity term found in this project's GSC data.
- **Current title tag:** `Home Inspectors Indianapolis | AllCheck
  Inspections` — the H1 and title share the core phrase ("Home Inspectors
  Indianapolis") without being identical, which is a healthy pattern, not a
  duplicate-content problem.
- **Natural wording:** reads as a real sentence, not keyword-stuffed.
- **Brand tone (`ALLCHECK_BRAND.md`):** "knowledgeable neighbor + licensed
  professional," reassuring and specific — "You Can Trust" fits that
  register without overpromising or using alarmist language.

Per Step 4's instruction: **this H1 is being kept, not rewritten**, because
it already aligns well with real ranking terms. This task does not propose
new wording for it — only removing the stray character and resolving the
two empty duplicates.

## Classification of every extra H1

| Current H1 | Keep? | New Tag | Reason | CMS Action |
|---|---:|---|---|---|
| *(empty H1 #1)* | No | Needs CMS inspection first, then likely `div`/`span` (if decorative/logo) or delete (if a genuine unused element) | An empty heading contributes no content or accessibility value and creates a second (blank) H1 in the DOM's heading outline, which is the exact duplicate-H1 problem this row exists to fix | Open the page in Avada, locate the element rendering as this empty H1 (check the logo/header area first, per the common pattern noted above), confirm what it actually is, then change its output tag to a non-heading element or remove it if truly redundant |
| `✓HOME INSPECTORS IN INDIANAPOLIS YOU CAN TRUST` (hero) | **Yes** | `h1` (unchanged) | This is the single H1 that should remain — see Decision above | Edit the text node only: remove the leading `✓` character so it reads `Home Inspectors in Indianapolis You Can Trust`. Do not change the tag, styling, or any other wording |
| *(empty H1 #2)* | No | Needs CMS inspection first, then likely `div`/`span` or delete | Same reasoning as empty H1 #1 | Same process as empty H1 #1 — inspect first, since this may be the responsive-duplicate twin of #1 rather than an unrelated element (see Step 6) |

## Responsive duplicate check (Avada)

This session cannot directly confirm which of the following is true — the
static crawl proves three H1 elements exist in server HTML, but not their
breakpoint visibility. Flagging the determination itself as **Needs CMS
inspection**, with the plausible scenarios ranked:

1. **Most likely, given there are exactly two empty H1s bracketing one real
   one:** the two empty H1s are a desktop/mobile (or similar breakpoint)
   duplicate pair of the *same* element — for example, a logo/header block
   that Avada renders twice (once per responsive container) with heading
   level left at H1 on both, and which happens to have no title text set in
   either copy. If confirmed, the fix is: **keep a semantic heading role on
   at most one logical version of that element (or none, if it's purely a
   logo and shouldn't be a heading at all), and make the other copy(ies)
   non-semantic** (`div`/`span`), per the task's stated preferred solution.
   Do not delete either responsive container outright if both are needed for
   layout — only change the *tag*, not the layout structure.
2. **Also possible:** the two empty H1s are unrelated elements (e.g., one a
   logo wrapper, one an unused Title module elsewhere on the page) rather
   than a responsive pair. This would change the CMS action from "make the
   duplicate non-semantic" to "independently resolve each one."
3. **Less likely but worth ruling out:** one or both empty H1s could belong
   to a global/reusable Avada template block (e.g., a shared header used
   across multiple pages), in which case a fix here could affect other pages
   too. If the developer finds this is the case, this should be flagged back
   before making the change, since it would expand this task's scope beyond
   the homepage.

**Do not delete a mobile/desktop layout container if it is needed for
layout** — per the task instructions, only the heading *tag* should change
on a redundant copy, not the container itself, unless the developer
confirms the container is truly unused.

## Keyword Protection Check

**Correction before this section: the existing `HOMEPAGE_BATCH.md` draft
states the homepage title "currently ranks #1 for its core term" — that
claim comes from the original third-party audit and has since been
disproven by real GSC data pulled in this project (see
`data/gsc/PROTECT_KEYWORDS.md`).** This check uses only the real, corrected
numbers.

- **Primary homepage query (real GSC, current 28-day period):**
  `home inspectors indianapolis` — position 4.37, 226 impressions, 6 clicks
  (improved from position 5.35 the prior period). This is the strongest real
  opportunity term found in this project's GSC data, and the one the H1
  wording most directly reflects.
- **Supporting query:** `home inspector indianapolis` (singular, position
  6.65, 75 impressions) and `home inspectors in indianapolis` (position
  4.64, 11 impressions) — close variants of the same phrase family the H1
  already covers.
- **Current H1 carrying relevance:** `Home Inspectors in Indianapolis You
  Can Trust` — contains the core phrase from all three queries above
  verbatim or near-verbatim.
- **Will relevance remain after H1 cleanup? Yes.** This task keeps the
  existing hero H1 text unchanged (aside from removing the stray `✓`
  character, which is not part of any query's relevance and only ever hurt
  clarity). Only the two empty, textless H1s are being addressed, and
  neither one carries any keyword relevance to remove — they have no text.
- **Notes:** Note that the real branded protect terms (`allcheck
  inspections`, `all check inspections` — see `data/gsc/PROTECT_KEYWORDS.md`)
  are **not** carried by the H1 text at all (the H1 doesn't contain
  "AllCheck"). That's fine — those terms are branded/navigational and are
  more likely driven by the title tag, page URL, and site-wide brand
  signals than by the H1 — but it means this H1 cleanup has no bearing on
  protecting those branded rankings either way. Separately, real GSC page
  data shows the homepage's ranking signal is currently split between
  `http://www.allcheck.biz/` (strong, position 3.71) and
  `https://allcheck.biz/` (weak, position 29.95) — this is the www/non-www
  technical issue already documented as the top priority in
  `tasks/PRIORITY_1_TECHNICAL_DEVELOPER_TICKET.md`. That issue is unrelated
  to H1 structure and is not affected by this task either way; it's noted
  here only so the two issues aren't conflated when interpreting future GSC
  changes.

## Developer / CMS Implementation Map

| Section | Current Tag | Current Text | New Tag | Text Change? | Exact Action |
|---|---|---|---|---|---|
| Empty H1 #1 (position 1 in DOM, per crawl order) | `h1` | *(none)* | `div` or `span` (pending CMS inspection — see Responsive Duplicate Check) | No | Open the homepage in Avada. Identify the element currently rendering as an empty H1 (check the logo/header area first). Confirm via the actual builder UI what module this is. If it's a logo/header element that doesn't need to be a heading, change its output tag to a non-heading element. If it's genuinely an unused, empty module, remove it. Do not touch layout/container structure unless confirmed unnecessary |
| Hero heading (position 2 in DOM) | `h1` | `✓HOME INSPECTORS IN INDIANAPOLIS YOU CAN TRUST` | `h1` (unchanged) | **Yes — remove the leading `✓` character only** | Open the Title/Text element containing this heading. Edit the text field to read exactly `Home Inspectors in Indianapolis You Can Trust`. Do not change font size, weight, color, spacing, alignment, or any other setting. Do not touch the H2/H3 structure of the rest of the page in this same pass |
| Empty H1 #2 (position 3 in DOM, per crawl order) | `h1` | *(none)* | `div` or `span` (pending CMS inspection) | No | Same process as Empty H1 #1. If CMS inspection confirms this is the responsive-duplicate twin of Empty H1 #1 (e.g., a mobile-breakpoint copy of the same logo/header block), apply the same tag change so neither copy remains a semantic H1 |

## Avada Notes

1. Open each relevant Title/Text element.
2. Check the HTML heading tag, not only visual typography.
3. Preserve font size, weight, spacing, and responsive styling.
4. For duplicate mobile/desktop sections, keep only one semantic H1.
5. Do not remove layout containers unless they are truly redundant.
6. Recheck rendered HTML after saving.

## Row 11 Validation Checklist

- [ ] Exactly one H1 remains in rendered homepage HTML
- [ ] The retained H1 matches homepage search intent
- [ ] No mobile/desktop duplicate H1 remains
- [ ] No visual styling was broken
- [ ] No important keyword relevance was accidentally removed
- [ ] Homepage title tag was not changed in this task
- [ ] H2/H3 restructuring was not started yet
- [ ] Final rendered HTML was rechecked

## Status

**Status: Ready for Implementation / Waiting on Developer.**

This task produced a complete audit and an exact implementation map, but
**no live CMS access exists in this session**, so nothing above has been
applied to the live homepage. Row 11 cannot be marked Done until a developer
(or someone with CMS access) makes the change in Avada and the rendered
HTML is rechecked to confirm exactly one H1 remains. Two items in the
implementation map are explicitly marked "pending CMS inspection" (the exact
identity of the two empty H1 elements) — a developer opening the actual
Avada builder should resolve those before executing the tag changes, since
this audit could only work from a static crawl, not the live builder.
