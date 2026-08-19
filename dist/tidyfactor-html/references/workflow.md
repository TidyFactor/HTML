# TidyFactor HTML — Workflow Discipline

Applies underneath every command in `commands/`.

## 1. Audit
- Map the file tree. Count: inline `<script>`/`<style>` blocks, repeated
  markup blocks (candidates for `compo`), hardcoded content that repeats
  across pages (candidates for `store`), pages without meta/OG tags.
- Report findings and the proposed target structure.
- **Stop for confirmation** before editing, unless told to proceed
  automatically.

## 2. Execute in batches
- One page / component / file group at a time — highest duplication or
  highest risk first.
- Never one giant diff across the whole repo in a single pass.
- Build-time partials mode: after each batch, actually run `node build.js`
  (or equivalent) and confirm the generated output matches expectations
  before moving to the next batch.

## 3. Verify
- Open (or describe) the affected pages — confirm no visual/functional
  regression.
- Report: files changed, files generated (build-time mode), remaining
  inline-script/style count, remaining hardcoded-content count.
- For Convert mode specifically: confirm nothing that required a server
  (form POST handlers, session state, DB reads) got silently dropped —
  flag it instead, it doesn't belong on this track.

## Mode-specific notes

**Init** — audit step is replaced by the Step 0 questions in `SKILL.md`;
everything else (execute in batches, verify) still applies once files
start being generated.

**Convert** — audit the *source* project first (what's actually there:
static HTML already, SPA, PHP, WordPress export, etc.) before proposing
the target structure. Flag anything server-dependent as out of scope
rather than trying to fake it client-side.

**Improve** — audit is the primary deliverable if the user just wants a
report; only move to execute once they confirm which findings to act on.
