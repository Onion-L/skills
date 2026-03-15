---
name: promote-design
description: Promote a selected design-gallery variation into a production-ready landing page. Collects brand constraints, refines the chosen prototype with real copy and styling, adds SEO meta tags, migrates it to the final route, and cleans up all temporary gallery files. Use after /design-gallery when the user says "I want variation 3", "promote page 2", "go with design 1", or "ship this one". Always used after design-gallery has already generated pages.
---

# Promote Design

Take a selected design-gallery variation from prototype to production: apply brand identity, real copy, SEO, and migrate to the final route.

## Inputs

- User indicates which variation they want (e.g. "I want page 3")
- Reads `{output_root}/gallery/{id}/directions.json` to confirm direction name and description (same session ID resolution logic as `/redesign`)

---

## Workflow

### Step 1 — Confirm Selection & Collect Brand Constraints

Resolve the session ID and page number, then ask:

```
You selected variation {N} — {Direction Name}.

Before I start, a few questions:

1. Primary brand color? (leave blank and I'll suggest one based on the direction)
2. Font? (leave blank to use a suitable default)
3. Hero headline and subheadline?
4. CTA button text?
5. Any real product screenshots or images to include?
```

If the user says "you decide" or leaves fields blank, propose values that fit the chosen design direction and **wait for confirmation** before writing any code.

**Do not write any code until brand constraints are confirmed.**

---

### Step 2 — Refine the Page

Upgrade the selected prototype in-place:

- Replace all placeholder copy with real content
- Apply brand color and font across the entire page
- If the user provided images, replace placeholder images
- Complete all interaction details: hover states, transition animations, responsive breakpoints

---

### Step 3 — Add SEO and Meta

Inject into the page's `<head>`:

```html
<title>{Product Name} — {One-line description}</title>
<meta name="description" content="..." />
<meta property="og:title" content="..." />
<meta property="og:description" content="..." />
<meta property="og:image" content="..." />
```

Derive all values from real content — never use placeholder text in meta tags.

---

### Step 4 — Migrate to Final Route

Before touching any files, confirm with the user:

```
Ready to migrate. I'll:
- Move the refined page to: {target_path} (default: `/`)
- Delete all temporary gallery files under /gallery/{id}/

Confirm? (yes / specify a different path)
```

After confirmation:

1. Move the refined page to the confirmed target path
2. Delete `/gallery/{id}/1` through `/gallery/{id}/5`
3. Delete `/gallery/{id}/` directory (including `directions.json` and the gallery index)
4. Update router config: remove all `/gallery/{id}/*` routes, register the new route if needed

---

### Step 5 — Acceptance Check

After migration, verify:

- All `<img>` elements have non-empty `alt` attributes
- No remaining "Lorem Ipsum", "placeholder", `[Product Name]`, or similar stub text
- No `console.log` statements or `TODO` comments
- Responsive breakpoints exist for mobile

List any issues found — do not silently skip.

---

## Output

```
Done! Your landing page is ready.

Route: /
Brand color: #6366f1
Font: Inter

Cleaned up /gallery/{id} and all temporary files.
Ready to deploy.
```
