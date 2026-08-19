# Command: `deploy` — Free-Hosting Launch

## Purpose
Get the finished static output live on a free/shared host correctly —
right folder pushed, headers set where the host allows it, HTTPS on,
custom domain wired, a real 404 page instead of the host's default.

## When to run it
- Always last (Phase 4, after `seo`).
- User names a target host, says "deploy this", "get this live", "prep
  for GitHub Pages/Netlify/Cloudflare Pages/cPanel", or runs `deploy`.

## What it does
1. Identify the target host (ask if not given — the checklist differs):
   - **GitHub Pages**: confirm `/dist` (or repo root) is the configured
     Pages source; add `CNAME` file if a custom domain is used; note
     Pages has no custom headers file — cache-busting must rely on the
     `assets.md` query-string approach, not HTTP headers.
   - **Netlify / Cloudflare Pages**: add a `_headers` file for
     cache-control on `/assets/*` (long cache, since filenames are
     versioned) and a `_redirects` file for the 404 page and any legacy
     URL redirects.
   - **Vercel (static)**: `vercel.json` with a `headers` block equivalent
     to the above; confirm no serverless functions crept in — this track
     is static-only.
   - **cPanel / shared free hosting**: `.htaccess` for cache headers and
     the 404 page; confirm the deployed folder is `public_html` (or the
     configured document root), and that `dist/` (build-time mode) is
     what actually gets uploaded, not the source tree.
2. Confirm HTTPS is enabled (most of these hosts auto-provision it; flag
   if the domain isn't yet pointed correctly for it to issue).
3. Add a real, on-brand `404.html` — not the host's default error page.
4. Final pre-launch check: `sitemap.xml`/`robots.txt` reference the live
   domain (not `localhost` or a placeholder), all internal links are
   relative or use the final canonical domain consistently.

## Output convention
```
GitHub Pages:        CNAME (if custom domain)
Netlify / CF Pages:  _headers, _redirects
Vercel:               vercel.json
cPanel:               .htaccess
All:                  404.html
```

## Checklist
- [ ] Correct output folder confirmed as the host's deploy source
- [ ] Cache headers or query-string versioning in place for the host type
- [ ] Custom 404 page present
- [ ] HTTPS confirmed
- [ ] `sitemap.xml`/`robots.txt`/canonical URLs point at the live domain
