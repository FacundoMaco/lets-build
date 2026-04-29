# Reddit Posts — /lets-build launch

---

## r/ClaudeAI

**Title:**
I built a Claude Code skill that spawns 4 specialized agents in parallel to scaffold a full project from a client brief

**Body:**
Been building client projects with Claude Code for a while and got tired of the same repetitive setup: PRD, folder structure, security headers, design tokens, CLAUDE.md, AGENTS.md...

So I built `/lets-build` — a skill that turns an 8-question intake into a production-ready project scaffold using 4 agents running in parallel:

- **Backend agent** → PRD, DB schema, server actions, auth helpers, env vars
- **Frontend agent** → pages, components, types, routing
- **Security agent** → middleware, headers, gitignore, threat model
- **Design agent** → full CSS token system, DESIGN.md, component patterns

Each agent only receives the brief fields it needs (~200 tokens of context). They write to files, not conversation — so no context bloat. Works with any stack but has full support for Next.js + Tailwind + Supabase.

The skill also asks for your language preference, recommends npm vs pnpm, and auto-generates `.claude/CLAUDE.md` and `.claude/AGENTS.md` so future Claude sessions on that project know exactly which agent to spawn for what.

GitHub: https://github.com/FacundoMaco/lets-build

Install:
```
claude plugin marketplace add FacundoMaco/lets-build && claude plugin install lets-build@lets-build
```

Happy to answer questions about the agent architecture if anyone's curious.

---

## r/cursor

**Title:**
Built a Claude Code skill with 4 parallel agents that scaffolds a full project from a brief — open source

**Body:**
Not Cursor-specific but this sub has the right crowd.

I made `/lets-build` — a Claude Code skill that takes an 8-question client brief and outputs a complete project scaffold using 4 specialized agents running in parallel:

**What you get from one command:**
- `PRD.md` with data model and feature list
- Full file structure for Next.js / Vite (or whatever stack you choose)
- `DESIGN.md` + complete CSS token system in globals.css
- `SECURITY.md` + `middleware.ts` with security headers
- `.env.example` with all required vars
- `.claude/CLAUDE.md` + `.claude/AGENTS.md` pre-configured for the project

**The architecture:**
```
/lets-build
     │
     ▼
[Orchestrator] — intake → compressed brief
     │
     ├─────────────────────┐
     ▼                     ▼
[Backend]            [Design]        ← parallel
     │                     │
     └──────┬──────────────┘
            ▼
     ┌──────────────────────┐
     ▼                      ▼
[Frontend]           [Security]      ← parallel
```

Token-efficient: agents communicate via files, not conversation context.

Stack-agnostic: works with any framework, recommends one if you're unsure.

https://github.com/FacundoMaco/lets-build

---

## Optional: Hacker News (Show HN)

**Title:**
Show HN: /lets-build — Claude Code skill that runs 4 specialized agents in parallel to scaffold a project

**Body:**
https://github.com/FacundoMaco/lets-build

Built a Claude Code skill called /lets-build. It takes an 8-question intake (stack, language, DB needs, design direction) and spawns 4 agents simultaneously:

1. Backend — PRD, schema, server actions, auth, env vars
2. Frontend — pages, components, TypeScript types, routing
3. Security — CSP headers, gitignore, threat model, RLS reminders
4. Design — full CSS token system, typography, DESIGN.md

Agents receive compressed briefs (~200 tokens each) and write to files rather than accumulating conversation context. The orchestrator doesn't re-read their outputs — it trusts the file list.

Output includes pre-configured .claude/CLAUDE.md and .claude/AGENTS.md so Claude Code knows which agent to invoke for future changes to that project.

Stack-agnostic. MIT license.
