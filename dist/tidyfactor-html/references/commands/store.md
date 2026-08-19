# Command: `store` — Content as Data

## Purpose
Move hardcoded, repeated, or list-like content (products, posts, team
members, FAQ entries, testimonials) out of markup and into structured
`/data/*.json` (or `/data/*.md` with front-matter for long-form content),
so pages become *generated from data* instead of hand-duplicated per item.

## When to run it
- The audit shows near-identical page/section blocks that differ only in
  content (product A vs. product B, post 1 vs. post 2).
- User says "move this to a database", "make this data-driven", "add a
  content file", or runs `store`.
- Note: this track has no server, so "database" always means a build-time
  or fetch-time JSON/Markdown file, never SQL/SQLite — that belongs on
  `tidyfactor-php`.

## What it does
1. Identify the repeating shape (e.g. every product has `name`, `price`,
   `image`, `slug`).
2. Define that shape as a JSON array in `/data/<collection>.json`, or as
   one Markdown file per item under `/content/<collection>/` with
   front-matter for long-form content (blog posts, articles).
3. Build-time partials mode: `build.js` reads the collection and loops
   `pages`' template over it to generate one static HTML file per item
   into `/dist` — hand this to `pages.md` for the generation-loop pattern.
4. Runtime Web Components mode: the relevant component `fetch()`s the
   JSON collection at runtime and renders items client-side — flag that
   this means content is invisible to crawlers unless paired with `seo`'s
   static-snapshot guidance, and prefer build-time mode for any
   content that needs to be indexable.
5. Never put secrets/API keys in `/data` — same rule as everywhere else on
   this track.

## Output convention
```
/data/products.json         (array of objects, one per item)
/content/blog/my-post.md    (front-matter + Markdown body, long-form)
```

## Checklist
- [ ] Content shape is consistent across all items in a collection
- [ ] No secrets or credentials in any `/data` or `/content` file
- [ ] Build-time mode: generated pages verified against the original
      hardcoded versions (zero content drift)
- [ ] Runtime mode: flagged to the user if the moved content needs to be
      search-indexable (crawler-invisible content is a real tradeoff, not
      a silent side effect)
