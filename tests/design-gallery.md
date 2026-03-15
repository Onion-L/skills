# Tests: design-gallery

Behavioral test cases for the `design-gallery` skill. Each case describes the input and expected agent behavior.

---

## Case 1: PRD Input (no codebase)

**Input prompt:**
> Here's my PRD for a task management SaaS. Generate design variations.

**Expected behavior:**
- Agent asks: "I only see a PRD document here. Would you like to choose your own tech stack, or should I default to Next.js + Tailwind CSS?"
- Waits for user answer before proceeding
- Generates session ID after stack is confirmed
- Extracts real content from PRD (product name, tagline, features) — no Lorem Ipsum
- Proposes 5 genuinely distinct directions and waits for approval
- Writes `directions.json` before generating any pages
- Builds 5 pages and a gallery index

---

## Case 2: Existing Codebase Input

**Input prompt:**
> Generate landing page variations for my project at ./my-app

**Expected behavior:**
- Reads `package.json` and config files to detect stack
- Identifies framework (e.g. Next.js App Router) without asking unless ambiguous
- Checks `/gallery/{id}/1–5` for conflicts before writing
- Proposes directions and waits for approval
- Uses correct file paths per routing convention (e.g. `app/gallery/{id}/1/page.tsx`)

---

## Case 3: Monorepo Scenario

**Input prompt:**
> Generate designs for my turborepo project

**Expected behavior:**
- Detects monorepo via `turbo.json` (or `workspaces` / `pnpm-workspace.yaml`)
- Asks: "This is a monorepo. Where should I put the design gallery code? (e.g. `apps/gallery` or `packages/landing`)"
- Waits for user answer before proceeding
- Places all gallery files under the user-specified path

---

## Case 4: Ambiguous Stack

**Input prompt:**
> Make landing page designs for my project

**Expected behavior:**
- Reads `package.json`; if stack cannot be determined confidently
- Stops and asks the user — does not guess
- Only proceeds after stack is confirmed

---

## Case 5: Existing Routes Conflict

**Setup:** `/gallery/a3f9k2/1` already exists.

**Expected behavior:**
- Detects the conflict before writing anything
- Stops and informs user: "Route `/gallery/a3f9k2/1` already exists — I won't overwrite it."
- Does not proceed silently
