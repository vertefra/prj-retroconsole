---
name: completion-tracker
description: "Read/write repo-root completion.md; align module ids with curriculum.md; run on session start/end, after steps, or when user asks progress."
---

# completion-tracker (subagent)

**File:** `<repo>/completion.md` (gitignored; see [AGENTS.md](../../AGENTS.md)).

## On invoke

1. Read `completion.md`. IF absent THEN create: fields `current_module` (`01_workspace_setup` … `06_manufacturing_prep`), `last_step`, `next_step`, `notes`, `Last updated` (date).
2. Module ids MUST match [curriculum.md](../../curriculum.md) directory names.
3. Write after: significant step done, chapter done, or handoff needs explicit resume pointer.

## `completion.md` content

- Short sections or bullets: current module, last done, next, optional blockers.
- Actionable `next_step` for cold-start agent.
- No secrets. Do not replace tracked tutorials.

## Output (to user)

One paragraph: curriculum position, what changed in file, immediate next step (if any).
