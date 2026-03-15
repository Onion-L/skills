# directions.json

## File Format

```json
{
  "sessionId": "{id}",
  "directions": [
    { "page": 1, "name": "Dark & Bold", "description": "High contrast dark palette with split-screen hero and bold typography." },
    { "page": 2, "name": "Minimal Clean", "description": "Lots of whitespace, single-column layout, understated type." },
    { "page": 3, "name": "Glassmorphism", "description": "Frosted blur surfaces, asymmetric overlapping cards." },
    { "page": 4, "name": "Corporate Pro", "description": "Muted professional palette, grid-based layout with sidebar." },
    { "page": 5, "name": "Vibrant Playful", "description": "Expressive gradients, full-bleed sections, large visuals." }
  ]
}
```

## Path Rule

`{output_root}/gallery/{id}/directions.json`

## Write Rules (design-gallery)

- Write `directions.json` **immediately after the user approves** the 5 directions — before generating any pages.
- Confirm to the user: `"Directions saved."` once written.
- Do not duplicate directions: this file is the authoritative history of all directions used.

## Read Rules (redesign)

- Read `directions.json` as the first action before proposing anything. Do **not** rely on session memory alone.
- This file determines which directions are off-limits for new proposals.
- Never propose a direction that appears anywhere in `directions.json`, even if that page was later redesigned.

## Update Rules (redesign)

- Immediately after the user approves new directions, replace the entries for redesigned pages in `directions.json` before writing any code.
- Keep entries for unchanged pages exactly as they were.
- This keeps `directions.json` as the single source of truth at all times.
