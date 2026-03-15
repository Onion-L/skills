---
name: design-gallery
description: Generates 5 landing page design variations from an existing project or PRD document, then creates a /gallery/{id} navigation page to compare them. Combines UI/UX design analysis with frontend implementation. Use when the user wants to explore multiple design directions for a landing page.
---

# Design Gallery

Generate 5 distinct landing page UI variations from a project or PRD, then produce a `/gallery/{id}` navigation page to browse and compare them all.

## When to Use This Skill

- User provides an existing project codebase and wants landing page design options
- User provides a PRD document and wants to visualise design directions
- User says "generate design variations", "show me different landing page styles", or "design gallery"

---

## Workflow

### Step 0 — Generate Session ID

See [lib/session.md](../../lib/session.md) — Session ID Generation

Use this ID as a namespace for all routes in this run:

- Gallery index: `/gallery/{id}` (e.g. `/gallery/a3f9k2`)
- Pages: `/gallery/{id}/1` through `/gallery/{id}/5`

---

### Step 1 — Understand the Input

Determine what the user has provided:

**If the input is a PRD file only (no existing code):**
> "I only see a PRD document here. Would you like to choose your own tech stack, or should I default to **Next.js + Tailwind CSS**?"
- Wait for the user's answer before proceeding.

**If the input is an existing codebase:**

See [lib/stack-detection.md](../../lib/stack-detection.md)

**Check for existing gallery routes before writing anything:**
- Check whether `/gallery/{id}/1` through `/gallery/{id}/5` already exist as files or routes.
- If any of them already exist, **stop and inform the user** — do not silently overwrite.

Do not proceed until the stack and output location are confirmed.

> **Note:** If the `frontend-design` or `ui-ux-pro-max` skill is available, it will be used to guide the design analysis in Step 2.

---

### Step 2 — Analyse the Project

If either of these skills is installed in `~/.claude/skills/`, use it to guide the design language analysis below:
- `frontend-design`
- `ui-ux-pro-max`

If neither is found, proceed using your own UI/UX design expertise.

Read the project or PRD thoroughly. Identify:
- Core product value proposition
- Target audience and tone (professional, playful, technical, consumer, etc.)
- Key features or sections that must appear on the landing page
- Any existing brand signals (colours, logos, fonts) if present in the codebase

**Placeholder content strategy:**
- Always extract real content from the PRD or codebase (product name, tagline, feature names, target audience).
- If the PRD lacks enough copy for a specific section, derive it from context (e.g. infer a tagline from the value proposition). Do not use Lorem Ipsum.
- Only use generic placeholder text (`[Product Name]`, `[Feature Description]`) as a last resort when the section has no extractable signal at all.

Use this analysis to define a design language internally. **Do not write this to a file.**

---

### Step 3 — Propose 5 Design Directions (WAIT FOR APPROVAL)

Present exactly 5 design directions to the user. Each direction must differ in **both visual style and layout structure**. Format:

```
Here are the 5 design directions I'm planning:

1. **[Direction Name]** — [One sentence: visual style + layout approach]
2. **[Direction Name]** — [One sentence: visual style + layout approach]
3. **[Direction Name]** — [One sentence: visual style + layout approach]
4. **[Direction Name]** — [One sentence: visual style + layout approach]
5. **[Direction Name]** — [One sentence: visual style + layout approach]

Shall I proceed with these, or would you like to adjust any direction?
```

**Do not write any code until the user approves.** If the user requests changes, revise the directions and re-present before proceeding.

---

### Step 4 — Persist Directions to File

Immediately after the user approves the 5 directions, write a `directions.json` file **before generating any pages**.

See [lib/directions.md](../../lib/directions.md) — Format & Write Rules

Confirm to the user: `"Directions saved."`

---

### Step 5 — Build the 5 Pages

After writing `directions.json`, implement all 5 pages as **UI-only** (no business logic, no real data fetching).

**Routing rules:** See [lib/stack-detection.md](../../lib/stack-detection.md) for the full routing convention table.

If the user specified different route names during setup, use those instead.

**Each page must:**
- Fully implement its unique design direction (colours, typography, layout, spacing, components)
- Be visually distinct from all other pages — different layout structure, not just different colours
- Use content derived from the project analysis (see Step 2 placeholder strategy)
- Be self-contained and renderable without external dependencies beyond the project's installed packages

**Tell the user as you complete each page:**
> "Page 1 (Dark & Bold) — done."

---

### Step 6 — Build the Navigation / Gallery Page

After all 5 pages are complete, create a gallery index page at `/gallery/{id}`.

**Gallery page content:**
- Title: "Design Gallery"
- Session ID displayed as a small badge (so users can reference it later)
- List all 5 variations, each as a card or row containing:
  - A link to the page (`/gallery/{id}/1`, `/gallery/{id}/2`, etc.)
  - The direction name (e.g. "Dark & Bold")
  - The one-sentence description from `directions.json`
- Simple, neutral styling — the gallery page should not compete visually with the designs themselves

**Finish with:**
> "Done! All 5 pages and the gallery are ready.
> - Gallery: `/gallery/{id}`
> - Pages: `/gallery/{id}/1` through `/gallery/{id}/5`
> - Session ID: `{id}` (used by `/redesign` to reference this gallery)
>
> To iterate on any of them, run `/redesign`."

---

## Design Direction Guidelines

When choosing 5 directions, ensure they are genuinely distinct. Good combinations:

| # | Style Example | Layout Example |
|---|---|---|
| 1 | Minimal / clean, lots of whitespace | Single-column, hero + stacked sections |
| 2 | Dark mode, high contrast, bold type | Split-screen hero, horizontal feature rows |
| 3 | Glassmorphism / frosted blur effects | Asymmetric, overlapping cards |
| 4 | Corporate / professional, muted palette | Grid-based, sidebar navigation |
| 5 | Vibrant / playful, expressive gradients | Full-bleed sections, large visuals |

Do not reuse directions across a session — `/redesign` relies on this history.

---

## Notes

- Pages are **UI prototypes only** — no authentication, no API calls, no database
- Always follow the project's existing linting and formatting conventions
- Do not modify any existing project files outside the new routes/pages created
- If the user asks for more than 5 variations, generate the additional ones before creating the gallery
