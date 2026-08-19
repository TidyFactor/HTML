# Command: `pages` — Page Assembly

## Purpose
Turn each route into a thin file that assembles components (`compo`) and
data (`store`) — no page should contain raw repeated markup once this
command has run.

## When to run it
- After `compo` and `store` exist for the content on that page.
- User says "clean up my pages", "generate a page per product", or runs
  `pages`.

## What it does
1. **Static pages** (about, contact, home): a source file under `/pages/`
   containing only its unique content plus include tokens / component
   tags for shared chrome (header, nav, footer).
2. **Generated pages** (one per data item — products, posts): a single
   *template* page plus a `store`-sourced collection; build-time mode
   loops the template over the collection in `build.js`, writing one
   `/dist/<collection>/<slug>.html` per item. Runtime mode renders the
   list/detail view client-side from the fetched collection, with routing
   handled by a minimal hash-based or `history.pushState` router if
   multiple "pages" are needed without a server (see `modules.md`).
3. Every generated or static page gets a canonical URL structure decided
   once, up front, and applied consistently (`/products/slug.html` or
   `/products/slug/` — pick one, don't mix trailing-slash styles).
4. Hand off metadata specifics to `seo.md` — `pages` wires the *slots*
   (title, description placeholders) that `seo` fills in.

## Output convention
```
Build-time:
/pages/product-template.html   (source template)
/dist/products/blue-widget.html (generated, one per item)

Runtime:
/index.html + client-side router in /assets/js/modules/router.js
```

## Checklist
- [ ] No page contains markup that should have come from a `compo`
      partial/component instead
- [ ] Generated pages match one-per-data-item, zero manual duplication
- [ ] URL structure is consistent project-wide
- [ ] Title/description slots present on every page (filled by `seo`)
