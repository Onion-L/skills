# Workflow

End-to-end landing page generation: explore design directions, iterate, and ship.

```
/gallery  →  review variations  →  /redesign (optional, repeat)  →  /finalize
```

---

## Step 1 — Explore: `/gallery`

**Command:** `/gallery [project-or-prd]`

**What happens:**

```
You → /gallery
Agent → generates session ID (e.g. a3f9k2)
Agent → detects tech stack
Agent → analyses project / PRD
Agent → proposes 5 design directions
You  → approve or adjust
Agent → saves directions.json
Agent → builds /gallery/a3f9k2/1 … /gallery/a3f9k2/5
Agent → builds /gallery/a3f9k2 (navigation page)
Agent → "Done! Session ID: a3f9k2"
```

**Output:** 5 distinct prototype pages + navigation index + `directions.json`

---

## Step 2 — Iterate: `/redesign` (optional)

**Command:** `/redesign [pages] [session-id]`

**When to use:** You're not satisfied with one or more variations.

**What happens:**

```
You  → /redesign 3 and 5
Agent → loads directions.json (reads history)
Agent → shows current variations
Agent → proposes new directions (never repeats history)
You  → approve or adjust
Agent → updates directions.json
Agent → rebuilds pages 3 and 5
Agent → updates gallery navigation
Agent → "Done! Redesigned: 3, 5. Unchanged: 1, 2, 4."
```

Repeat as many times as needed. `directions.json` accumulates the full history so directions are never recycled.

---

## Step 3 — Ship: `/finalize`

**Command:** `/finalize [page-number] [session-id]`

**When to use:** You've found the right direction and want to ship it.

**What happens:**

```
You  → /finalize 3
Agent → confirms selection: "Variation 3 — Glassmorphism"
Agent → collects brand constraints (color, font, headline, CTA, images)
You  → provide constraints (or say "you decide")
Agent → refines prototype with real copy + brand
Agent → adds SEO / Open Graph meta tags
Agent → "Ready to migrate to /. Confirm?"
You  → yes
Agent → moves page to /
Agent → deletes /gallery/a3f9k2/ (all temp files)
Agent → runs acceptance check
Agent → "Done! Ready to deploy."
```

---

## Interaction Diagram

```
┌─────────────────────────────────────────────────────────┐
│                     /gallery                            │
│  input: project/PRD                                     │
│  output: 5 prototypes + directions.json                 │
└────────────────────────┬────────────────────────────────┘
                         │
              ┌──────────▼──────────┐
              │   satisfied?         │
              └──────┬──────────────┘
           no │                │ yes
              ▼                ▼
   ┌──────────────────┐   ┌──────────────────┐
   │    /redesign     │   │    /finalize      │
   │  select + redo   │   │  brand + ship     │
   └────────┬─────────┘   └──────────────────┘
            │ (repeat)
            └──────────────► satisfied? → /finalize
```

---

## Key Files

| File | Purpose |
|---|---|
| `gallery/{id}/directions.json` | Authoritative history of all design directions used |
| `gallery/{id}/1–5` | Prototype pages (temporary) |
| `gallery/{id}/` | Navigation index (temporary) |
| `/` (or custom route) | Final production page (after `/finalize`) |
