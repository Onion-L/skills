# Tests: redesign

Behavioral test cases for the `redesign` skill.

---

## Case 1: Single Page Redesign

**Setup:** Session `a3f9k2` with 5 pages exists.

**Input prompt:**
> Redesign page 3

**Expected behavior:**
- Resolves session from context (no prompt needed)
- Loads `directions.json` and identifies all used directions
- Shows current variations with names/descriptions
- Proposes one new direction for page 3 that hasn't been used before
- Waits for approval
- Updates `directions.json` (replaces page 3 entry)
- Rebuilds only page 3
- Updates gallery navigation to reflect new direction name
- Leaves pages 1, 2, 4, 5 untouched

---

## Case 2: Redesign All Pages

**Input prompt:**
> None of these work, redo all of them

**Expected behavior:**
- Loads `directions.json` — all 5 current directions are off-limits
- Proposes 5 entirely new directions (different in both style and layout)
- Waits for approval
- Updates all 5 entries in `directions.json` before writing code
- Rebuilds all 5 pages
- Updates gallery navigation

---

## Case 3: Multiple Sessions — User Must Choose

**Setup:** Two sessions exist: `a3f9k2` and `b1d4m8`.

**Input prompt:**
> Redesign page 2

**Expected behavior:**
- Detects two `directions.json` files
- Lists both sessions and asks: "I found multiple gallery sessions: `a3f9k2`, `b1d4m8`. Which one would you like to work with?"
- Waits for user selection before loading anything

---

## Case 4: No Session Found

**Setup:** No `gallery/` directory exists.

**Input prompt:**
> /redesign

**Expected behavior:**
- Scans for `directions.json` files and finds none
- Stops: "I couldn't find a `directions.json` from a previous `design-gallery` run. Please run `/design-gallery` first."
- Does not attempt to create anything
