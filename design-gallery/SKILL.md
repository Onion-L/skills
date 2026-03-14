---
name: design-gallery
description: Generates 5 landing page design variations from an existing project or PRD document, then creates a /gallery navigation page to compare them. Combines UI/UX design analysis with frontend implementation. Use when the user wants to explore multiple design directions for a landing page.
---

# Design Gallery

Generate 5 distinct landing page UI variations from a project or PRD, then produce a `/gallery` navigation page to browse and compare them all.

## When to Use This Skill

- User provides an existing project codebase and wants landing page design options
- User provides a PRD document and wants to visualise design directions
- User says "generate design variations", "show me different landing page styles", or "design gallery"

---

## Workflow

### Step 1 — Understand the Input

Determine what the user has provided:

**If the input is a PRD file only (no existing code):**
> "I only see a PRD document here. Would you like to choose your own tech stack, or should I default to **Next.js + Tailwind CSS**?"
- Wait for the user's answer before proceeding.

**If the input is an existing codebase:**
- Read `package.json`, config files, and framework indicators to detect the stack.
- If the stack is ambiguous or you are not confident, **stop and ask the user** — do not guess.
- If it is a monorepo:
  > "This looks like a monorepo. Where should I put the design gallery code? (e.g. `apps/gallery` or `packages/landing`)"
  - Wait for the user's answer.

Do not proceed until the stack and output location are confirmed.

---

### Step 2 — Check for Design Sub-skills

Check whether either of these skills is installed in `~/.claude/skills/`:
- A skill named `frontend-design`
- A skill named `ui-ux-pro-max`

**If a design skill is found:** Use it to guide the design language analysis in Step 3.
**If none are found:** Proceed using your own UI/UX design expertise — do not mention this to the user.

---

### Step 3 — Analyse the Project

Read the project or PRD thoroughly. Identify:
- Core product value proposition
- Target audience and tone (professional, playful, technical, consumer, etc.)
- Key features or sections that must appear on the landing page
- Any existing brand signals (colours, logos, fonts) if present in the codebase

Use this analysis to define a design language internally. **Do not write this to a file.**

---

### Step 4 — Propose 5 Design Directions (WAIT FOR APPROVAL)

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

Keep an internal record of all direction names used — this is needed by `/redesign`.

---

### Step 5 — Build the 5 Pages

After approval, implement all 5 pages as **UI-only** (no business logic, no real data fetching, placeholder copy is fine).

**Routing rules — detect the project type and follow its conventions:**

| Project Type | Route Convention |
|---|---|
| Next.js (App Router) | `app/1/page.tsx`, `app/2/page.tsx` … `app/5/page.tsx` |
| Next.js (Pages Router) | `pages/1.tsx`, `pages/2.tsx` … `pages/5.tsx` |
| Nuxt.js | `pages/1.vue`, `pages/2.vue` … `pages/5.vue` |
| React (React Router) | Page files in `src/pages/` — update router config **once** after all pages are written |
| Vue (Vue Router) | Page files in `src/views/` — update router config **once** after all pages are written |
| Plain HTML | `1.html`, `2.html` … `5.html` |

If the user specified different route names during setup, use those instead.

> **⚠️ Router config write order (React Router / Vue Router only):**
> Write all 5 page component files first. Then update the single router config file in one pass with all 5 routes added. This prevents concurrent write conflicts on the shared config file.

**Each page must:**
- Fully implement its unique design direction (colours, typography, layout, spacing, components)
- Be visually distinct from all other pages — different layout structure, not just different colours
- Include realistic placeholder content relevant to the project (not Lorem Ipsum if avoidable)
- Be self-contained and renderable without external dependencies beyond the project's installed packages

**Tell the user as you complete each page:**
> "Page 1 (Dark & Bold) — done."

---

### Step 6 — Build the Navigation / Gallery Page

After all 5 pages are complete, create a gallery page.

**Path:** `/gallery`
- If `/gallery` already exists as a route or file, choose an alternative name (e.g. `/design-gallery`, `/showcase`) and inform the user which name you chose.

**Gallery page content:**
- Title: "Design Gallery"
- List all 5 variations, each as a card or row containing:
  - A link to the page (`/1`, `/2`, etc.)
  - The direction name (e.g. "Dark & Bold")
  - The one-sentence description you proposed in Step 4
- Simple, neutral styling — the gallery page should not compete visually with the designs themselves

**Finish with:**
> "Done! All 5 pages and the gallery are ready.
> - Gallery: `/gallery`
> - Pages: `/1` through `/5`
>
> If you'd like to completely redesign any of them, run `/redesign`."

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
