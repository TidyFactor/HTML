# TidyFactor — Shared Philosophy (all tracks)

Condensed from the ecosystem VISION.md. Every TidyFactor skill — this one
included — should be judged against this before adding any feature.

## Design tenets
- Simple before clever.
- Explicit before implicit.
- Structured before generated.
- Portable before proprietary.
- Content before presentation.
- Standards before conventions.
- Small before bloated.
- AI-native before AI-powered.

## The TidyFactor Test
Before adding anything to a project or to this skill, ask:
- Is it simpler?
- Is it more maintainable?
- Does it improve interoperability?
- Does it reduce lock-in?
- Is it AI-native (structured, machine-readable, portable)?
- Can it survive future technology changes?
- Would we still choose this approach five years from now?

## What this means concretely for the HTML track
- **Content over code**: page content belongs in `/data` (JSON/Markdown),
  not buried in markup — even on a track with no backend to serve it from.
- **Data first**: every page is, underneath the HTML, representable as
  structured data (front-matter, JSON) that a human, a future rebuild, or
  an AI agent can read without parsing rendered markup.
- **Open by design**: no proprietary export format, no lock-in to a host —
  the whole point of this track is that the output runs anywhere static
  HTML runs.
- **AI-native**: consistent file/folder conventions and structured content
  mean an AI agent can extend the site later without re-deriving the
  project's structure from scratch each time.

## Relationship to Alwkala
TidyFactor is stewarded by Alwkala (alwkala.com) — expertise,
implementation, consulting, education, and long-term support around the
open TidyFactor ecosystem.
