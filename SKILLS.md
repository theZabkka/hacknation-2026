# Skills for the Hack Nation monorepo

Run these in the repo root. They install into the project (e.g. `.claude/skills/` / `.agents/skills/`),
so commit them and the whole team plus every agent (Claude Code, Cursor, Codex) gets the same skills.
Rule from the video: few skills, consistent style. Read each SKILL.md before installing.

## Core (install on day 0)
```bash
# Skill discovery: lets the agent search skills.sh itself
npx skills add vercel-labs/skills --skill find-skills

# React / Next.js: Vercel's official rules
npx skills add vercel-labs/agent-skills --skill vercel-react-best-practices
npx skills add vercel-labs/agent-skills --skill vercel-composition-patterns
npx skills add vercel-labs/agent-skills --skill web-design-guidelines
npx skills add vercel-labs/next-skills --skill next-best-practices   # may redirect to vercel/next.js

# Mobile
npx skills add expo/skills --skill '*'
npx skills add vercel-labs/agent-skills --skill vercel-react-native-skills

# Supabase
npx skills add supabase/agent-skills

# Browser verification for agents (token-efficient alternative to Playwright MCP)
npm i -g @playwright/cli
playwright-cli install-browser
# + its skill: see https://playwright.dev/agent-cli/introduction
```

## Engineering workflow (Matt Pocock, used in the video)
```bash
npx skills add mattpocock/skills --skill grill-me
npx skills add mattpocock/skills --skill improve-codebase-architecture
npx skills add mattpocock/skills --skill tdd
```

## Pitch / demo video
```bash
npx skills add heygen-com/hyperframes     # HTML -> MP4, needs Node >= 22 and FFmpeg
```

## Our own skills (saved in Claude, copy into .claude/skills/ for Claude Code)
- verify-before-done: test-first, typecheck, lint, tests, screenshot
- react-engineering-standards: architecture, boundaries, conventions

## Playwright: what is per project vs per machine
- `@playwright/test` = devDependency per project (version pinned in the lockfile).
- Browser binaries = per machine, shared cache: `%USERPROFILE%\AppData\Local\ms-playwright` on Windows.
  `npx playwright install chromium` downloads once per Playwright version and every project reuses it.
