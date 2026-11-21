# AGENTS.md — Hack Nation monorepo

> Single source of truth for every coding agent (Claude Code, Codex, Cursor, Copilot).
> CLAUDE.md only imports this file. Keep it short — every line costs tokens in every session.

## Project
- What: <one sentence — what we're building and for whom>
- Status: <hackathon day 0 / MVP / demo-ready>
- Demo deadline: <date + hour>

## Stack
- Monorepo: Turborepo + pnpm workspaces
- `apps/web` — Next.js (App Router, TypeScript), deployed on Vercel
- `apps/mobile` — Expo (React Native, Expo Router, TypeScript)
- `packages/db` — Supabase client factory + generated types (`database.types.ts`)
- `packages/shared` — zod schemas, domain types, pure utils (no React, no Node-only APIs)
- `packages/ui` — only if web and mobile truly share components (default: don't)
- Backend: Supabase (Postgres, Auth, Storage, Edge Functions)

## Commands
- `pnpm dev` — all apps · `pnpm --filter web dev` · `pnpm --filter mobile start`
- `pnpm typecheck` · `pnpm lint` · `pnpm test`
- `pnpm db:types` — regenerate Supabase types after every migration

## Definition of done (verification — mandatory)
A task is NOT done until all of these pass:
1. `pnpm typecheck` and `pnpm lint` are clean.
2. Tests for the changed behaviour pass. Write the test FIRST, then implement.
   Test the important paths only — no tests for trivial getters or one-line wrappers.
3. UI changes: open the page in the browser, take a screenshot, check it visually.
Never report "done" based on reasoning alone — report what you actually ran and its output.

## Supabase rules
- Every new table: RLS enabled + explicit policies in the same migration. No exceptions.
- Schema changes only through migration files (`supabase/migrations`), never ad hoc in the dashboard.
- Never use the service_role key in `apps/web` client code or in `apps/mobile`.
- After a migration: regenerate types, fix type errors, then continue.

## Code style
- TypeScript strict. No `any` without a comment explaining why.
- Validate external input (forms, API, Edge Functions) with zod schemas from `packages/shared`.
- Prefer small, boring code over clever abstractions. Delete dead code instead of commenting it out.
- User-facing text: sentence case. Never ALL CAPS in UI labels, buttons or headings.
- No new dependency without saying why in the PR description.

## Working rules for agents
- Big task (new feature, >3 files, schema change): plan first, wait for approval.
- Small task (typo, rename, style tweak): just do it, no plan.
- Read only the files you need. If you are unsure where something lives, ask instead of scanning the whole repo.
- Explain non-obvious decisions in 1–2 sentences — I want to understand the code, not just accept it.

## Git / PRs
- Branch per task (`feat/…`, `fix/…`); worktree per parallel agent.
- Commit messages and PR descriptions in English, imperative mood.
- PR description: what changed, why, how it was verified.
