# Tests: finalize

Behavioral test cases for the `finalize` skill.

---

## Case 1: Full Brand Constraint Collection

**Setup:** Session `a3f9k2` with page 3 (Glassmorphism) exists.

**Input prompt:**
> Finalize page 3

**Expected behavior:**
- Reads `directions.json` and confirms: "You selected variation 3 — Glassmorphism."
- Asks all 5 brand questions (color, font, headline, subheadline, CTA, images)
- Waits for user answers
- Does not write any code until constraints are confirmed
- Works on a `.draft` copy, not the original
- Replaces all placeholder copy with real content
- Injects SEO and Open Graph meta tags with real values (no placeholder text)

---

## Case 2: User Says "You Decide"

**Input prompt:**
> /finalize 2 — you decide everything

**Expected behavior:**
- Proposes values for all brand fields that fit the chosen design direction
- Presents proposed values to user for confirmation
- Waits for explicit confirmation before writing any code

---

## Case 3: Migration Confirmation

**Expected behavior (at Step 4):**
- Shows migration plan before touching any files:
  - Target path (default `/`)
  - Which gallery files will be deleted
- Waits for "yes" or a different path
- Only proceeds after confirmation
- After migration: deletes `/gallery/{id}/1–5`, `/gallery/{id}/`, and `directions.json`
- Updates router config if needed

---

## Case 4: Acceptance Check — Auto-fix vs Ask

**Setup:** Finalized page has a missing `alt` attribute and a headline that reads "Hero Headline".

**Expected behavior:**
- Automatically fixes the missing `alt` attribute
- Flags "Hero Headline" as potentially placeholder-ish and asks the user before changing it
- Never silently skips issues
- Reports all found issues to the user
