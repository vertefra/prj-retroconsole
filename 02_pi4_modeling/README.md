# Module 2: The Core (Raspberry Pi 4)

Modeling the heart of the arci console.

## Step 1: Parametric Spreadsheet
- **Action:** Go to the `Spreadsheet` workbench and create a new spreadsheet.
- **Action:** Enter `Pi_Width = 85` and `Pi_Height = 56`.
- **Goal:** Set up your board dimensions as variables for easy future adjustment.

## Step 2: Initial Sketch
- **Action:** Switch to `PartDesign`.
- **Action:** Create a new `Body`, then a new `Sketch` on the XY-Plane.
- **Action:** Draw a rectangle and constrain it using the spreadsheet values (press `=` in the constraint box to link to the spreadsheet).
- **Goal:** Create the basic PCB footprint.

## Step 3: Mounting Holes
- **Action:** Inside the same sketch, add four circles.
- **Action:** Use the **Symmetry** constraint to center them.
- **Action:** Constrain the spacing to 58mm x 49mm (per `component_specs.md`).
- **Goal:** Precision placement of holes.

---

## 📝 Progress Tracking
- **Action:** Update `completion.md` in the root directory to reflect that you have completed Module 2.
- **Goal:** Maintain an accurate record of your progress.
