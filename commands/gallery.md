# /gallery Command

**Trigger words:** `/gallery`, `/design-gallery`

## Usage

```
/gallery [project-path-or-prd]
/design-gallery [project-path-or-prd]
```

## Parameters

- `project-path-or-prd` (optional) — path to an existing codebase or PRD file. If omitted, the skill uses the current working directory.

## What It Does

Invokes the `design-gallery` skill:

1. Generates a session ID
2. Detects the tech stack
3. Analyses the project or PRD
4. Proposes 5 distinct design directions (waits for approval)
5. Writes `directions.json`
6. Builds 5 landing page variations at `/gallery/{id}/1–5`
7. Creates a navigation page at `/gallery/{id}`

## Output

A gallery index at `/gallery/{id}` linking to all 5 variations, plus a `directions.json` file for use by `/redesign` and `/finalize`.
