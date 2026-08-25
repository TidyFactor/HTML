# Workflow: compo

Builds reusable native Web Components or modular HTML snippets with zero build step.

---

## Steps

1. **Define Web Component**:
   - Create class extending `HTMLElement` and register via `customElements.define()`.

2. **Mount & Export**:
   - Import component script in `js/main.js` and insert `<custom-tag>` into markup.

3. **Pre-Emit Self-Critique**:
   - `/* Pre-emit critique: P5 H5 E5 S5 R5 V5 D5 */`

---

## Validation checklist

- [ ] Component extends `HTMLElement` with valid custom element name (contains hyphen).
- [ ] No external bundler required to execute component.
- [ ] Pre-emit critique stamp included.
