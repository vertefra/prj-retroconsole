# arci - Retro Console Design Project

This repository holds my design notes and FreeCAD curriculum for the **arci** retro console. I’m updating it **while I work through the project**—live docs, live structure, plenty of sweat and tears. Nothing here pretends to be a polished, “done” reference; you’ll see incremental edits, backtracking, and rough edges because that’s how it’s being built.

If you follow along, use the [curriculum](curriculum.md) and module READMEs as the moving source of truth.

**How it all fits:** Read [architecture.md](architecture.md) for the **holistic design**—which CAD pieces map to which real parts and how the shell, screen, Pi, fan, and controls attach conceptually.

## Project Hardware
- **Core:** Raspberry Pi 4 Model B
- **Display:** HMTECH 7" Display (HTC6070V P01)
- **Cooling:** iUniker Pi Fan (4010)
- **Controls:** Sanwa-style Joystick and Arcade Buttons
- **IO:** USB Panel Mount Port (for OS configuration)

## Getting Started
1.  Read [architecture.md](architecture.md) so you know what you are building and how modules relate.
2.  Read [component_specs.md](component_specs.md) for technical data.
3.  Follow [curriculum.md](curriculum.md) to design the enclosure in FreeCAD.

## Workflow
All CAD work should be performed in FreeCAD (Linux AppImage recommended). Ensure you use a parametric approach (Spreadsheets) for the best results.
