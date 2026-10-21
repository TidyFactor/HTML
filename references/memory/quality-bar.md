# Memory: quality-bar (Static HTML Anti-Slop & Quality Gate)

Enforces 100% serverless static perfection, semantic HTML5, zero broken paths, and fast Lighthouse scores.

---

## 🛡️ 7-Axis Pre-Emit Self-Critique Stamp

Every generated static page, component, or config must be stamped:
`/* Pre-emit critique: P5 H5 E5 S5 R5 V5 D5 */`

| Axis | Dimension | Score 1 (Slop / Reject) | Score 5 (Production Pass) |
|:---:|---|---|---|
| **P** | **Philosophy & Zero Runtime** | Requires Node runtime, SSR, or backend server to view. | 100% static HTML/CSS/JS; runs by double-clicking or uploading to cPanel. |
| **H** | **HTML5 Semantics & Structure** | `<div>` soup; missing `main`, `header`, `nav`, `section`, `footer`. | Semantic HTML5 structure with proper heading hierarchy (`h1` -> `h2` -> `h3`). |
| **E** | **Encapsulation & Links** | Absolute workstation paths (`file:///C:/...`) or broken relative links. | Clean relative links (`./css/style.css`, `../assets/icon.svg`). |
| **S** | **SEO & Agentic Readiness** | Missing OpenGraph tags, no `llms.txt` discovery, non-semantic div-buttons causing agent click failures. | Complete OpenGraph, Twitter Cards, canonical URL, `/llms.txt` discovery tag, and accessible semantic controls for AI agents. |
| **R** | **RTL & Internationalization** | Hardcoded text in markup preventing localization; broken RTL. | `dir="rtl"` / `lang="ar"` support with CSS logical properties (`margin-inline`). |
| **V** | **Velocity & Asset Hygiene** | Uncompressed 5MB hero images; blocking render scripts; layout shifts (CLS > 0.1). | Optimized SVGs, WebP images with explicit width/height (CLS ≤ 0.05), deferred scripts. |
| **D** | **Decision Alignment** | Inconsistent foundation ignoring `.tidyfactor/html-brief.md`. | 100% compliant with confirmed Component Model and CSS strategy. |
