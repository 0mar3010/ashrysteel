---
name: ashrysteel
description: Editorial, documentary-photography-led B2B site for an Egyptian steel manufacturer — credibility through witnessed reality, not spec sheets.
colors:
  white: "#fbfcfe"
  ink: "#26272e"
  ink-dim: "#5c5f68"
  ink-faint: "#767a83"
  border: "#dfe1e6"
  ashry-blue: "#0e2e61"
  ashry-blue-deep: "#0a2249"
  charcoal-band: "#13161c"
  charcoal-band-deep: "#090b0f"
  ink-on-dark: "#e2e5e9"
  ink-on-dark-dim: "#a2a5aa"
  border-on-dark: "#303338"
  blue-on-dark: "#5b87c8"
typography:
  display:
    fontFamily: "Manrope, -apple-system, sans-serif"
    fontSize: "clamp(2.5rem, 1.6rem + 4.5vw, 5rem)"
    fontWeight: 700
    lineHeight: 1.08
    letterSpacing: "-0.01em"
  headline:
    fontFamily: "Manrope, -apple-system, sans-serif"
    fontWeight: 700
    lineHeight: 1.15
  body:
    fontFamily: "Inter, -apple-system, sans-serif"
    fontSize: "1.0625rem"
    fontWeight: 400
    lineHeight: 1.65
  label:
    fontFamily: "Inter, -apple-system, sans-serif"
    fontSize: "0.75rem"
    fontWeight: 600
    letterSpacing: "0.08em"
rounded:
  none: "0px"
  sm: "4px"
spacing:
  sm: "0.75rem"
  md: "1.5rem"
  lg: "3rem"
  xl: "6rem"
  2xl: "9rem"
components:
  button-primary:
    backgroundColor: "{colors.ashry-blue}"
    textColor: "{colors.white}"
    rounded: "{rounded.sm}"
    padding: "14px 32px"
  button-primary-hover:
    backgroundColor: "{colors.ashry-blue-deep}"
  link-arrow:
    textColor: "{colors.ashry-blue}"
  link-arrow-on-dark:
    textColor: "{colors.blue-on-dark}"
---

# Design System: ashrysteel

## 1. Overview

**Creative North Star: "The Working Record"**

ashrysteel's site is built like a documentary record of an industrial operation, not a marketing brochure and not an annual-report spreadsheet. The two directions already tried and rejected were a dark "committed navy" environment (too heavy, too close to a moody tech-startup dark mode) and a light "restrained corporate" system (too generic, too safe — indistinguishable from any B2B template). This third direction takes its cue from how a company like ArcelorMittal actually presents itself: cinematic, real photography carrying the weight of the story; flowing editorial copy instead of bullet-point marketing; restrained, light-weight numbers instead of shouted stats; and a deliberate rhythm of light and dark bands across the page instead of one flat canvas.

Credibility here comes from **witnessed reality** — real plants, real product, real projects, shown at scale and given room to breathe — not from a spec-sheet aesthetic or a corporate-safe palette. Ashry Blue (the real logo color) is the **only** accent color in the system: no orange, no amber, no second or third hue competing for attention. It marks interactivity and nothing else.

**Key Characteristics:**
- Cinematic full-bleed photography as the primary credibility device, not a supporting graphic
- Editorial paragraph copy — reads like a documentary caption, not ad copy
- Restrained, light-weight stat typography — large but quiet, never a shouting SaaS metric
- Asymmetric bento layouts mixing photo-blocks and text-blocks; filmstrip galleries instead of bordered card grids
- A deliberate light/dark band rhythm: mostly white, punctuated by a dark charcoal "in the field" section
- Ashry Blue as the sole accent — interactive states only, never decoration, never a second color introduced alongside it

## 2. Colors

### Primary
- **Ashry Blue** (`#0e2e61`): the exact logo navy. Used only for interactive elements — links, primary buttons, active states, arrows. Never a background block, never decoration.
- **Ashry Blue Deep** (`#0a2249`): hover/active state for Ashry Blue.
- **Blue on Dark** (`#5b87c8`): the same hue, lifted in lightness for use inside the dark charcoal band, where the deep navy itself would vanish against a near-black surface.

### Neutral (light band)
- **White** (`#fbfcfe`): primary page background.
- **Ink** (`#26272e`): primary text on light backgrounds.
- **Ink Dim** (`#5c5f68`): secondary/body text on light backgrounds.
- **Ink Faint** (`#767a83`): tertiary text, captions, metadata.
- **Border** (`#dfe1e6`): hairline rules and dividers on light backgrounds.

### Neutral (dark band)
- **Charcoal Band** (`#13161c`): the dark section background — a true neutral near-black, not a tinted-navy "environment" like the rejected dark direction. Reads as steel/iron, not as a mood-lit tech interface.
- **Charcoal Band Deep** (`#090b0f`): deepest layer within the dark band (e.g. carousel card overlays).
- **Ink on Dark** (`#e2e5e9`): primary text on the charcoal band.
- **Ink on Dark Dim** (`#a2a5aa`): secondary text on the charcoal band.
- **Border on Dark** (`#303338`): hairline rules within the dark band.

### Named Rules
**The One Accent Rule.** Ashry Blue is the only hue in this system besides neutrals. If a second color is needed for anything, the answer is a different weight or lightness of blue, or a neutral — never a new hue, never orange or amber.
**The Witnessed Rule.** Photography carries credibility, not color or iconography. When in doubt between a graphic device and a real photo, use the photo.

## 3. Typography

**Display Font:** Manrope (headlines, stat numbers)
**Body Font:** Inter (paragraph copy, labels, captions)

**Character:** Manrope's weight carries confidence in headlines without shouting; Inter's neutrality lets editorial paragraph copy read calmly at length. Numbers are set in Manrope but at a **lighter** weight than a typical SaaS metric — restrained, not a hero-metric callout.

### Hierarchy
- **Display** (700, `clamp(2.5rem, 1.6rem + 4.5vw, 5rem)`, tight line-height): the one big cinematic hero headline, used once per page.
- **Headline** (700, section-level): section headings, editorial-weight, `text-wrap: balance`.
- **Stat number** (500–600, large but not maximal): restrained emphasis — the number matters more than its size.
- **Body** (400, 1.0625rem, 1.65 line-height, ≤70ch measure): flowing editorial paragraphs, not bullet fragments.
- **Label** (600, 0.75rem, uppercase, 0.08em tracking): used sparingly — captions under photography, "read more" links — never as a kicker repeated above every section.

### Named Rules
**The Caption Rule.** Uppercase label type is for photo captions and read-more links, not for section eyebrows. If it's sitting directly above a heading on more than one section, remove it.

## 4. Elevation

Flat by default. No bordered-card-with-shadow as the default container — that reads as a SaaS dashboard, not a documentary record. Photography sits flush to its grid cell (no radius, no border) except where a small radius softens a UI control (buttons, form fields). Depth comes from the light/dark band rhythm and from real photographic depth, not from drop shadows.

### Named Rules
**The Flush Photo Rule.** Photography is never boxed in a bordered, shadowed card. It sits flush within its grid cell, edge to edge, or full-bleed.

## 5. Components

### Buttons
- **Shape:** 4px radius, not the large "SaaS card" radius used in the previous direction.
- **Primary:** Ashry Blue background, white text, 14px/32px padding.
- **On photography:** white or outline-white variant with suf­ficient scrim behind it — never dark text directly on an unscrimmed photo.

### Photo Galleries / Filmstrips
- Real photography in a horizontal strip or bento grid, no rounded corners, no card border, no shadow.
- Captions (if any) use Label type, sitting below or overlaid with a scrim — never competing with the image for attention.

### Stat Blocks
- A thin hairline rule above the block, the number in Manrope medium/semibold weight (not maximal boldness), a small caption below in Ink Dim.
- No bordered grid box per stat — let whitespace separate them.

### Dark Band Sections
- Charcoal Band background, Ink on Dark / Ink on Dark Dim text, Blue on Dark for interactive accents (arrows, read-more links).
- Used for exactly one purpose on this page: a case-study / "steel in the field" showcase, so the dark band stays a deliberate rhythm break, not a second competing environment.

## 6. Do's and Don'ts

### Do:
- **Do** let real photography fill the frame — full-bleed hero, flush filmstrip galleries, no decorative cropping into rounded cards.
- **Do** write section copy as flowing editorial paragraphs.
- **Do** keep stat numbers restrained — large, but quiet; a thin rule and a caption, not a bordered box.
- **Do** use exactly one dark charcoal band on the page for rhythm, and keep it truly neutral (not blue-tinted) so it doesn't become a second "environment."
- **Do** use Ashry Blue for every interactive element and nothing else.

### Don't:
- **Don't** introduce orange, amber, or any second accent hue anywhere on the site.
- **Don't** box photography in bordered, shadowed cards with large radius — that's the rejected SaaS-corporate look.
- **Don't** use a tiny uppercase eyebrow label above more than one section heading.
- **Don't** revert to the dark "Foundry Navy" full-environment direction, or the flat "Industrial Clarity" light-only direction — both were explicitly rejected.
- **Don't** use gradients, glassmorphism, or unscrimmed text directly on a busy photograph.
