# Command: `seo` — Search & Share Metadata

## Purpose
Fill in the metadata layer that free static hosts don't provide for
you (no server-side redirect/canonical logic, no SSR meta injection) —
title/description per page, Open Graph/Twitter cards, structured data,
sitemap, robots.

## When to run it
- `pages` has finalized the page/URL structure (Phase 4, always after
  structure work, never before — metadata for pages that are about to be
  restructured just gets thrown away).
- User says "improve SEO", "add social preview cards", "generate a
  sitemap", or runs `seo`.

## What it does
1. Every page gets a unique `<title>` and `<meta name="description">` —
   filled from `store`'s data where the page is data-driven (product
   name/description), authored directly for static pages.
2. Open Graph (`og:title`, `og:description`, `og:image`, `og:url`) and
   Twitter card tags on every page — `og:image` should point to a real
   asset, not a missing placeholder.
3. `<link rel="canonical">` on every page, using the project's decided URL
   structure from `pages.md` — critical here since there's no server to
   enforce one canonical form.
4. Structured data (JSON-LD) where it clearly applies (Article, Product,
   Organization, BreadcrumbList) — don't force schema types that don't fit
   the content.
5. Generate/update `sitemap.xml` by walking the final `/dist` (or source)
   page tree, and `robots.txt` pointing to it.
6. Bilingual mode: cross-reference `i18n.md`'s `hreflang` requirement —
   `seo` is what actually adds it if `i18n` hasn't run yet.

## Output convention
```
/dist/sitemap.xml   (or /sitemap.xml in runtime mode)
/dist/robots.txt
Per-page: <title>, <meta description>, og:*, twitter:*, canonical, JSON-LD
```

## Checklist
- [ ] No two pages share an identical `<title>`
- [ ] Every page has a working `og:image`
- [ ] `sitemap.xml` matches the actual final page tree, no stale entries
- [ ] `robots.txt` present and correctly points to the sitemap
- [ ] Canonical URLs match the structure `pages.md` established
