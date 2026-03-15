# Stack Detection

## Monorepo Detection

Treat a project as a monorepo if **any** of these exist:

- A `workspaces` field in `package.json`
- A `pnpm-workspace.yaml` file
- A `turbo.json` file

If a monorepo is detected:
> "This is a monorepo. Where should I put the design gallery code? (e.g. `apps/gallery` or `packages/landing`)"

Wait for the user's answer before proceeding.

## Framework Identification & Routing Conventions

Read `package.json` and config files to detect the stack, then follow the appropriate routing convention:

| Project Type | Route Convention |
|---|---|
| Next.js (App Router) | `app/gallery/{id}/[1–5]/page.tsx` |
| Next.js (Pages Router) | `pages/gallery/{id}/[1–5].tsx` |
| Nuxt.js | `pages/gallery/{id}/[1–5].vue` |
| React (React Router) | Page files in `src/pages/` — update router config **once** after all pages are written |
| Vue (Vue Router) | Page files in `src/views/` — update router config **once** after all pages are written |
| Plain HTML | `gallery/{id}/1.html` … `gallery/{id}/5.html` |

> **Router config write order (React Router / Vue Router only):**
> Write all 5 page component files first. Only after all 5 files exist, update the router config file in **one single pass** with all 5 routes added together. Never update the router config incrementally between pages.

## When Ambiguous

If the stack is ambiguous or you are not confident, **stop and ask the user** — do not guess.
