# skills

A collection of [Claude Code](https://github.com/anthropics/claude-code) skills for UI/UX design and frontend development workflows.

## Skills

### `/design-gallery`

Generates **5 distinct landing page design variations** from an existing project or PRD document, then creates a `/gallery` navigation page so you can compare them side-by-side.

**Workflow:**
1. Detects your tech stack (asks if ambiguous or PRD-only)
2. Analyses the project/PRD to understand product, audience, and brand signals
3. Proposes 5 design directions — **waits for your approval** before writing any code
4. Builds 5 UI-only pages at `/1`–`/5`, following your project's router conventions
5. Creates a `/gallery` navigation page with links and direction descriptions

**Supports:** Next.js (App & Pages Router), Nuxt.js, React Router, Vue Router, plain HTML

---

### `/redesign`

Companion to `/design-gallery`. Lets you **selectively redesign** one or more of the 5 variations. Never repeats a design direction already used in the session.

**Workflow:**
1. Lists all 5 current pages with their design direction names
2. You pick which ones to redesign (one, several, or all)
3. Proposes fresh directions — **waits for your approval** before writing any code
4. Rebuilds selected pages and updates the gallery

---

## Install

```bash
npx claude install Onion-L/skills
```

Install individual skills:

```bash
npx claude install Onion-L/skills/design-gallery
npx claude install Onion-L/skills/redesign
```

## Usage

In any project with Claude Code, run:

```
/design-gallery
```

Point it at your project root or a PRD file. After the gallery is generated, run:

```
/redesign
```

Pick which pages to redo — the agent will propose new directions and never repeat old ones.

## Requirements

- [Claude Code](https://github.com/anthropics/claude-code)
- A web project (Next.js, Nuxt, React, Vue) or a PRD document

## License

MIT
