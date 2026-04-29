# /lets-build

A Claude Code skill that turns a client brief into a production-ready project scaffold using 4 specialized AI agents working in parallel.

**One command. Full project.**

---

## What it does

Type `/lets-build` in Claude Code. Answer 8 questions. Get:

- `PRD.md` — product requirements document
- Complete file structure for your chosen stack
- `DESIGN.md` + full CSS token system
- `SECURITY.md` + middleware + `.gitignore` + `.env.example`
- `.claude/CLAUDE.md` + `.claude/AGENTS.md` — pre-configured for the project

---

## How it works

```
/lets-build
     │
     ▼
[Orchestrator] — 8 intake questions → compressed brief
     │
     ├──────────────────────────────────────┐
     ▼                                      ▼
[Backend Agent]                    [Design Agent]
 PRD, schema, actions,              Token system, globals.css,
 auth helpers, env vars             DESIGN.md, component preview
     │                                      │
     └──────────────┬───────────────────────┘
                    ▼
     ┌──────────────────────────────────────┐
     ▼                                      ▼
[Frontend Agent]                  [Security Agent]
 Pages, components,                middleware.ts, headers,
 types, routing                    SECURITY.md, .gitignore
     │                                      │
     └──────────────┬───────────────────────┘
                    ▼
           .claude/ scaffolded
           CLAUDE.md + AGENTS.md
           Summary printed
```

Each agent receives only the brief fields it needs. They communicate via files, not conversation. Token-efficient by design.

---

## Stack support

| Stack | Status |
|---|---|
| Next.js App Router + Tailwind v4 | Full support |
| Next.js App Router + Tailwind v3 | Full support |
| Vite + React + Tailwind | Full support |
| Any other stack | Partial (PRD, DESIGN, SECURITY always generated) |

Not sure what stack to use? Type "recommend me one" during intake — the skill picks based on your project type.

---

## Install

```bash
claude plugin marketplace add mavre-dev/lets-build && claude plugin install lets-build@lets-build
```

---

## Usage

Open any project folder in Claude Code and run:

```
/lets-build
```

Follow the 8-question intake. All agents run in parallel after intake completes.

---

## Output example

See [`examples/output-example.md`](examples/output-example.md) for a full walkthrough with a real project (TaskFlow — team task management SaaS).

---

## Agent roles

| Agent | Owns | When to re-invoke |
|---|---|---|
| Backend | Schema, actions, auth, env vars | Adding DB tables, new server actions |
| Frontend | Pages, components, types, routing | Adding features, new pages |
| Security | Headers, gitignore, threat model | Pre-production review, new auth flows |
| Design | Token system, CSS, DESIGN.md | Rebranding, adding component patterns |

Each agent's full instruction set lives in [`agents/`](agents/).

---

## Token efficiency

- Orchestrator passes compressed briefs (~200 tokens) to each agent
- Agents write to files — no context accumulation between agents
- Works well with the [caveman](https://github.com/JuliusBrussee/caveman) skill for additional compression

---

## Requirements

- Claude Code 2.x
- Node.js 18+

---

## License

MIT
