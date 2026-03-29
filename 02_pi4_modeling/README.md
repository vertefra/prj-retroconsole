# Module 2: The Core (Raspberry Pi 4)

## What you're building
A **parametric model of the Raspberry Pi 4 board** in CAD: the **rectangular PCB outline** (real-world width × height) and the **four corner mounting holes** on the correct spacing. That geometry is the **reference “brain”** of the console—later modules (screen, fan, shell, mounts) will align to it so the digital assembly matches physical parts.

## Step 1: Parametric Spreadsheet
- **Action:** Go to the `Spreadsheet` workbench and create a new spreadsheet.
- **Concept:** A **named value** is a **cell alias**. The number stays **in the cell**; the alias is a label you set in that cell’s **Properties** so constraints and expressions can refer to it (e.g. `Spreadsheet.Pi_Width`). If your sheet is auto-named `Spreadsheet001`, use that object name instead of `Spreadsheet`.
- **Action:** Select a cell (e.g. **A1**), type **`85`**, press Enter.
- **Action:** With the cell still selected, open **Properties** and set **Alias** to **`Pi_Width`** (use a valid identifier: letters, digits, underscore; no spaces).
- **Action:** Repeat for height: e.g. **A2** → value **`56`** → alias **`Pi_Height`**.
- **Note:** You are **not** typing `Pi_Width = 85` into the cell—that phrase only describes the idea. The cell holds **`85`**; **`Pi_Width`** is the separate **Alias** field.
- **Goal:** Board dimensions live in the spreadsheet so you can change them later without redrawing manually.

## Step 2: Initial Sketch
- **Action:** Switch the workbench dropdown to **`Part Design`** (full name in the list—not **`Part`**). **`Part`** is a different workbench and has **no Body**; if you are in `Part`, you will not see Body tools.
- **Concept:** A **`Body`** is a Part Design container for one chain of features (sketches, pads, …) that build a single solid. You need it before the usual Part Design sketch → pad workflow.
- **Action — create a Body:** With **`Part Design`** active, use **Create body** on the Part Design toolbar (tooltip often “Create body”; icon is often a small origin/block). If you do not see that toolbar, **right‑click the empty strip below the menu bar** → enable **Part Design**, or use the menu **Part Design → Create body** if your build exposes it. A **Body** should appear in the tree (with an **Origin** under it).
- **Action — shortcut:** Alternatively click **Create sketch**; if no body exists, FreeCAD often **prompts to create a Body**—accept it, then choose the **XY plane** (e.g. under the Body’s **Origin**).
- **Action:** Create a new **`Sketch`** on the **XY** plane (attached to the Body).
- **Action:** Draw a rectangle and add **dimensional** constraints so width and height come from the spreadsheet:
    - Use **Horizontal dimension** and **Vertical dimension** in the Sketcher toolbar (names may appear as such in the tooltip).
    - **Select a line** for each dimension—the line highlights **blue** when selected; apply one tool for board **width**, the other for **height** (match each to the correct edge orientation).
    - When the dimension dialog appears, click **`fx`** (expression editor). That opens the field where you can type or pick **`Spreadsheet…`** with autocompletion, then the alias (e.g. `Spreadsheet001.Pi_Width` / `Spreadsheet001.Pi_Height`—use your sheet’s name from the tree). You may not see spreadsheet completion until **`fx`** is used.
- **Goal:** Create the basic PCB footprint.

## Step 3: Mounting Holes
- **Concept:** **Construction geometry** means sketch lines (or arcs) you use **only as references** for constraints—they usually show **dashed**. FreeCAD ignores them when building 3D from the sketch. The **3D step** (later) is **Pad** in Part Design: it takes your **flat sketch** and gives it **thickness** so you get a solid board—like pulling a flat cookie cutter shape upward into a block. **Pad uses the normal (solid) edges of the sketch** (your rectangle and circles); **construction lines are not part of that**—they are only guides. (Other programs call this “extrude”; FreeCAD’s usual name is **Pad**.) Draw a line, select it, then use **Toggle construction geometry** (Sketcher toolbar or context menu; name varies slightly by FreeCAD version). If you prefer to skip construction lines, constrain hole centers with **horizontal/vertical distances** and **midpoint** constraints on the rectangle instead—same result, different tools.
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

- **From a hole to a side of the board (step G):** Use the general **Distance** constraint (often a single “dimension” icon without H/V—tooltip may say **Distance** or **Length**). **Click the tool once**, then **click the hole center**, then **click the rectangle edge as a line** (the actual **segment** of the outline, not empty space). Enter **13.5** or **3.5** as given below. That measures the **shortest gap** from the point to the line—which, for a straight board edge, is the inset you want.

**E — How wide is the hole pattern:** **Horizontal distance** between **bottom-left** and **bottom-right** centers → **58 mm**.

**F — How tall is the hole pattern:** **Vertical distance** between **bottom-left** and **top-left** centers → **49 mm**.

**G — Slide the pattern to the correct place on the board:** The board rectangle is **85 mm** wide and **56 mm** tall. Insets: **left** edge ↔ either **left** hole center → **13.5 mm**; **right** edge ↔ either **right** hole center → **13.5 mm**; **bottom** edge ↔ either **bottom** hole center → **3.5 mm**; **top** edge ↔ either **top** hole center → **3.5 mm**. Use **Distance** (point → line) as above for each.

If FreeCAD complains the sketch is **over-constrained**, remove one duplicate rule and try again. When it works, you usually see **fully constrained** (often green) in the sketch status.

- **Optional (shorter CAD path):** If you already like **construction lines** and **Symmetric**, you can instead use one hole, **29 mm** and **24.5 mm** from center axes, and mirror—same result, fewer words here, more Sketcher experience needed.
- **Goal:** Four holes that cannot move anymore, matching the Pi 4 mounting pattern.

---

## 📝 Progress Tracking
- **Action:** Update `completion.md` in the root directory to reflect that you have completed Module 2.
- **Goal:** Maintain an accurate record of your progress.
