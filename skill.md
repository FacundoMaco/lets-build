# /lets-build

A multi-agent project scaffolding skill for Claude Code.
Runs 4 specialized agents in parallel to generate backend, frontend, security, and design artifacts from a client brief.

## Trigger

`/lets-build`

---

## Phase 1 — Intake

Ask the user these questions before spawning any agent. Wait for all answers.

```
1. Project name?
2. What does this product do? (one sentence)
3. Who is the end user?
4. What language should UI copy and comments be in? (default: English)
5. Stack preference? (or say "recommend me one")
   - If "recommend": suggest Next.js App Router + Tailwind + TypeScript + Supabase for full-stack, Vite + Tailwind for landing/static
6. Package manager? (pnpm recommended — explain why if they ask)
7. Does this need a database / auth? (yes / no / not sure)
8. Any design references, brand colors, or style direction?
```

Compress all answers into a single **brief block** using this format:

```
PROJECT: <name>
PURPOSE: <one sentence>
USER: <end user>
LANG: <language>
STACK: <framework> | <styling> | <language> | <backend?>
PKG: <npm|pnpm>
DB_AUTH: <yes|no|tbd>
DESIGN: <references or none>
```

---

## Phase 2 — Parallel Agent Dispatch

Spawn all 4 agents simultaneously using the `Agent` tool.
Pass each agent only its required section of the brief. Do not pass the full conversation.

### Agent 1 — Backend

**Role:** Design server-side architecture.

**Input:** PROJECT, PURPOSE, STACK, DB_AUTH fields from brief.

**Output files to create inside `<project-name>/`:**
- `PRD.md` — product requirements (features, data model, API routes)
- `supabase/schema.sql` — if DB is needed
- `lib/db.ts` — Supabase client setup (if applicable)
- `lib/auth.ts` — auth helpers (if applicable)
- `.env.example` — all required env vars, no real values

**Instructions for this agent:**
- Be opinionated. Choose patterns that scale.
- If stack is Next.js: use Server Actions for mutations, Route Handlers for external webhooks only.
- If no DB needed: output `PRD.md` and `.env.example` only.
- Use TypeScript strict. No `any`.
- Output code only — no explanations inside files.

---

### Agent 2 — Frontend

**Role:** Scaffold UI component tree and page structure.

**Input:** PROJECT, PURPOSE, USER, STACK, LANG fields from brief. Wait for Backend agent PRD.md before running if possible — if not available, infer from PURPOSE.

**Output files to create inside `<project-name>/`:**
- Page files matching PRD routes (or inferred from PURPOSE)
- `components/` structure with placeholder components
- `lib/types.ts` — shared TypeScript interfaces
- `public/` — empty, with `.gitkeep`

**Instructions for this agent:**
- Next.js App Router: all pages as Server Components by default. Add `'use client'` only when needed.
- Vite: standard `src/pages/` and `src/components/` structure.
- Do not hardcode colors. Use design tokens from Design agent output (or use CSS variables as placeholders: `var(--color-primary)`).
- UI copy in the language specified in brief.
- No placeholder lorem ipsum. Use realistic copy based on PURPOSE.

---

### Agent 3 — Security

**Role:** Harden the project before it ships.

**Input:** STACK, DB_AUTH, PROJECT fields from brief.

**Output files to create inside `<project-name>/`:**
- `.gitignore` — comprehensive, stack-aware
- `middleware.ts` — security headers (CSP, HSTS, X-Frame-Options) if Next.js
- Append to `.env.example` any security-related vars (JWT_SECRET, etc.)
- `SECURITY.md` — brief threat model + what was implemented

**Instructions for this agent:**
- Never store secrets in code. Flag any env var that would be exposed client-side.
- If Supabase: enable RLS on all tables, add note in SECURITY.md.
- If auth: enforce session expiry, recommend httpOnly cookies over localStorage.
- Be concise. SECURITY.md max 60 lines.

---

### Agent 4 — Design

**Role:** Define the visual system and generate base UI using Claude's design capabilities.

**Input:** PROJECT, PURPOSE, USER, DESIGN, LANG, STACK fields from brief.

**Output files to create inside `<project-name>/`:**
- `app/globals.css` (or `src/index.css`) — complete design token system
- `DESIGN.md` — color palette, typography scale, spacing, component patterns
- A rendered design preview using Claude artifacts (if supported in current session)

**Instructions for this agent:**
- Define a complete token system: colors (primary, secondary, neutral, semantic), typography (2 fonts max), spacing scale, border radius, shadows.
- Tailwind v4 projects: use `@theme {}` block in globals.css — no tailwind.config.js.
- Tailwind v3 projects: output `tailwind.config.js` with `theme.extend`.
- Match tone to PURPOSE and USER (e.g., medical → clean/minimal, creative agency → bold/expressive).
- If DESIGN references provided: extract palette and typographic direction from them.
- Generate a visual component preview (hero, card, button, input) using Claude design mode if available.

---

## Phase 3 — Assembly

After all 4 agents complete:

1. Create `.claude/` folder inside the project:
   - `settings.json` — permissions scoped to this project
   - `CLAUDE.md` — project-specific conventions (use `templates/CLAUDE.md` as base, fill with actual stack + decisions made)
   - `AGENTS.md` — document the 4 agents and their roles for future sessions

2. Output a summary to the user:

```
Project: <name>
Stack: <stack>
Package manager: <pkg>

Created:
  PRD.md
  .env.example
  SECURITY.md
  DESIGN.md
  .claude/CLAUDE.md
  .claude/AGENTS.md
  [all scaffolded files]

Next steps:
  1. Fill in .env vars
  2. Run <install command>
  3. Review PRD.md and adjust to your needs
```

---

## Token Efficiency Rules

- Each agent receives only its required brief fields — not the full conversation
- Agents communicate via files, not messages
- Use fragment-style output inside agents (caveman compression)
- The orchestrator does not re-read agent outputs — it trusts the file list
- If `/caveman` skill is installed, activate it before spawning agents
