# {{PROJECT_NAME}} — Claude Code Instructions

## Stack
- **Framework:** {{FRAMEWORK}}
- **Styling:** {{STYLING}}
- **Language:** TypeScript strict
- **Package manager:** {{PKG_MANAGER}}
- **Backend:** {{BACKEND}}

## Language policy
- Code, variables, file names: English
- UI copy and comments: {{UI_LANG}}

## Code conventions
- No comments unless the WHY is non-obvious
- No placeholder stubs — implement or skip
- Validate only at system boundaries
- No `any` in TypeScript
- All shared types in `lib/types.ts`

## Project structure
{{PROJECT_STRUCTURE}}

## Agents available for this project
See `AGENTS.md` for the 4 specialized agents and their responsibilities.

## Environment variables
Copy `.env.example` to `.env.local` and fill in values before running.
Never commit `.env.local`.
