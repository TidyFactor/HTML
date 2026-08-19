# Command: `modules` — Vanilla JS Modules

## Purpose
Extract client-side behavior (form validation, nav toggle, filtering,
routing) into standalone, feature-scoped JS files — no bundler, no
framework.

## When to run it
- The audit shows one large `main.js`/inline script handling multiple
  unrelated behaviors, or repeated behavior logic across pages.
- User says "split up my JS", "organize my scripts", or runs `modules`.

## What it does
1. Identify each distinct behavior (nav toggle, form validation, filter
   UI, lightbox, router if using client-side routing from `pages.md`).
2. Build-time / general case: one IIFE or ES module per behavior under
   `/assets/js/modules/name.js`, loaded via `<script defer src="...">` (or
   `type="module"` if using real ES `import`/`export` — prefer this when
   the project already uses `<script type="module">` anywhere).
3. Runtime Web Components mode: a "module" and a "component" often
   collapse into the same file (the custom element *is* the module) —
   don't force an artificial split; only extract a separate module file
   for behavior that isn't tied to one specific custom element (e.g. a
   shared router, a global scroll-spy).
4. No global namespace pollution — each module exposes at most one
   intentional global (or none, if using real ES modules).
5. Wire the module into whichever page/component needs it explicitly; no
   "just in case, load it everywhere" scripts.

## Output convention
```
/assets/js/modules/nav-toggle.js
/assets/js/modules/form-validate.js
/assets/js/modules/router.js        (only if client-side routing is used)
```

## Checklist
- [ ] Each module has one clear responsibility
- [ ] No unintentional global-scope leakage
- [ ] Only loaded on pages/components that actually use it
- [ ] Consistent with the project's chosen componentization method
