# Module 2: The Core (Raspberry Pi 4)

## What you're building
A **parametric model of the Raspberry Pi 4 board** in CAD: the **PCB outline** (real-world width × height; real boards have **rounded corners**, see reference table) and the **four mounting holes** on the correct spacing. That geometry is the **reference “brain”** of the console—later modules (screen, fan, shell, mounts) will align to it so the digital assembly matches physical parts.

## Pi model dimensions (reference)

Single place for **numbers the Pi model uses** today. Keep them aligned with [component_specs.md](../component_specs.md) §1 and the [mechanical drawing](https://datasheets.raspberrypi.com/rpi4/raspberry-pi-4-mechanical-drawing.pdf). **Extend this table** when you add ports, keepouts, or more spreadsheet-driven geometry—add a row here and a matching **cell alias** in the spreadsheet, then reference it from sketches or Pad via **`fx`** (e.g. `Spreadsheet001.Pi_Hole_Pitch_X`).

| Quantity | Value (mm) | Spreadsheet alias in this course | Where it appears |
|----------|------------|----------------------------------|------------------|
| PCB width | 85.0 | **`Pi_Width`** (Step 1) | Board rectangle |
| PCB height | 56.0 | **`Pi_Height`** (Step 1) | Board rectangle |
| PCB corner radius | 3.0 | *Suggested later:* `Pi_PCB_Corner_Radius` | Real outline; optional **Fillet** after Pad (Step 4) |
| PCB slab thickness (Pad) | 1.6 typical | *Suggested later:* `Pi_PCB_Thickness` | Part Design **Pad** after sketch |
| Mounting hole diameter | 2.75 | *Suggested later:* `Pi_Hole_Diameter` | Step 3 circles |
| Hole pitch, left–right columns (center–center) | 58.0 | *Suggested later:* `Pi_Hole_Pitch_X` | Step 3 |
| Hole pitch, bottom–top rows (center–center) | 49.0 | *Suggested later:* `Pi_Hole_Pitch_Y` | Step 3 |
| Inset, long edge → **tight** hole column | 3.5 | *Suggested later:* `Pi_Hole_Inset_Long_Tight` | Step 3 — pair with PDF / USB side |
| Inset, other long edge → **other** column | 23.5 | *Suggested later:* `Pi_Hole_Inset_Long_Other` | Step 3 |
| Inset, short edge → hole row (top and bottom) | 3.5 | *Suggested later:* `Pi_Hole_Inset_Short` | Step 3 |

**Suggested aliases** are optional until you add them to the sheet; Steps 1–3 may still use typed numbers in constraints. Migrating those numbers to aliases keeps one source of truth as the model grows.

## Organize the tree (rename things)

A **readable Model tree** is part of the workflow: you always know which object is the Pi, which sketch is the board outline, and expressions still use the **spreadsheet object name** (e.g. `Spreadsheet001`)—renaming the **Body** does not break `Spreadsheet001.Pi_Width`.

**How to rename:** In the **Model** tree, click an object, press **F2**, type the new name, Enter—or **right‑click → Rename** (wording varies by version).

**Where the spreadsheet lives:** The spreadsheet should sit **under the document** (`Unnamed` / your file name), **sibling** to **Bodies**—**not** nested inside a **Body**. If yours ended up inside `Body`, **drag** it to the document root in the tree.

**Suggested names for Module 2** (adjust if you prefer; stay consistent for later modules):

| Object | Suggested name | When |
|--------|----------------|------|
| Spreadsheet | `Spreadsheet_arci` (or keep `Spreadsheet001` and rename only bodies) | After creating it (Step 1) |
| Part Design Body | `Body_Pi` or `Pi_Board` | After creating the Body (Step 2) |
| Board + holes sketch | `Sketch_Pi_board` | After creating the sketch (Step 2–3) |
| Pad | `Pad_Pi_board` | After Step 4 |
| Corner fillet(s) | `Fillet_Pi_corners` (one feature with four edges is ideal; if you have several fillets, rename or merge when you know how) | After filleting (Step 4) |

Later modules add more **Bodies** (`Body_Bezel`, `Body_Shell`, …) using the same idea: **one Body per logical part**, **clear sketch / Pad names**.

## Step 1: Parametric Spreadsheet
- **Action:** Go to the `Spreadsheet` workbench and create a new spreadsheet.
- **Concept:** A **named value** is a **cell alias**. The number stays **in the cell**; the alias is a label you set in that cell’s **Properties** so constraints and expressions can refer to it (e.g. `Spreadsheet.Pi_Width`). If your sheet is auto-named `Spreadsheet001`, use that object name instead of `Spreadsheet`.
- **Action:** Select a cell (e.g. **A1**), type **`85`**, press Enter.
- **Action:** With the cell still selected, open **Properties** and set **Alias** to **`Pi_Width`** (use a valid identifier: letters, digits, underscore; no spaces).
- **Action:** Repeat for height: e.g. **A2** → value **`56`** → alias **`Pi_Height`**.
- **Note:** You are **not** typing `Pi_Width = 85` into the cell—that phrase only describes the idea. The cell holds **`85`**; **`Pi_Width`** is the separate **Alias** field.
- **Goal:** Board dimensions live in the spreadsheet so you can change them later without redrawing manually.
- **Action — name it:** Rename the spreadsheet object in the tree (e.g. **`Spreadsheet_arci`**) and confirm it sits **at document root**, not inside a Body ([details](#organize-the-tree-rename-things)).
- **See also:** [Pi model dimensions (reference)](#pi-model-dimensions-reference) for the full list and future aliases.

## Step 2: Initial Sketch
- **Action:** Switch the workbench dropdown to **`Part Design`** (full name in the list—not **`Part`**). **`Part`** is a different workbench and has **no Body**; if you are in `Part`, you will not see Body tools.
- **Concept:** A **`Body`** is a Part Design container for one chain of features (sketches, pads, …) that build a single solid. You need it before the usual Part Design sketch → pad workflow.
- **Action — create a Body:** With **`Part Design`** active, use **Create body** on the Part Design toolbar (tooltip often “Create body”; icon is often a small origin/block). If you do not see that toolbar, **right‑click the empty strip below the menu bar** → enable **Part Design**, or use the menu **Part Design → Create body** if your build exposes it. A **Body** should appear in the tree (with an **Origin** under it).
- **Action — rename the Body:** Rename it to **`Body_Pi`** or **`Pi_Board`** ([naming guide](#organize-the-tree-rename-things)).
- **Action — shortcut:** Alternatively click **Create sketch**; if no body exists, FreeCAD often **prompts to create a Body**—accept it, then choose the **XY plane** (e.g. under the Body’s **Origin**).
- **Action:** Create a new **`Sketch`** on the **XY** plane (attached to the Body).
- **Action — rename the sketch:** e.g. **`Sketch_Pi_board`**.
- **Action:** Draw a rectangle and add **dimensional** constraints so width and height come from the spreadsheet:
    - Use **Horizontal dimension** and **Vertical dimension** in the Sketcher toolbar (names may appear as such in the tooltip).
    - **Select a line** for each dimension—the line highlights **blue** when selected; apply one tool for board **width**, the other for **height** (match each to the correct edge orientation).
    - When the dimension dialog appears, click **`fx`** (expression editor). That opens the field where you can type or pick **`Spreadsheet…`** with autocompletion, then the alias (e.g. `Spreadsheet001.Pi_Width` / `Spreadsheet001.Pi_Height`—use your sheet’s name from the tree). You may not see spreadsheet completion until **`fx`** is used.
- **Goal:** Create the basic PCB footprint.
- **Note (shape):** A plain **rectangle** is fine for clearance checks. The real Pi 4 PCB has **3.0 mm** radius on all four outer corners ([component_specs.md](../component_specs.md)). To match that in 3D, easiest path is often: **Pad** first, then **Part Design → Fillet** the **four vertical outer corner edges** of the slab with radius **3.0 mm** (or rebuild the outline with sketch arcs).

## Step 3: Mounting Holes
- **Concept:** **Construction geometry** means sketch lines (or arcs) you use **only as references** for constraints—they usually show **dashed**. FreeCAD ignores them when building 3D from the sketch. The **3D step** (later) is **Pad** in Part Design: it takes your **flat sketch** and gives it **thickness** so you get a solid board—like pulling a flat cookie cutter shape upward into a block. **Pad uses the normal (solid) edges of the sketch** (your rectangle and circles); **construction lines are not part of that**—they are only guides. (Other programs call this “extrude”; FreeCAD’s usual name is **Pad**.) Draw a line, select it, then use **Toggle construction geometry** (Sketcher toolbar or context menu; name varies slightly by FreeCAD version). If you prefer to skip construction lines, use **horizontal/vertical distances** between hole centers plus **edge insets** from `component_specs.md` (Pi 4 is **not** left-right symmetric—do **not** rely on “center the holes on the rectangle” unless you have checked the official drawing).
- **Action — get into the sketch:** In the **Model** tree (left), **double‑click** the sketch that has your rectangle—or select it and press **Edit sketch** / the pencil-style control. The **Sketcher** workbench should activate and you are **editing** that sketch (not a new one).
- **Action — holes are circles:** On the **Sketcher** toolbar, choose **Create circle** (circle icon; tooltip often “Create circle by center”). **First click** = hole **center**. **Second click** = any point on the **edge** of the circle (rough size is OK). The circle is the **hole cross‑section** in the sketch; a later **Pocket** (or cutting Pad) will turn it into a real hole through the board—you are only drawing the **round outline** here.
- **Action — hole size:** Select the circle, use **Dimension → diameter** (or the diameter constraint tool), set **2.75 mm** (see `component_specs.md`). Repeat for each circle once all four exist.

### Pinning where the holes sit (read this if CAD is new)
So far each circle has a **size**. The **centers** can still slide until you add **constraints**—extra rules FreeCAD must obey (fixed distances, “these two points line up,” and so on).

**Names for the four holes (pick names that match your screen):** imagine the board as a table: **bottom-left**, **bottom-right**, **top-left**, **top-right**. The rest of the steps use those names.

**A — Make the left column one straight line:** You need **two circles** on the left first (both with ø 2.75 mm). The **Horizontal** and **Vertical** alignment constraints in Sketcher do **not** work on a **single** point—FreeCAD will say it cannot constrain that item. They always compare **two points** (or a line). **Order that usually works:** (1) Click the **Vertical** constraint icon once (tool stays active). (2) Click the **center point** of the **bottom-left** circle—the small dot in the middle, not the circle’s edge. (3) Click the **center point** of the **top-left** circle. That forces both centers to share the same left-right position (a straight column).

**B — Make the right column one straight line:** **Vertical** tool → **bottom-right** center → **top-right** center.

**C — Make the bottom row one straight line:** **Horizontal** tool → **bottom-left** center → **bottom-right** center (same height).

**D — Make the top row one straight line:** **Horizontal** tool → **top-left** center → **top-right** center.

### How to “set a distance” in Sketcher (click order)
You are looking for **driving dimensions**—numbers FreeCAD must satisfy—not the align tools (**Horizontal** / **Vertical**) you used for columns and rows.

- **Between two hole centers (steps E and F):** Use **Horizontal distance** or **Vertical distance** (same family of tools you used for the **85 mm** and **56 mm** rectangle sizes—icons often show a dimension with a small **H** or **V**). **Click the tool once**, then **click the first center point** (small dot in the middle of a circle), then **click the second center point**. A dialog opens: type **58** or **49** and confirm.  
  - **E:** **Horizontal distance** → **bottom-left** center → **bottom-right** center → **58 mm** (only makes sense after step **C**, so the bottom row is level).  
  - **F:** **Vertical distance** → **bottom-left** center → **top-left** center → **49 mm** (after step **A**, left column is straight).

- **From a hole to a side of the board (step G):** Use the general **Distance** constraint (often a single “dimension” icon without H/V—tooltip may say **Distance** or **Length**). **Click the tool once**, then **click the hole center**, then **click the rectangle edge as a line** (the actual **segment** of the outline, not empty space). Enter the values in step **G** below. That measures the **shortest gap** from the point to the line—which, for a straight board edge, is the inset you want.

**E — How wide is the hole pattern:** **Horizontal distance** between **bottom-left** and **bottom-right** centers → **58 mm**.

**F — How tall is the hole pattern:** **Vertical distance** between **bottom-left** and **top-left** centers → **49 mm**.

**G — Slide the pattern to the correct place on the board:** The board rectangle is **85 mm** wide and **56 mm** tall. On a real **Pi 4**, the holes are **not** centered left-to-right on the PCB: one column sits **3.5 mm** from its long edge, the other **23.5 mm** from the opposite long edge (**3.5 + 58 + 23.5 = 85**). Vertically it is **3.5 mm** from **both** short edges (**3.5 + 49 + 3.5 = 56**). Match your sketch to the [mechanical drawing](https://datasheets.raspberrypi.com/rpi4/raspberry-pi-4-mechanical-drawing.pdf) and your physical board (USB side, GPIO side).  
  - **Long edge with the “tight” column** ↔ those two hole centers → **3.5 mm**  
  - **Opposite long edge** ↔ the other column → **23.5 mm**  
  - **Bottom** short edge ↔ bottom row centers → **3.5 mm**  
  - **Top** short edge ↔ top row centers → **3.5 mm**  
  Use **Distance** (point → line) for each. If you already used the old **13.5 / 13.5** numbers, delete those dimensions and replace them with **3.5 / 23.5** on the long edges.

If FreeCAD complains the sketch is **over-constrained**, remove one duplicate rule and try again. When it works, you usually see **fully constrained** (often green) in the sketch status.

- **Optional (shorter CAD path):** **Symmetric mirroring from the rectangle center is wrong** for Pi 4 horizontal placement (the hole pattern is **not** left-right symmetric on the 85 mm outline). Prefer the **3.5 / 23.5 / 3.5 / 3.5** edge distances above, or trace the official PDF.
- **Goal:** Four holes that cannot move anymore, matching the Pi 4 mounting pattern.

## Step 4: Board thickness (Pad)

- **Action:** Close the sketch. In **Part Design**, with the sketch selected under **Body**, use **Pad** and set length to **1.6 mm** (typical PCB thickness), or to **`Spreadsheet001.Pi_PCB_Thickness`** once you add that alias (see [reference table](#pi-model-dimensions-reference)).
- **Action — rename the Pad:** e.g. **`Pad_Pi_board`** ([naming guide](#organize-the-tree-rename-things)).
- **Optional — rounded board outline:** Select the **Pad** in the tree, then **Fillet** and pick the **four outer vertical edges** where side faces meet (the “rim” corners). Set radius to **3.0 mm** (or `Spreadsheet001.Pi_PCB_Corner_Radius` if you add it).
- **Action — rename the Fillet:** e.g. **`Fillet_Pi_corners`** (if you used one fillet for all four edges; otherwise rename each feature so the tree stays readable).
- **Goal:** A thin solid board with through-holes (if the sketch inner circles are treated as holes by your Pad).

---

## 📝 Progress Tracking
- **Action:** Update `completion.md` in the root directory to reflect that you have completed Module 2.
- **Goal:** Maintain an accurate record of your progress.
