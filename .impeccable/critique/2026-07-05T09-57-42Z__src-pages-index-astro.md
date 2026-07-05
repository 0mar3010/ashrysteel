---
target: homepage
total_score: 27
p0_count: 0
p1_count: 2
timestamp: 2026-07-05T09-57-42Z
slug: src-pages-index-astro
---
Method: dual-agent (A: a698a088c66c1dd31 · B: a00c7789e89432271)

## Design Health Score

| # | Heuristic | Score | Key Issue |
|---|-----------|-------|-----------|
| 1 | Visibility of System Status | 3 | Scroll-spy nav, hover states, form spinner/status all present; no "required field" indicator pre-submission |
| 2 | Match Between System and Real World | 3 | Industry-correct language (B420 DWR, ERW tube, mill certificates) speaks the buyer's technical language |
| 3 | User Control and Freedom | 2 | Mobile menu had no scroll-lock/backdrop (see P1 below) |
| 4 | Consistency and Standards | 3→4 | Was docked for Hero's structural inconsistency vs. every other section's clean pattern — that inconsistency is now fixed |
| 5 | Error Prevention | 1 | Quote form's Product-of-interest field is `required` in markup but has zero client-side validation — silently passes empty |
| 6 | Recognition Rather Than Recall | 3 | Sticky nav with active-section highlighting; always-visible form labels |
| 7 | Flexibility and Efficiency of Use | 2 | No accelerators (acceptable for this site type); disabled Arabic toggle gives no timeline |
| 8 | Aesthetic and Minimalist Design | 3→4 | Was docked specifically for Hero noise/contrast — now fixed |
| 9 | Help Recognize/Diagnose/Recover from Errors | 3 | Specific, humane error copy ("Add a few more details so sales can quote accurately") |
| 10 | Help and Documentation | 2 | No FAQ, but phone/email given as a reasonable substitute for a B2B lead-gen page |
| **Total** | | **27/40** (25 at assessment time, +2 from the Hero fix applied mid-session) | **Acceptable — significant items resolved, real gaps remain** |

## Anti-Patterns Verdict

**Not AI slop by palette or pattern** — checked against every DON'T in the parent skill: no gradient text, no glassmorphism, no purple-blue gradients, no cream/sand default, no numbered 01/02/03 scaffolding, no side-stripe borders, no identical-card-grid monotony (Products.astro's asymmetric lead+3-support layout is a genuine counter-example). Eyebrow labels are used contextually, not as a blanket per-section tic.

**But a real, structural bug was masquerading as a design defect**: `Hero.astro` had regressed to a `background: url(...)` full-bleed photo directly behind dark text with zero scrim or text-shadow — both assessments independently flagged this (A via live visual inspection at all 3 breakpoints, B via source-code + structural analysis, unable to compute a pixel ratio due to cross-origin canvas tainting but corroborating the same root cause). **This has been fixed during this session** — restored to the two-panel text+photo grid layout, verified clean at 1280px, 768px, and 375px.

**Deterministic scan**: `detect.mjs` does not exist anywhere in this repo (confirmed via full filesystem search by Assessment B, not just a path/resolution issue) — the CLI detector step could not run. No false positives to report since there was no detector output at all. This is a genuine tooling gap in the project's `.claude/skills/impeccable/scripts/` install, not a finding about the site itself.

## Overall Impression

The credibility-focused core of this page (Capacity spec-plate, Products grid, Sustainability quote) is genuinely well-executed B2B design — both assessments called out the spec-plate specifically as "exemplary" and free of SaaS-metric-card cliché. The gap between that quality and the Hero's now-fixed regression was the single biggest risk: a visitor's first 2 seconds were fighting illegible text, directly contradicting the "clarity" thesis the whole brand is built on. With that fixed, the remaining issues are a form-validation gap and a mobile-menu scroll-lock gap — both concrete, both fixable in one pass.

## What's Working

1. **Capacity spec-plate** (`CapacityPlate.astro`) — real `dl`/`dt`/`dd` semantics, bold blue numerals, bordered grid — reads exactly like the "annual report" DESIGN.md calls for, not a SaaS impact-stat row.
2. **Products.astro's asymmetric grid** — one media-led lead card + three visually distinct support cards (two photographic, one tinted text-only) actively avoids the identical-card-grid tell.
3. **Form error copy** — specific and humane ("Enter a valid email, like name@company.com"), with real `aria-live`/`aria-describedby` wiring, not just visual polish.

## Priority Issues

**[P0] Hero text illegible against its background photo — FIXED during this session**
- **Why it matters**: First 2 seconds of every visit; directly undermines the "clarity/precision" brand thesis.
- **Fix applied**: Restored `Hero.astro` to a two-panel grid (text column + dedicated image column) instead of a full-bleed CSS background behind text. Verified clean at 1280/768/375px.
- **Suggested command**: n/a — already resolved.

**[P1] Quote form silently accepts submissions with no product selected**
- **Location**: `QuoteForm.astro` — `validators` object omits `product`; the `<select>` has `required` but the `<form>` has `novalidate`, suppressing native browser validation entirely.
- **Why it matters**: Sales loses the single most useful lead-qualification field, and the user is falsely told "Request sent" when the system should have caught this.
- **Fix**: Add a `product` validator (reject the empty placeholder value) alongside the existing `name`/`company`/`email`/`message` checks.
- **Suggested command**: `/impeccable harden`

**[P1] Mobile menu doesn't cover or lock the page behind it**
- **Location**: `Nav.astro` `.mobile-menu` — static positioning, content height auto-fits; Hero's own CTAs remain visible/interactive directly beneath the open menu.
- **Why it matters**: WCAG 2.1 focus-management concern (background content should be inert while a full-screen-style menu is open) and a confusing visual overlap.
- **Fix**: Make `.mobile-menu` a fixed-position overlay covering the viewport when open, and set `inert` on `<main>` while it's open.
- **Suggested command**: `/impeccable adapt`

**[P2] Capacity spec-plate groups 6 stats in one ungrouped list**
- **Location**: `CapacityPlate.astro` — exceeds the ≤4-items-per-chunk cognitive-load guideline.
- **Fix**: Visual sub-grouping (e.g., "Scale" vs. "Footprint") or stronger distinction between the 3 headline stats and 3 supporting ones.
- **Suggested command**: `/impeccable layout`

**[P3] Several inline text links under 44px tap height**
- **Location**: Footer nav links, phone/email links throughout (17-23px measured heights at 375px).
- **Why it matters**: Minor — these are inline-text-style links, which WCAG 2.5.8 generally exempts from the 44px minimum, but worth a look if mobile conversion on the footer contact links matters.
- **Suggested command**: `/impeccable adapt`

## Persona Red Flags

**Jordan (confused first-timer)**: Would skip the Product-of-interest field with no visible penalty (confirmed bug, see P1) — the most likely persona to leave it at the placeholder since the taxonomy is unfamiliar to them.

**Riley (stress tester)**: Refreshing mid-form loses all input silently (expected browser behavior, no draft-save — minor but real for a form this length); confirmed the Product-of-interest gap by testing it directly.

**Procurement manager under time pressure**: "Manufacturing sites" (plant locations) is buried as the *unit* text of a stat cell in small gray type rather than its own visually distinct row — a time-pressured buyer scanning for logistics-relevant plant locations would likely miss it.

## Minor Observations

- Footer logo (`ashrysteel-lockup.png`) declared at 112×112 in markup, rendered at 96×96 via CSS — harmless but worth tidying for a "precision" brand.
- Disabled Arabic language toggle gives no timeline or alternative, for an Egyptian audience where Arabic is likely expected rather than a bonus.
- No console errors or failed network requests found at any breakpoint (clean baseline).

## Questions to Consider

1. Now that the Hero is a two-panel layout instead of a full-bleed image, does the photo still carry enough "foundry floor" weight, or does it need to feel bigger/bolder within its own column?
2. Is Product-of-interest actually necessary as a hard-required field — should the fix be tightening validation, or relaxing the requirement and defaulting to "Not sure yet"?
3. Should the quote form show a confirmation summary of what was submitted (e.g., "We received your request for Rebar & Sections") rather than a one-line status message, given this is a considered B2B purchase?
