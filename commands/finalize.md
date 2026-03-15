# /finalize Command

**Trigger words:** `/finalize`

## Usage

```
/finalize [page-number] [session-id]
```

## Parameters

- `page-number` (optional) — which variation to finalize, e.g. `3`. If omitted, the skill asks.
- `session-id` (optional) — 6-character session ID. If omitted, auto-resolved from context or file scan.

## What It Does

Invokes the `finalize` skill:

1. Resolves the session ID and confirms the selected variation
2. Collects brand constraints (color, font, headline, CTA, images)
3. Refines the prototype with real copy and brand styles
4. Adds SEO and Open Graph meta tags
5. Migrates the page to the final route (default: `/`)
6. Deletes all temporary gallery files
7. Runs an acceptance check

## Prerequisite

Must be run after `/gallery` (and optionally `/redesign`) has completed.
