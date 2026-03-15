# Session ID

## Session ID Generation

Generate a **6-character alphanumeric session ID** (e.g. `a3f9k2`) before doing anything else. Use this ID as a namespace for all routes in a run:

- Gallery index: `/gallery/{id}` (e.g. `/gallery/a3f9k2`)
- Pages: `/gallery/{id}/1` through `/gallery/{id}/5`

This prevents path collisions when multiple agents run in parallel.

## Session ID Resolution

Use this logic whenever a skill needs to determine the active session:

1. **From context** — if the user provided an explicit session ID (e.g. "session a3f9k2"), use it.
2. **Scan `gallery/`** — look for `directions.json` files under `{output_root}/gallery/`.
3. **Single session found** — use it automatically without asking.
4. **Multiple sessions found** — list them and ask the user to pick:
   > "I found multiple gallery sessions: `a3f9k2`, `b1d4m8`. Which one would you like to work with?"
5. **No sessions found** — stop:
   > "I couldn't find a `directions.json` from a previous `design-gallery` run. Please run `/design-gallery` first."
