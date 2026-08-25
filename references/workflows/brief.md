# Workflow: brief

Discovers and records core static site baselines (Component Model, CSS Strategy, Content Source, Deploy Target) using CDL.

---

## Steps

1. **Check Existing State**:
   - Inspect `.tidyfactor/html-brief.md` and `package.json` for existing configurations.

2. **Conduct Structured Discovery (Max 3 Questions)**:
   - If not specified, ask:
     1. **Componentization Model (H1)**: Native Web Components or Static Inline?
     2. **CSS Strategy (H2)**: Vanilla CSS custom properties or Tailwind CDN?
     3. **Deploy Target (H4)**: GitHub Pages, Cloudflare Pages, or cPanel?

3. **Record Decisions**:
   - Save `.tidyfactor/html-brief.md` with confirmed parameters.

4. **Report Summary**:
   - Confirm baseline parameters and prompt user to invoke `/init` or `/pages`.

---

## Validation checklist

- [ ] `.tidyfactor/html-brief.md` exists and contains confirmed values for H1–H5.
- [ ] No more than 3 questions were asked in a single round.
- [ ] Static baseline conforms to `references/memory/quality-bar.md`.
