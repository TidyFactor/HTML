# Command: `compo` — Modular Components

## Purpose
Break repeated or logically-distinct markup blocks into reusable
components — the structural unit above "page" and below "module" (see
`modules.md` for the JS-behavior equivalent). This is the command that
makes real DRY components possible on a track with no native server-side
include.

## When to run it
- The audit shows the same block (header, nav, card, footer, testimonial,
  pricing table...) repeated across multiple pages/files.
- User says "componentize this", "make this modular", or runs `compo`.

## What it does — Build-time partials method
1. Identify each repeated/distinct UI block during audit.
2. Extract it into its own file under `/partials/name.html`.
3. Give it explicit inputs via simple token replacement — `build.js`
   supports `{{variable}}` substitution and `<!--#include partials/x.html
   var="value"-->` for parameterized includes. Don't invent a heavier
   templating syntax; keep the build script's grammar minimal and
   documented in the project README.
4. Name by what the block *is*, not where it's used (`product-card.html`,
   not `homepage-box-3.html`).
5. Replace the original inline markup in every page with the include
   token, then run the build and diff the output against the original
   rendered HTML to confirm zero visual change.

## What it does — Runtime Web Components method
1. Same identification step.
2. Extract into `/assets/js/components/name.js`, a custom element using
   `<template>` + Shadow DOM (or light DOM if the project's CSS needs to
   cascade in — match whatever the project's first example established).
3. Inputs become element attributes (`<product-card title="..." price=
   "...">`) read via `attributeChangedCallback` or `observedAttributes`.
4. Register via `customElements.define('product-card', ProductCard)`,
   loaded once via `<script type="module" defer>`.
5. Replace the original inline markup with the custom element tag in every
   page.

## Output convention
```
Build-time:  /partials/product-card.html
Runtime WC:  /assets/js/components/product-card.js  (defines <product-card>)
```

## Checklist
- [ ] No component contains hardcoded page-specific content it should
      take as an input/parameter instead
- [ ] Same visual output as before extraction (diff-checked)
- [ ] Named by purpose, not by page location
- [ ] Used in at least 2 places (single-use blocks may not need
      extraction yet — flag instead of forcing it)
- [ ] Componentization method matches what `init` (or the existing
      project) already established — never mix methods in one project
