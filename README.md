# arci — retro console (FreeCAD curriculum)

Design notes + stepwise FreeCAD lessons. Repo evolves with the build; expect drift.

## Agent tutorial delivery

**Order:** [AGENTS.md](AGENTS.md) → [curriculum.md](curriculum.md) → active `NN_topic/README.md`.

| Rule | Content |
|------|---------|
| Steps | One step per advance; verify; source = module `README.md`. End of each step: ask for screenshot + confirm user is unblocked; see [AGENTS.md](AGENTS.md) (End of each lesson step). |
| Teaching frame | MUST when user asks progress / next / resume / new chat: block = (what CAD next) + (fit: modules + hardware via architecture + component_specs); then actions. Forbidden: checklist-only / alias-only. |
| Tone | Short clear sentences; calm direct tutor voice. Multi-part answers: bullets or spaced paragraphs, not one packed paragraph ([AGENTS.md](AGENTS.md) Readability). Closing phrase verbatim per AGENTS. |
| Context files | [architecture.md](architecture.md) assembly; [component_specs.md](component_specs.md) dimensions. |
| State | `completion.md` at root (gitignored). Create if absent; update after meaningful progress; spec [AGENTS.md](AGENTS.md). |
| Subagent: state | [completion-tracker](.cursor/agents/completion-tracker.md) reads/writes `completion.md`. |
| Subagent: clarify | `[clarify]` → [clarify](.cursor/agents/clarify.md). Step how-to: numbered actions from module README first—not concepts only. Persist optional in `clarifications/`. |
| Marker: clarification | Prefix `[clarification]` → answer; IF tutorial unclear THEN minimal doc fix (`README.md` / `curriculum.md` / specs). |
| Curriculum fixes | IF step wrong or unclear THEN smallest edit to tracked docs; recurring confusion ⇒ patch source. |

## Humans: start here

1. [curriculum.md](curriculum.md) + module folders = lesson source.
2. [architecture.md](architecture.md) = CAD vs real parts.
3. [component_specs.md](component_specs.md) = numbers.

## Hardware

- SoC board: Raspberry Pi 4 Model B
- Display: HMTECH 7" (HTC6070V P01)
- Fan: iUniker 4010
- Controls: Sanwa-style stick + arcade buttons
- IO: USB panel mount (OS access)

## CAD

FreeCAD (Linux AppImage recommended). Parametric (spreadsheet aliases) where tutorials specify.
