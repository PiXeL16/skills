---
name: walkthrough
description: Open each piece of new functionality from the current branch in Chrome one-by-one, summarize it with Claude's perception, and wait for the user's feedback before advancing. Used after a sprint to do a guided UX pass before merging or shipping.
args:
  - name: base
    description: Git ref to diff against to find "new" functionality (default main).
    required: false
  - name: scope
    description: Optional path filter (e.g. apps/web) to narrow which surfaces count as UI.
    required: false
user-invokable: true
---

Guided UX walkthrough of new functionality on the current branch. Open each touched surface in Chrome, give a short summary + your honest perception, then **stop and wait** for the user's feedback. Advance only when the user signals to proceed.

The user (Chris) drives the pace. Do not batch multiple surfaces into one message. One surface, one summary, one pause.

## Step 1 — Discover the surfaces

Find UI surfaces touched on the current branch versus the base ref:

```sh
git branch --show-current
git diff --name-only <base>...HEAD
```

Filter to UI-relevant files. For this repo and most React/Next/Astro projects, that means:

- `apps/*/src/routes/**`
- `apps/*/src/components/**`
- `apps/*/src/pages/**` (if Next/Astro)

Ignore: tests, schemas, server-only routers, migrations, scripts, config, lock files.

**Group changes into "surfaces."** A surface is a distinct user-visible screen or flow, NOT a file. Multiple files under one route directory collapse into one surface. Examples:

- 5 files under `routes/_app/clients/**` → one surface: "Clients"
- A new sheet component + a route change → one surface (the route that hosts it)
- A shared StatCard refactor that touched 6 pages → six surfaces (one per page that adopted it)
- A new tRPC procedure with no UI consumer → SKIP (not user-facing)

Map each surface to a URL path the user can visit (e.g. `/clients`, `/settings?tab=inbox`, `/knowledge/entity/<some-real-id>`).

## Step 2 — Confirm the plan

Before opening Chrome, show the user the surface list in this format:

```
Walkthrough plan — N surfaces:
1. /clients — new side sheets + summary cards
2. /projects — billable toggle + archived hidden by default
3. /knowledge — view toggle in header + summary stats
…
```

Ask: "Ready to start with #1? Or want to reorder / drop any?"

Wait for the user's go-ahead. Do not start touring without confirmation.

## Step 3 — Verify a dev server is running

You need a running app to walk through. Check for the project's typical dev port (3000 / 3035 / 4000 / 5173 etc — read package.json or Procfile if unsure). If nothing is listening:

```sh
lsof -nP -iTCP -sTCP:LISTEN 2>/dev/null | grep -E '300[0-9]|517[0-9]'
```

If no dev server is up, tell the user and ask them to start it (e.g. `make dev` or `pnpm dev`). Don't try to start it yourself unless they ask — dev servers vary per project.

## Step 4 — Walk one surface at a time

For each surface in order:

1. **Load Chrome MCP tools if not already loaded.** Browser tools are deferred:
   ```
   ToolSearch with query "select:mcp__claude-in-chrome__tabs_context_mcp,mcp__claude-in-chrome__navigate,mcp__claude-in-chrome__read_page"
   ```
   Load others (find, javascript_tool, get_page_text) as needed for the specific surface.

2. **Open the surface.** Either reuse the active tab via `tabs_context_mcp` + `navigate`, or open a new tab if the user is using their browser for something else.

3. **Read the page** with `read_page` (or `get_page_text` for a leaner snapshot). Look for:
   - Layout structure — does it match the design system?
   - Empty/loading/error states — do they render?
   - Color discipline — is red reserved for genuine "bad" states?
   - Microcopy — does the page read calm and confident, or jargony?
   - Interactive affordances — buttons / inputs / side sheets actually present?

4. **Give the user a short report.** Keep it to 4-7 lines. Structure:

   ```
   ### /<path> — <surface name>

   What changed: <1 sentence>

   What I see now: <2-3 bullets on the current rendered state>

   My perception: <1-2 sentences — honest read. Mention anything off:
   spacing, copy, color, layout, missing affordances, broken states>

   Suggested next: <"proceed", or 1-2 specific tweaks if I see issues>
   ```

5. **Stop. Wait for the user.** Do not move to the next surface, do not call more tools. Just sit on the report.

   The user might:
   - Say "next" / "proceed" / "looks good" → advance to the next surface
   - Ask follow-up questions → answer, then re-confirm before advancing
   - Request a tweak → make the change, re-verify in Chrome, report back, then wait again
   - Request a screenshot or zoom into a specific area → comply, then wait

## Step 5 — Final report

When all surfaces are toured, summarize:

- How many surfaces reviewed
- Tweaks made during the walk (with file paths)
- Anything the user flagged that wasn't fixed (queue for follow-up)
- Whether all surfaces are user-approved

If tweaks were made, ask whether to commit them now or batch with other work.

## Anti-patterns (don't)

- **Don't dump all surfaces in one message.** One at a time. The user wants a paced review, not a wall of text.
- **Don't skip the "wait for feedback" step.** Even if a surface looks perfect, stop. The user might still see something you missed.
- **Don't fabricate observations.** If `read_page` didn't show the relevant detail, say so and offer to use `get_page_text` or `javascript_tool` to inspect deeper.
- **Don't be sycophantic.** "My perception" means honest. If a header is louder than the design system says it should be, say it. If copy is jargony, say it. The user trusts you more when you flag real concerns.
- **Don't expand scope.** If you spot an unrelated bug while touring, note it for the final report — don't go fix it mid-walk.
- **Don't auto-advance.** "Looks good to me, moving on…" is the wrong move. The user signals advance; you don't.

## When to use this skill

- After a sprint of UI work, before merging the branch
- Before recording a demo or sending a stakeholder update
- When the user wants to validate a design-system rollout across multiple pages
- After a port from another product (Midday → Goldenberry-style work)

## When NOT to use this skill

- For backend-only changes (no UI to walk through)
- For trivial 1-file tweaks (just diff and ship)
- When no dev server can be started (e.g. CI environment)
