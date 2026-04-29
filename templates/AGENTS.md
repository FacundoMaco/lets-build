# {{PROJECT_NAME}} — Agent Roster

This project was scaffolded with `/lets-build`. The 4 agents below have defined roles.
Spawn them explicitly when working on their domain to keep context focused and tokens low.

## Agent 1 — Backend
**Trigger:** When modifying DB schema, server actions, API routes, auth logic, or env vars.
**Stack ownership:** `lib/db.ts`, `lib/auth.ts`, `lib/actions.ts`, `supabase/`, `.env.example`
**Instruction file:** see `agents/backend.md` in the lets-build skill

## Agent 2 — Frontend
**Trigger:** When adding pages, components, or modifying routing.
**Stack ownership:** `app/` or `src/pages/`, `components/`, `lib/types.ts`, `lib/utils.ts`
**Instruction file:** see `agents/frontend.md` in the lets-build skill

## Agent 3 — Security
**Trigger:** When reviewing for production readiness, adding new routes, or changing auth.
**Stack ownership:** `middleware.ts`, `.gitignore`, `SECURITY.md`, env var naming
**Instruction file:** see `agents/security.md` in the lets-build skill

## Agent 4 — Design
**Trigger:** When updating visual system, adding new component patterns, or theming.
**Stack ownership:** `app/globals.css` or `src/index.css`, `DESIGN.md`, `tailwind.config.js`
**Instruction file:** see `agents/design.md` in the lets-build skill

## Parallel dispatch rule
When a task spans multiple agents, spawn them simultaneously and have them write to files.
Agents communicate via files — not via conversation context.
