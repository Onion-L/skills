# /redesign Command

**Trigger words:** `/redesign`

## Usage

```
/redesign [page-numbers] [session-id]
```

## Parameters

- `page-numbers` (optional) — which variations to redesign, e.g. `1`, `3 and 5`, `all`. If omitted, the skill lists current variations and asks.
- `session-id` (optional) — 6-character session ID from a previous `/gallery` run. If omitted, auto-resolved from context or file scan.

## What It Does

Invokes the `redesign` skill:

1. Resolves the session ID
2. Loads `directions.json` to see what has already been used
3. Lists current variations and asks which to redesign
4. Proposes new directions that haven't been used before (waits for approval)
5. Updates `directions.json`
6. Rebuilds only the selected pages
7. Updates the gallery navigation page

## Prerequisite

Must be run after `/gallery` has completed at least once.
