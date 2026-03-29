# arci - Retro Console Design Project

This repository holds design notes and a **FreeCAD curriculum** for the **arci** retro console. It is updated **while the project is built**—live docs and rough edges are expected.

---

## For AI agents (tutorial delivery)

This repo is intended to be **ingested as the source of truth** for a **step-by-step, interactive FreeCAD tutorial**. If you are an agent guiding a student:

1. **Index and rules:** Read **[AGENTS.md](AGENTS.md)** first—module map, clarification workflow, when to ask for **screenshots** (FreeCAD UI), and how **`completion.md`** is used.
2. **Lesson order:** Follow **[curriculum.md](curriculum.md)** and each module’s **`README.md`** (`01_workspace_setup` … `06_manufacturing_prep`). Complete and verify **one step at a time** before advancing.
3. **Big picture:** Use **[architecture.md](architecture.md)** for how CAD bodies map to real hardware; **[component_specs.md](component_specs.md)** for dimensions.
4. **Student progress (local state):** Progress is tracked in **`completion.md`** at the repo root. That file is **gitignored**—it is **per-machine / per-student** state so sessions can **resume** without rereading the whole chat. **Create it** if missing; **update it** after meaningful steps (see AGENTS.md).
5. **Subagent for state:** Use the **Cursor subagent** **`completion-tracker`** (see [`.cursor/agents/completion-tracker.md`](.cursor/agents/completion-tracker.md)) to read or update **`completion.md`** so the **main conversation** stays focused on teaching while progress bookkeeping stays in a side context.
6. **Improving the curriculum:** If a step is unclear, wrong, or missing detail, **edit the relevant `README.md` / `curriculum.md` / specs** (smallest fix that removes the gap). Treat recurring confusion as a signal to patch the docs—not only to answer once in chat.

---

## For people following along

Use **[curriculum.md](curriculum.md)** and the module folders as the moving source of truth.

**How it all fits:** [architecture.md](architecture.md) explains which CAD pieces match which real parts and how they fit in the shell.

## Project Hardware
- **Core:** Raspberry Pi 4 Model B
- **Display:** HMTECH 7" Display (HTC6070V P01)
- **Cooling:** iUniker Pi Fan (4010)
- **Controls:** Sanwa-style Joystick and Arcade Buttons
- **IO:** USB Panel Mount Port (for OS configuration)

## Getting Started
1. Read [architecture.md](architecture.md) so you know what you are building and how modules relate.
2. Read [component_specs.md](component_specs.md) for technical data.
3. Follow [curriculum.md](curriculum.md) to design the enclosure in FreeCAD.

## Workflow
All CAD work should be performed in FreeCAD (Linux AppImage recommended). Use a **parametric** approach (spreadsheet aliases) where the tutorials suggest it.
