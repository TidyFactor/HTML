---
name: tidyfactor-html
description: "TidyFactor HTML track — 100% static HTML/CSS/JS platform starter with Contextual Decision Layer (CDL). Built for zero server runtime, free/shared hosting (GitHub Pages, Cloudflare Pages, Netlify, cPanel), and Web Components. Trigger on commands 'brief', 'init', 'compo', 'pages', 'assets', 'store', 'modules', 'i18n', 'seo', 'deploy', or requests like 'start a new static site', 'scaffold a static project', 'convert to plain HTML', 'componentize static site', 'prep for GitHub Pages'. Anti-triggers: Do NOT use for server-side databases or backend apps."
---

# TidyFactor HTML (Content-First Static Platform Starter)

A command dispatcher for 100% static HTML/CSS/JS web platforms. This router declares commands and workflows without performing execution directly.

## Commands

| User intent | Command | What it loads |
|---|---|---|
| Strategic Static Discovery & Brief Resolution | `references/commands/brief.md` | `references/workflows/brief.md` + `references/memory/decision-points.md` + `references/memory/quality-bar.md` |
| Primary deliverable — scaffold a new static site | `references/commands/init.md` | `references/workflows/init.md` + `references/memory/architecture.md` |
| Componentization & Web Components partials | `references/commands/compo.md` | `references/workflows/compo.md` + `references/memory/architecture.md` |
| Add new content pages / blog articles | `references/commands/pages.md` | `references/workflows/pages.md` + `references/memory/architecture.md` |
| Asset hygiene, favicon, and SVG optimization | `references/commands/assets.md` | `references/commands/assets.md` + `references/memory/quality-bar.md` |
| JSON / Markdown client-side content stores | `references/commands/store.md` | `references/commands/store.md` + `references/memory/decision-points.md` |
| Zero-build ES Modules & utility helpers | `references/commands/modules.md` | `references/commands/modules.md` + `references/memory/architecture.md` |
| Multilingual translation & Arabic RTL formatting | `references/commands/i18n.md` | `references/commands/i18n.md` + `references/memory/quality-bar.md` |
| SEO metadata, OpenGraph tags, sitemap generation | `references/commands/seo.md` | `references/commands/seo.md` + `references/memory/quality-bar.md` |
| Prepare deployment (GitHub Pages, Cloudflare, cPanel) | `references/commands/deploy.md` | `references/workflows/deploy.md` + `references/memory/quality-bar.md` |

Read only the command file that matches the request. Do not load all commands simultaneously.

## Non-Negotiable Invariants

1. **Contextual Decision Layer (CDL)**: Resolve static baselines via `/brief` or `.tidyfactor/html-brief.md` before emitting code.
2. **Zero Server Runtime**: Deliverable runs directly from static storage without Node, PHP, or database servers.
3. **Clean Relative Paths**: Never output absolute workstation drive paths (`file:///C:/...`). Use root-relative or relative links.
4. **Semantic HTML5**: Use proper semantic tags (`header`, `nav`, `main`, `section`, `footer`) and heading hierarchy.
5. **7-Axis Pre-Emit Critique**: All generated pages must be evaluated with `/* Pre-emit critique: P5 H5 E5 S5 R5 V5 D5 */`.
