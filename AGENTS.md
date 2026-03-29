# Repository Index (AGENTS.md)

This file provides a high-level map of the **arci** project repository.

> [!IMPORTANT]
> **Interactive Step-by-Step Style:**
> This repository is designed as a guided experience. Each module tutorial is structured as a sequence of granular steps. You should complete each step and verify the result before moving to the next.

## `[clarification]` (user marker)

When the user prefixes a message with **`[clarification]`**, they are asking about something that was **not clear from the prior explanation** in the tutorial or docs—not a casual follow-up.

**Agent workflow:**

1. **Answer** the clarification directly so the user can proceed.
2. **Verify** whether the gap was real (e.g. ambiguous wording, missing step, assumed prior knowledge). If the user simply misread or skipped a step, fix understanding only; no doc change is required.
3. **Improve the source** when verification shows the explanation was unclear: edit the relevant tutorial or index file (e.g. module `README.md`, `curriculum.md`) so future readers get the same clarity without needing to ask.

Prefer the smallest edit that removes the ambiguity (one sentence, one step, or one cross-link).

## Screenshots when helping with FreeCAD

FreeCAD state is hard to infer from short text (“Pad is greyed”, “sketch is red”, “wrong tree”). **Ask the user for one or more screenshots** when:

- The problem involves the **UI** (toolbars, task panel, which workbench), the **Model tree**, or **sketch constraints** / solver messages.
- The user’s description is vague or could match several causes.

**Useful shots (any subset):** the **main window** including **Model tree** and **3D view**; if a **task panel** or **constraint list** is open, include it; mention **FreeCAD version** if known.

This reduces guesswork and matches how this project has already been debugged in practice.

## 🏗️ Core Documentation
- **[README.md](README.md)**: Project overview, hardware list, and general introduction.
- **[architecture.md](architecture.md)**: Holistic system architecture—CAD pieces vs real parts, how they fit inside the shell, and module mapping.
- **[component_specs.md](component_specs.md)**: Technical reference for all hardware dimensions (Pi 4, Display, Fan, Controls).
- **[curriculum.md](curriculum.md)**: The main entry point for the FreeCAD course, indexing all teaching modules.

## 🎓 Learning Modules
Each folder below contains a step-by-step tutorial for a specific phase of the design.

1.  **[01_workspace_setup](01_workspace_setup/README.md)**: Installing FreeCAD and configuring the environment for Linux.
2.  **[02_pi4_modeling](02_pi4_modeling/README.md)**: Creating a parametric model of the Raspberry Pi 4.
3.  **[03_display_integration](03_display_integration/README.md)**: Designing the bezel and mounting for the HMTECH 7" screen.
4.  **[04_cooling_and_controls](04_cooling_and_controls/README.md)**: Integrating the iUniker fan and the Qenker arcade kit.
5.  **[05_enclosure_design](05_enclosure_design/README.md)**: Modeling the console shell and final assembly.
6.  **[06_manufacturing_prep](06_manufacturing_prep/README.md)**: Final inspection and exporting files for 3D printing/laser cutting.

## 📝 Project State Tracking
To maintain continuity between agent sessions, this repository uses a `completion.md` file (ignored by Git).

> [!IMPORTANT]
> **Agent First Action:**
> The first thing an agent should do is check for the existence of `completion.md` in the root directory. If it does not exist, create it.
> This file should be updated after every significant step or chapter completion to record the current state of the tutorial.

---
*Last Updated: 2026-03-29*
