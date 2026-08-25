# Memory: decision-points (Contextual Decision Layer — CDL v1.0)

A thin arbitration protocol for resolving static HTML site architecture, componentization, and deployment targets before code emission.

---

## 🏛️ Decision Matrix (H1–H5)

| Code | Decision Dimension | Options (Reference SSOT) | Default Fallback | Trigger / Ambiguity Condition |
|:---:|---|---|---|---|
| **H1** | **Componentization Model** | • `web-components` (Native `<custom-element>` runtime partials)<br>• `static-inline` (Single/multi-page pure HTML without runtime dependencies) | `web-components` | When prompt asks to componentize or reuse headers/navbars. |
| **H2** | **CSS Styling Strategy** | • `vanilla-css` (Scoped CSS custom properties & modern reset)<br>• `tailwind` (Tailwind CDN / standalone utility layer) | `vanilla-css` | When styling static markup. |
| **H3** | **Content Data Source** | • `json-store` (`data/content.json` loaded via fetch/ESM)<br>• `markdown-content` (Markdown files parsed client-side)<br>• `inline-html` (Direct semantic HTML text) | `inline-html` | When managing blog posts, catalogs, or multilingual text. |
| **H4** | **Deployment Target** | • `github-pages` (Zero configuration static GitHub Pages)<br>• `cloudflare-pages` (Global edge CDN static hosting)<br>• `cpanel-static` (Apache `public_html` static upload) | `github-pages` | When preparing deployment instructions or CI scripts. |
| **H5** | **Output Scope & Depth** | • `single-page` (Single static landing or brochure)<br>• `multi-page-site` (Multi-page platform with shared header/footer) | `single-page` | When prompt does not declare page count. |

---

## ⚡ Boolean Skip Conditions (Deterministic Bypass)

Skip interactive elicitation and proceed silently when ANY of the following are true:
1. **Cached Brief Exists**: `.tidyfactor/html-brief.md` exists.
2. **Explicit User Declaration**: Prompt explicitly declares component model and CSS (e.g. `"Build a multi-page static site with vanilla CSS and GitHub Pages"`).
3. **Direct Command Invocation**: User invokes explicit commands (`/compo`, `/pages`, `/i18n`, `/seo`).

---

## 💾 Brief Persistence Protocol

When `/brief` runs, save confirmed decisions to `.tidyfactor/html-brief.md`:
```markdown
# Static HTML Site Brief
- Component Model: [web-components | static-inline]
- CSS Strategy: [vanilla-css | tailwind]
- Content Source: [json-store | markdown-content | inline-html]
- Deployment Target: [github-pages | cloudflare-pages | cpanel-static]
- Scope Depth: [single-page | multi-page-site]
- Confirmed At: YYYY-MM-DD
```
