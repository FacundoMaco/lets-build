# Example Output — Task Management SaaS

This is what `/lets-build` produces after the intake phase completes.

## Intake answers

```
Project: TaskFlow
Purpose: Team task management with real-time updates
User: Small teams (2-10 people), non-technical
Language: English
Stack: Next.js App Router + Tailwind v4 + TypeScript + Supabase
Package manager: pnpm
DB/Auth: Yes
Design: Clean, minimal. Reference: Linear.app
```

## Brief block (passed to agents)

```
PROJECT: TaskFlow
PURPOSE: Team task management with real-time updates
USER: Small teams (2-10 people), non-technical
LANG: English
STACK: Next.js App Router | Tailwind v4 | TypeScript | Supabase
PKG: pnpm
DB_AUTH: yes
DESIGN: Clean minimal, Linear.app reference
```

## Files created

```
taskflow/
├── .claude/
│   ├── CLAUDE.md
│   ├── AGENTS.md
│   └── settings.json
├── app/
│   ├── layout.tsx
│   ├── page.tsx
│   ├── dashboard/
│   │   ├── page.tsx
│   │   └── components/
│   │       ├── TaskList.tsx
│   │       ├── TaskCard.tsx
│   │       └── CreateTaskModal.tsx
│   └── auth/
│       ├── login/page.tsx
│       └── callback/route.ts
├── components/
│   ├── ui/
│   │   ├── Button.tsx
│   │   ├── Input.tsx
│   │   └── Modal.tsx
│   └── layout/
│       ├── Header.tsx
│       └── Sidebar.tsx
├── lib/
│   ├── types.ts
│   ├── utils.ts
│   ├── db.ts
│   ├── auth.ts
│   └── actions.ts
├── supabase/
│   └── schema.sql
├── middleware.ts
├── .env.example
├── .gitignore
├── PRD.md
├── DESIGN.md
└── SECURITY.md
```

## PRD.md (excerpt)

```md
# PRD — TaskFlow

## Problem
Teams lose track of work across Slack threads and spreadsheets.
TaskFlow centralizes task ownership with real-time visibility.

## Users
Small teams (2-10). Non-technical. Mobile-first usage expected.

## Features
- [ ] Create / edit / delete tasks
- [ ] Assign tasks to team members
- [ ] Real-time status updates
- [ ] Due date tracking
- [ ] Simple dashboard view

## Data Model
- users (id, email, name, avatar_url, created_at)
- teams (id, name, created_at)
- team_members (team_id, user_id, role)
- tasks (id, title, description, status, assignee_id, team_id, due_date, created_at)

## API / Actions
- createTask(teamId, data)
- updateTaskStatus(taskId, status)
- assignTask(taskId, userId)
- deleteTask(taskId)
```

## DESIGN.md (excerpt)

```md
# Design System — TaskFlow

## Personality
Clean and focused. Every element earns its place.
Inspired by Linear: high information density without visual noise.

## Colors
| Token | Value | Usage |
|---|---|---|
| --color-primary | #5E6AD2 | CTAs, active states, links |
| --color-background | #FAFAFA | Page background |
| --color-surface | #FFFFFF | Cards, modals |
| --color-border | #E5E7EB | Dividers, input borders |
| --color-text | #111827 | Primary text |
| --color-text-muted | #6B7280 | Secondary text, labels |

## Typography
- Heading: Inter — system-familiar, highly legible
- Body: Inter — single typeface for visual consistency
```

## SECURITY.md (excerpt)

```md
# Security — TaskFlow

## Threat model
Primary risk: unauthorized access to team data across tenant boundaries.
RLS policies enforce team-scoped data access at the DB layer.

## Implemented
- [x] Security headers via middleware.ts (CSP, HSTS, X-Frame-Options)
- [x] RLS enabled on all Supabase tables
- [x] Auth via Supabase (httpOnly cookies)
- [x] No secrets with NEXT_PUBLIC_ prefix

## Requires manual review before production
- [ ] CSP policy — adjust allowed script/style sources
- [ ] CORS — add production domain to allowed origins
- [ ] Rate limiting on auth endpoints
```
