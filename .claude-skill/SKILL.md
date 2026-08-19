---
name: tidyfactor-html
description: TidyFactor HTML track — 100% static HTML/CSS/JS sites for free/shared hosting (GitHub Pages, Cloudflare Pages, Netlify, Vercel static, cPanel) with zero server runtime and zero mandatory build tooling. Trigger on commands "init", "compo", "pages", "assets", "store", "modules", "i18n", "seo", "deploy" (scaffolding, componentization, page assembly, asset/perf hygiene, JSON/Markdown content, JS modules, translation/RTL, SEO metadata, free-hosting deploy), or requests like "start a new static site", "scaffold a static project", "convert this to plain HTML", "componentize this static site", "make this bilingual", "prep for GitHub Pages/Netlify/Cloudflare Pages/cPanel", "audit this static site". Covers three modes — Init, Convert, Improve — and two componentization methods (build-time partials vs. runtime Web Components).
---

# TidyFactor HTML (Static HTML/CSS/JS → Free-Hosting-Ready Structure)

Part of the TidyFactor skill library (see `references/tidyfactor-vision.md` for
the shared philosophy). This skill covers the **HTML track**: no server
runtime at all, deployable to any free static host. Sibling tracks
(`tidyfactor-php`, `tidyfactor-vanilla-js`, `tidyfactor-micro-js`,
`tidyfactor-track-*`) live in their own skills — see "Related skills" below
for when to defer to them instead.

## Step 0 — Identify the mode (ask if not obvious)

Three lifecycle modes share this skill. If not obvious from the request or
the existing repo, ask once, briefly:

> "What are we doing?
> 1. **Init** — start a brand-new static project from scratch
> 2. **Convert** — bring an existing site, SPA, or other stack onto this
>    track (100% static, free-hosting-ready)
> 3. **Improve** — audit and upgrade a project that's already on this track"

For Convert and Improve, also identify (from the repo, or ask) which
**componentization method** applies — this changes what `compo`, `pages`,
`store`, and `i18n` actually produce:

- **Build-time partials** — a tiny zero-dependency Node script
  (`build.js`, no npm packages) inlines partials/data into plain `.html`
  files at build time. Output is still 100% static; the build step never
  ships to the host. Recommended default — real DRY components, real
  data-driven pages, still deploys anywhere static.
- **Runtime Web Components** — native `<template>` + `customElements` +
  `fetch()`, zero build step, edited directly on the host (e.g. cPanel file
  manager, no local tooling at all). Choose this only when the user
  explicitly cannot run any build/deploy step.

Don't guess silently between the two — ask if the project doesn't already
show one in use. Init mode: ask directly as part of scaffolding.

## Command Index

| Command | Purpose | Reference |
|---|---|---|
| `init` | Scaffold — new project folder structure, chosen componentization method, base files | `references/commands/init.md` |
| `assets` | Asset Hygiene — consolidate CSS/JS/images, cache-busting, perf basics | `references/commands/assets.md` |
| `compo` | Modular Components — extract repeated markup into partials or Web Components | `references/commands/compo.md` |
| `store` | Content as Data — move hardcoded content into JSON/Markdown, data-driven pages | `references/commands/store.md` |
| `pages` | Page Assembly — thin per-route files assembling components + data | `references/commands/pages.md` |
| `modules` | Vanilla JS Modules — feature-scoped IIFEs or custom elements, no bundler | `references/commands/modules.md` |
| `i18n` | Translation & RTL/LTR — centralized dictionaries, dual-tree pre-render for SEO | `references/commands/i18n.md` |
| `seo` | Search & Share Metadata — meta/OG/JSON-LD, sitemap.xml, robots.txt | `references/commands/seo.md` |
| `deploy` | Free-Hosting Launch — host-specific checklist, headers, HTTPS, 404 | `references/commands/deploy.md` |

New commands follow `references/commands/_template.md`.

## Command Sequencing & Phases

1. **Phase 1 — Foundation.** `assets` first — a clean, organized
   CSS/JS/image base makes every later command easier and catches perf
   issues before they get baked into components.
2. **Phase 2 — Structure & Data.** `compo` → `store` → `pages` → `modules`,
   in that order — components need to exist before pages assemble them,
   and data-driven pages need `store`'s data source in place first.
3. **Phase 3 — Scale.** `i18n` — only after `compo`/`pages` are stable, so
   translation work isn't scattered across markup that's about to move.
4. **Phase 4 — Launch.** `seo` then `deploy` — metadata and sitemap need
   final page structure to be accurate; `deploy` is always last.

Never run two commands "at the same time" — each finishes, gets verified,
and gets reported before the next starts. If the repo isn't ready for a
requested command (e.g. `i18n` before any `compo`/`pages` exist), say so
and suggest the prerequisite instead of forcing it through.

## Running a single command

1. Confirm mode (Step 0) and componentization method — a command's output
   shape depends on both.
2. Read the matching reference file in full before acting.
3. Do a scoped audit for just that command's concern.
4. Execute in small batches (one page/component/file group at a time).
5. Report using that command's checklist.

## Running a full mode end-to-end

- **Init**: run `init` (it scaffolds ahead of the phase order, then leaves
  the project ready for `compo`/`store`/`pages` as content grows).
- **Convert / Improve**: follow the Phase 1→4 order above in full.

Within each command, still follow the underlying audit → execute → verify
discipline in `references/workflow.md`.

## Hard constraints (apply to every command)

- Zero functionality/visual regressions — flag anything risky instead of
  guessing.
- Zero server-side runtime, ever — if a request needs one, it belongs on
  `tidyfactor-php` or another track, not here. Say so and hand off.
- Build-time partials mode: the build step is dev-only tooling — nothing
  the free host executes. Never introduce a bundler, framework, or npm
  dependency beyond Node's built-in `fs`/`path`.
- Runtime Web Components mode: zero build step, period — no compilation,
  no transpilation.
- Never hardcode secrets/API keys into any file — this track has no secure
  place to keep them; flag any integration that needs one as out of scope
  for pure static hosting.
- Preserve bilingual/RTL support (`dir="rtl"`, language switching) if
  present; match the project's existing naming/CSS convention instead of
  inventing a new one.
- Don't mix componentization methods within one project — pick one in
  Step 0 and apply it consistently.

## Two operating modes (execution style)

- **Mode A — do it directly.** Files are uploaded or accessible via
  `view`/`bash_tool`/`str_replace`/`create_file`. Run Step 0, then execute
  directly.
- **Mode B — generate a handoff prompt.** The user wants a copy-paste
  prompt for an external agent (Codex CLI, Claude Code, Cursor) instead.
  Still run Step 0 first so the prompt is scoped correctly. Build it from
  the matching `references/commands/<name>.md` file(s), injecting the
  chosen mode, componentization method, and (for Convert/Improve) the real
  file tree and hotspots found in a quick audit.

## Related skills

- Needs a server runtime, database, or auth → `tidyfactor-php` (or the
  relevant `tidyfactor-track-*` skill once available).
- Target is Webletz Core or a PocketOffice module specifically → defer to
  `webletz-core-architecture` / `pocketoffice-module-builder` for their
  locked project-specific architecture.
- General SPA/PHP/micro-framework refactor not scoped to the HTML track →
  `clean-code-refactor`.
