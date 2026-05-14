# claude-skills

My collection of [Claude Code](https://claude.com/claude-code) skills. Drop them into `~/.claude/skills/` and they become available everywhere.

## Install

```bash
git clone https://github.com/PiXeL16/claude-skills.git
cp -R claude-skills/skills/* ~/.claude/skills/
```

Or cherry-pick individual skills:

```bash
cp -R claude-skills/skills/diagnose ~/.claude/skills/
```

## Layout

Each top-level directory under `skills/` is a single skill. Every skill has a `SKILL.md` with YAML frontmatter (`name`, `description`) plus any supporting files the skill loads.

## What's here

45 skills, grouped roughly by intent:

### Engineering workflow

- **`spec`** — refine a feature into a tracked epic
- **`implement`** — implement an epic as stacked PRs
- **`review`** — address PR review comments
- **`topr`** — rebase a stacked PR onto `origin/main`
- **`next`** — reset session to start fresh
- **`diagnose`** — disciplined diagnosis loop for hard bugs and perf regressions
- **`tdd`** — red-green-refactor with deep-modules / interface-design / mocking guidance
- **`prototype`** — build a throwaway prototype to flesh out a design
- **`improve-codebase-architecture`** — find deepening opportunities in a codebase
- **`grill-me`** / **`grill-with-docs`** — stress-test a plan; the docs variant updates `CONTEXT.md` and ADRs inline
- **`triage`** — state-machine-driven issue triage
- **`to-issues`** — turn a plan into tracer-bullet issues
- **`to-prd`** — turn the current context into a PRD
- **`zoom-out`** — step back from the weeds

### Design & UX

- **`frontend-design`** — distinctive, production-grade frontend interfaces
- **`audit`** — interface quality audit (a11y, perf, theming, responsive)
- **`critique`** — UX critique with hierarchy / IA / emotional resonance
- **`polish`** — final pre-ship pass for alignment, spacing, detail
- **`extract`** — pull reusable components / tokens into the design system
- **`normalize`** — align design to the system
- **`teach-impeccable`** — one-time setup that captures design context
- **`onboard`** — onboarding flows, empty states, first-time UX
- **`harden`** — error handling, i18n, overflow, edge cases
- **`distill`** — strip designs to their essence
- **`delight`** — joy, personality, unexpected touches
- **`animate`** — purposeful motion and micro-interactions
- **`adapt`** — cross-device / cross-screen-size adaptation
- **`optimize`** — load speed, rendering, animations, bundle size
- **`bolder`** / **`quieter`** — amplify or tone down intensity
- **`colorize`** — strategic color additions
- **`clarify`** — UX copy, microcopy, error messages
- **`walkthrough`** — open each new feature in Chrome and narrate the UX pass

### Productivity & meta

- **`handoff`** — compact the conversation into a handoff doc for the next agent
- **`grill-me`** — interview-style design pressure test
- **`caveman`** — ultra-compressed communication mode (~75% fewer tokens)
- **`write-a-skill`** — scaffold a new skill with proper structure
- **`setup-matt-pocock-skills`** — bootstrap project context for the workflow skills

### Personal & misc

- **`edit-article`** — restructure and tighten article drafts
- **`obsidian-vault`** — search, create, manage notes with wikilinks
- **`codex-review`** — run OpenAI Codex review on the current branch, fix P0/P1, commit
- **`setup-pre-commit`** — Husky + lint-staged + typecheck + tests
- **`git-guardrails-claude-code`** — Claude Code hooks blocking dangerous git commands
- **`scaffold-exercises`** — exercise dir scaffolding for courses
- **`migrate-to-shoehorn`** — replace `as` in tests with `@total-typescript/shoehorn`

## Attribution

A large portion of these skills come from [mattpocock/skills](https://github.com/mattpocock/skills) — specifically the `engineering/`, `misc/`, `personal/`, and `productivity/` categories. Huge thanks to Matt for publishing them.

## License

MIT
