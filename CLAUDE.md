# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A single-page marketing/credibility site for **ashrysteel**, an Egyptian steel manufacturer (est. 1983). The site's job is to convert B2B visitors (contractors, procurement managers, developers) into quote requests. Built with Astro, no UI framework, no CSS framework — plain scoped `<style>` blocks per component plus a shared token system.

## Commands

- `npm run dev` — start the dev server (port 4321)
- `npm run build` — runs `astro check` (type/template diagnostics) then `astro build`; treat a failing `astro check` as a real error, not noise
- `npm run preview` — serve the production build locally

There is no test suite and no linter configured — don't invent test commands.

## Source of truth for design decisions

**`PRODUCT.md`** (strategic: audience, brand personality, anti-references) and **`DESIGN.md`** (visual: color tokens, typography, elevation, named rules) at the project root are the living design spec. Read both before making any visual or copy change. They are overwritten in place as direction changes — there is no changelog of past directions, and old direction should never be resurrected without the user explicitly asking. `DESIGN.md`'s frontmatter carries the canonical hex values; `global.css` carries the same colors as OKLCH. If they ever drift, `DESIGN.md` is normative.

The current direction ("The Working Record") is cinematic/documentary photography-led, with Ashry Blue (`#0e2e61`, sampled directly from the company logo) as the **only** accent color in the entire system — no orange, no second hue, ever. `DESIGN.md`'s "One Accent Rule" and "Witnessed Rule" encode this; don't add a second color without re-reading it first.

`doc/ashrysteel.md` is a sourced research dossier (facilities, products, certifications, financials, leadership) with per-claim confidence ratings and a conflict log where sources disagree. Any new factual content on the site (capacity figures, certifications, employee counts) must be checked against it — several numbers there are explicitly flagged as unverifiable and should not be published (e.g. there is no verified ISO certificate number; don't invent one).

## Architecture

Single route (`src/pages/index.astro`) that composes one section per component, in order, inside `<Base>`:

`Nav → Hero → Products → CapacityPlate → Facilities → FieldRecord → Sustainability → QuoteForm → Footer`

- **`src/layouts/Base.astro`** — HTML shell, meta tags, imports `global.css` as an ES module (not a CSS `@import` — that was a deliberate perf fix; don't revert it), and owns the one piece of shared client JS: an `IntersectionObserver` that adds `.is-visible` to any `.reveal` element as it scrolls into view. Components opt into scroll-reveal by adding `class="reveal"` — no per-component JS needed.
- **`src/styles/global.css`** — all design tokens (`--color-*`, `--text-*`, `--space-*`, `--ease-*`) plus a handful of shared utility classes (`.container`, `.btn`/`.btn--primary`/`.btn--secondary`/`.btn--on-dark`, `.label`, `.section-heading`, `.section-lead`, `.stat`/`.stat__value`/`.stat__label`, `.section-pad`). Component-specific layout lives in each component's own scoped `<style>` block.
- **Component-local JS** lives in inline `<script>` tags inside the `.astro` file that needs it (see `Nav.astro` for the mobile-menu/scrollspy logic, `QuoteForm.astro` for client-side validation). There's no shared JS module system — each interactive component is self-contained.
- **Dark band**: `FieldRecord.astro` is the one deliberate dark-charcoal section on the page (`--color-charcoal`, not blue-tinted — that's intentional, see DESIGN.md's "Flush Photo Rule"/dark-band notes). Everything else is the light canvas. Don't add a second dark section without updating DESIGN.md first — the rhythm is meant to be one light/dark break, not a recurring pattern.
- **Images**: all photography is sourced from Unsplash by direct CDN URL (`images.unsplash.com/photo-<id>?auto=format&fit=crop&w=...`) with real `srcset`/`sizes`, verified to resolve (Unsplash's page-slug URLs and its CDN `photo-<id>` URLs are *not* the same ID format — if sourcing a new image, fetch the Unsplash photo page and read the actual `images.unsplash.com/photo-<id>` URL out of the page rather than guessing an ID from the slug). Brand assets (logo mark, lockup, favicon) are real files in `public/images/`.

## Known environment quirks (not code bugs)

- The dev server occasionally serves a **stale cached scoped `<style>` block** after a full-file rewrite (old CSS rules persisting alongside new markup, e.g. after using the `Write` tool to replace a component). A cache-busting query string reload usually isn't enough to fix it — stopping and restarting the dev server reliably does.
- `html { scroll-behavior: smooth }` is set globally. Any automated/scripted scroll (tests, tooling) should pass `behavior: 'instant'` explicitly, or reads of `window.scrollY` immediately after a scroll call will return a stale, mid-animation value.
