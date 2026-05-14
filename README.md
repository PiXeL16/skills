# skills

A curated collection of agent skills I use day to day. Drop them into `~/.claude/skills/` and they're available in every project, on every machine.

> **Skills** are small, self-contained instruction packs (a `SKILL.md` plus optional supporting files) that an agent loads on demand when its description matches the task. The format originated in Claude Code, but the underlying idea — natural-language playbooks that travel with you — is generic, and most modern coding agents now support it directly or via a thin adapter.

## Install

Clone and copy whatever you want into your skills directory:

```bash
git clone https://github.com/PiXeL16/skills.git
cp -R skills/skills/* ~/.claude/skills/
```

Or cherry-pick:

```bash
cp -R skills/skills/diagnose ~/.claude/skills/
cp -R skills/skills/tdd      ~/.claude/skills/
cp -R skills/skills/handoff  ~/.claude/skills/
```

Each top-level directory under `skills/` is one skill. Open the `SKILL.md` inside to see what it does and when it triggers.

## What's in here

**45 skills**, loosely grouped by intent.

### 🛠 Engineering workflow

The day-to-day "what am I doing right now" verbs.

| Skill | What it does |
|---|---|
| [`spec`](skills/spec/) | Refine a feature into a tracked epic with sub-issues |
| [`implement`](skills/implement/) | Implement an epic as a chain of stacked PRs |
| [`review`](skills/review/) | Address PR review comments methodically |
| [`topr`](skills/topr/) | Rebase a stacked PR onto `origin/main` cleanly |
| [`next`](skills/next/) | Reset the session and start fresh |
| [`diagnose`](skills/diagnose/) | Disciplined diagnosis loop for hard bugs and perf regressions |
| [`tdd`](skills/tdd/) | Red-green-refactor with bundled guidance on deep modules, mocking, and interface design |
| [`prototype`](skills/prototype/) | Build a throwaway prototype to flesh out a design before committing |
| [`improve-codebase-architecture`](skills/improve-codebase-architecture/) | Find deepening / consolidation opportunities |
| [`grill-me`](skills/grill-me/) · [`grill-with-docs`](skills/grill-with-docs/) | Stress-test a plan; the docs variant updates `CONTEXT.md` and ADRs inline |
| [`triage`](skills/triage/) | State-machine-driven issue triage |
| [`to-issues`](skills/to-issues/) | Turn a plan into tracer-bullet vertical-slice issues |
| [`to-prd`](skills/to-prd/) | Turn the current context into a PRD |
| [`zoom-out`](skills/zoom-out/) | Step back from the weeds |

### 🎨 Design & UX

A cohesive set of design skills that share a single source of design principles (`frontend-design`). Each one is a different lens.

| Skill | What it does |
|---|---|
| [`frontend-design`](skills/frontend-design/) | Create distinctive, production-grade interfaces that avoid generic "AI slop" aesthetics — the root skill |
| [`audit`](skills/audit/) | Comprehensive interface quality audit (a11y, perf, theming, responsive) |
| [`critique`](skills/critique/) | UX critique covering hierarchy, IA, and emotional resonance |
| [`polish`](skills/polish/) | Final pre-ship pass for alignment, spacing, and detail |
| [`extract`](skills/extract/) | Pull reusable components / tokens into the design system |
| [`normalize`](skills/normalize/) | Align design to the established system |
| [`teach-impeccable`](skills/teach-impeccable/) | One-time setup that captures durable design context |
| [`onboard`](skills/onboard/) | Onboarding flows, empty states, first-time UX |
| [`harden`](skills/harden/) | Error handling, i18n, overflow, edge cases |
| [`distill`](skills/distill/) | Strip designs to their essence |
| [`delight`](skills/delight/) | Joy, personality, unexpected touches |
| [`animate`](skills/animate/) | Purposeful motion and micro-interactions |
| [`adapt`](skills/adapt/) | Cross-device, cross-screen-size adaptation |
| [`optimize`](skills/optimize/) | Load speed, rendering, animations, bundle size |
| [`bolder`](skills/bolder/) · [`quieter`](skills/quieter/) | Amplify or tone down visual intensity |
| [`colorize`](skills/colorize/) | Strategic color additions |
| [`clarify`](skills/clarify/) | UX copy, microcopy, error messages |
| [`walkthrough`](skills/walkthrough/) | Open each new feature in Chrome and narrate a guided UX pass |

### 🧠 Productivity & meta

| Skill | What it does |
|---|---|
| [`handoff`](skills/handoff/) | Compact the conversation into a handoff doc for the next agent |
| [`caveman`](skills/caveman/) | Ultra-compressed communication mode (~75% fewer tokens) |
| [`write-a-skill`](skills/write-a-skill/) | Scaffold a new skill with proper structure and progressive disclosure |
| [`setup-matt-pocock-skills`](skills/setup-matt-pocock-skills/) | Bootstrap the project context the engineering skills expect |

### 📒 Personal & misc

| Skill | What it does |
|---|---|
| [`edit-article`](skills/edit-article/) | Restructure and tighten article drafts |
| [`obsidian-vault`](skills/obsidian-vault/) | Search, create, and link notes in an Obsidian vault |
| [`codex-review`](skills/codex-review/) | Run an OpenAI Codex review on the current branch, fix P0/P1, commit |
| [`setup-pre-commit`](skills/setup-pre-commit/) | Husky + lint-staged + typecheck + tests, set up in one shot |
| [`git-guardrails-claude-code`](skills/git-guardrails-claude-code/) | Hooks that block destructive git commands before they run |
| [`scaffold-exercises`](skills/scaffold-exercises/) | Exercise directory scaffolding for course content |
| [`migrate-to-shoehorn`](skills/migrate-to-shoehorn/) | Replace `as` assertions in tests with `@total-typescript/shoehorn` |

## Inspiration & credits

This collection wouldn't exist without people generously publishing their work.

### 🧑‍🏫 [`mattpocock/skills`](https://github.com/mattpocock/skills)

The entire **engineering workflow** category, plus the **productivity & meta** skills (apart from `handoff`-style helpers I'd already adopted), come from Matt Pocock's public skills repo — specifically the `engineering/`, `misc/`, `personal/`, and `productivity/` directories. Matt's `diagnose`, `tdd`, `prototype`, `grill-me`, `to-issues`, `to-prd`, and `triage` are particularly excellent — they encode a coherent way of working that pays off across projects.

If you want the canonical, kept-up-to-date versions, go to the source.

### 🎨 The "Impeccable" design skill pack

The design category (`frontend-design`, `audit`, `polish`, `critique`, `bolder`, `quieter`, `colorize`, `distill`, `delight`, `harden`, `adapt`, `extract`, `normalize`, `onboard`, `optimize`, `animate`, `clarify`, `teach-impeccable`, `walkthrough`) is built around the **Impeccable** design skill pack. Its root skill, `frontend-design`, carries an explicit `license: Apache 2.0. Based on Anthropic's frontend-design skill.` line in its frontmatter — so the lineage is:

```
Anthropic's official frontend-design skill (Apache-2.0)
    └── Impeccable design pack (Apache-2.0, derivative)
            └── this collection
```

The other design skills (`audit`, `polish`, …) chain into `frontend-design` as their single source of design principles, which is how the pack stays cohesive.

### 🛠 My own additions

A small handful are mine:

- `spec`, `implement`, `review`, `topr`, `next` — the stacked-PR workflow I use for shipping multi-issue features
- `codex-review` — pairs nicely with `review` for a structured second opinion before merging
- `walkthrough` — a guided UX pass over a branch's new surfaces before shipping

These borrow liberally in spirit from the two collections above.

## License

- **My own skills** (`spec`, `implement`, `review`, `topr`, `next`, `codex-review`, `walkthrough`) are MIT — see `LICENSE`.
- **`frontend-design`** is Apache-2.0, inherited from Anthropic's upstream skill (per its own frontmatter).
- **Skills imported from `mattpocock/skills`** retain whatever license is set there; this repo redistributes them with attribution. Please check the upstream for the authoritative terms.

If you're the author of a skill in here and want it removed, attributed differently, or relicensed — open an issue and I'll fix it the same day.

## Contributing

This is primarily my personal toolkit, but PRs that improve attribution, fix bugs in the skills I authored, or add useful new ones are welcome.
