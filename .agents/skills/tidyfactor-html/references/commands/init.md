# Command: `init` — Project Scaffold

## Purpose
Generate a complete boilerplate for a brand-new project on the HTML
track — the only command that runs *before* there's a repo to audit.

## When to run it
- Mode is Init (Step 0).
- User says "start a new static site", "scaffold a project", "give me a
  boilerplate", or runs `init`.

## What it does
1. Confirm (ask if not given): project name, bilingual/RTL needed?,
   componentization method (build-time partials vs. runtime Web
   Components — see SKILL.md Step 0), target free host if known (affects
   `deploy` file placement later, not required now).
2. Create the folder structure (see Output convention).
3. Generate a minimal working homepage — not a placeholder wall of Lorem
   Ipsum, a real skeleton: header, nav, main, footer, one content section
   wired to `/data/site.json`.
4. Build-time partials mode: write `build.js` (zero dependencies, uses
   only Node's `fs`/`path`) that inlines `<!--#include partials/x.html-->`
   tokens and injects `/data/*.json` into pages, outputting to `/dist`.
   Add a `package.json` with only a `"build": "node build.js"` script —
   no dependencies field beyond that.
5. Runtime Web Components mode: write one example custom element
   (`/assets/js/components/site-header.js`) registered via
   `customElements.define`, loaded with `<script type="module" defer>`,
   demonstrating the pattern `compo` will repeat.
6. Add `robots.txt`, an empty `sitemap.xml` stub (real generation happens
   in `seo`), `.gitignore` (`/dist` if build-time mode), and a project
   `README.md` explaining the chosen method and how to build/preview
   locally.
7. Stop here — do not pre-build `compo`/`store`/`i18n` structure beyond
   the one working example; those commands grow the project as real
   content arrives.

## Output convention
```
Build-time partials mode:
/
├── partials/          (header.html, footer.html, nav.html)
├── pages/              (source pages, pre-build)
├── data/site.json
├── assets/{css,js,img}/
├── build.js
├── package.json
├── dist/               (generated — deploy this folder)
├── robots.txt
├── sitemap.xml
└── README.md

Runtime Web Components mode:
/
├── index.html
├── assets/js/components/site-header.js
├── assets/{css,img}/
├── data/site.json
├── robots.txt
├── sitemap.xml
└── README.md
```

## Checklist
- [ ] Componentization method confirmed and documented in README
- [ ] Homepage renders real structure, not lorem-ipsum filler
- [ ] Build-time mode: `node build.js` runs with zero installed
      dependencies and produces `/dist`
- [ ] No secrets, API keys, or server assumptions anywhere in the scaffold
- [ ] Bilingual/RTL scaffolded if requested (see `i18n.md` for the full
      dual-tree pattern — `init` only needs to set the `dir`/`lang`
      attributes and a placeholder dictionary file)
