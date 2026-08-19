# Command: `assets` — Asset Hygiene

## Purpose
Consolidate and organize CSS/JS/images, and apply the performance basics
that matter most on a track with no server-side caching/compression
control (many free hosts serve files as-is).

## When to run it
- The audit shows inline `<style>`/`<script>` blocks, scattered image
  paths, or no cache-busting on updated assets.
- User says "clean up my assets", "fix caching", "speed this up", or runs
  `assets`. Always Phase 1 — run before `compo`/`pages` restructure on top
  of a messy asset base.

## What it does
1. Move all inline `<style>` into `/assets/css/`, all inline `<script>`
   (non-trivial ones) into `/assets/js/` — one concern per file, named for
   what it styles/does.
2. Cache-busting without a build step's hash pipeline: build-time mode
   appends a content hash query string (`style.css?v=<hash>`) computed by
   `build.js` from file contents; runtime mode uses a manually-bumped
   version string in a single `/data/version.json` referenced by every
   page — flag that this is manual and needs discipline.
3. Images: enforce `width`/`height` attributes (prevents layout shift),
   `loading="lazy"` on below-the-fold images, and flag any image over a
   reasonable size threshold (~200KB) for compression — don't auto-compress
   without checking the user wants that (lossy operation).
4. Consolidate near-duplicate CSS rules; don't invent a new naming
   convention — match BEM/whatever the project already uses.
5. Add `<link rel="preconnect">` for any third-party font/script origin
   already in use.

## Output convention
```
/assets/css/*.css
/assets/js/*.js
/assets/img/*
```

## Checklist
- [ ] Zero inline `<style>`/non-trivial inline `<script>` remaining
- [ ] Cache-busting mechanism in place and documented in README
- [ ] All images have explicit dimensions; below-fold images lazy-load
- [ ] No CSS/JS duplicated across files that should share one source
