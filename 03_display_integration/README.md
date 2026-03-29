# Module 3: Display Integration

## Module overview (read this when you enter Module 3)

**What this module is:** Module 2 gave you a **parametric Pi 4**—a reference **PCB solid** with holes. Module 3 is **not** more Pi work. Here you model the **HMTECH 7″ LCD panel’s frame**: the **bezel** (the part that surrounds the **viewing window**), the **opening** the panel passes through, and **clearance** so the real screen is not jammed. The reference display is an **LCD module**, not a touchscreen—**arcade controls** (Module 4) handle input. That bezel is a **printed (or fabricated) part** you will mate to the **outer shell** in Module 5; the Pi board sits **behind** the stack and is located with Module 2’s geometry.

**Why a second spreadsheet:** Screen width/height (**165 × 104 mm** here) belong in **`Spreadsheet_Bezel`**, not in **`Spreadsheet_Pi`**. Mixing Pi and display parameters in one sheet makes later edits risky; **`fx`** expressions still use names like **`Spreadsheet_Bezel.Screen_W`**.

**Two new tree objects from the start:** You need (**1**) a **Part Design body** **`Body_Bezel`**—the container for all bezel **sketches, pads, pockets,** etc.—and (**2**) **`Spreadsheet_Bezel`** for those two dimensions (and any you add later). Many FreeCAD builds only let you add the **second** spreadsheet when a **Body** is active, so **creating `Body_Bezel` first is normal** and is the **recommended** opening move below.

**See also:** [architecture.md](../architecture.md) (layers: bezel + screen vs shell vs Pi), [component_specs.md](../component_specs.md) (display numbers).

---

## What you're building (short)

**Cutout** means **material removed** from a part so you get a **hole or window** (in FreeCAD, often a **Pocket** through a pad, or a boolean cut). In Module 3 the important cutout is the bezel **opening**: the **viewing window** where the LCD **active area** shows through, sized with a little **clearance** so the display front / panel edges are not pinched. Later, Module 5 adds **port cutouts** in the **shell** (USB, power)—same idea, different face.

The **bezel / frame geometry** for the **HMTECH 7\" display panel**: that **opening**, clearance (tolerance), and how it **mounts** relative to the rest of arci.

---

## At the start of Module 3 — do this first in FreeCAD

Use this list when you **have not started Module 3 yet** (nothing in the tree for the bezel except maybe an empty **`Body_Bezel`** you are about to create).

1. **Create `Body_Bezel`:** Open the **Part Design** workbench. Start a new body with **Create body** (toolbar: icon of a solid with a **+**; on some versions **Part Design → Create body** in the menu). A new **`Body`** appears in the **Model** tree with only **Origin** inside. Select it, press **F2** (or right-click → **Rename**) and type **`Body_Bezel`**. No sketch yet—this is just the **container** for bezel geometry.
2. **Create `Spreadsheet_Bezel`:** With **`Body_Bezel`** **selected** in the tree, switch to **Spreadsheet** → new spreadsheet → rename **`Spreadsheet_Bezel`**. It may appear **under** **`Body_Bezel`**; that is fine.  
   - **Alternate:** If your build allows it, select the **document** node first, create the spreadsheet, and get **`Spreadsheet_Bezel`** at document level—then ensure **`Body_Bezel`** exists before Step 2 sketching (create it in Step 2 if needed).
3. **Aliases:** In two cells (e.g. **A1** / **A2**), enter **`165`** and **`104`**, then set **cell aliases** **`Screen_W`** and **`Screen_H`** (same idea as **`Pi_Width`** / **`Pi_Height`** in Module 2—**Data / Alias** on each cell).
4. **Check:** In any dimension **`fx`** field, you can type **`Spreadsheet_Bezel.Screen_W`** (adjust if your object name differs).

Steps below match **Step 1** and **Step 2** for **`completion.md`** tracking.

---

## Step 1: Screen Dimensions

- **Concept:** Same as the overview: **`Spreadsheet_Bezel`** holds display numbers; **`Body_Bezel`** is the geometry container. Path quirks are covered in **At the start of Module 3** above.

**Path A — spreadsheet at document level (if it works on your build):** Select the **document** node → **Spreadsheet** → new spreadsheet → **`Spreadsheet_Bezel`**. If **`Body_Bezel`** does not exist yet, create it in Step 2 before sketching.

**Path B — recommended for many builds (Body first, then sheet):**
- **Action:** **`Body_Bezel`** exists → select it → **Spreadsheet** → new spreadsheet → rename **`Spreadsheet_Bezel`** (often nested under the Body).
- **Action:** Cells **165** / **104**, aliases **`Screen_W`** / **`Screen_H`**.

- **Goal:** Centralize display dimensions; bezel sketches use **`Spreadsheet_Bezel.Screen_W`** / **`Screen_H`** in **`fx`**.

## Step 2: Creating the Bezel (plate + window)

**Why this is two steps in CAD:** A **Pocket** (a cut that makes a **hole**) only removes material from **existing solid**. If you sketch only the “hole” first, there is nothing to cut yet. So the usual pattern here is: **(1) Pad** a flat **bezel blank** from an **outer** rectangle, **(2) Pocket** through it using a second sketch for the **opening** the display module fits through.

**Prerequisites:** **`Body_Bezel`** exists, **`Spreadsheet_Bezel`** has **`Screen_W`** / **`Screen_H`** (165 / 104 per [component_specs.md](../component_specs.md)). If you used **Path A** and still have no body, create **`Body_Bezel`** now (**Part Design** → **Create body** → rename)—then continue.

### 2a — Outer bezel (solid blank)

**Names like `Pad_BezelBase`:** FreeCAD does **not** ship with that object. A **Pad** is the Part Design command that **extrudes** a closed sketch into **3D solid** (like **Pad** / **Pad001** in the tree). **`Pad_BezelBase`** is only a **suggested rename** (F2) after you create that first pad so the tree reads clearly. Until you finish step 6 below, your tree may show only **`Body_Bezel`** and **`Spreadsheet_Bezel`**—that is expected.

1. Select **`Body_Bezel`** in the tree (active Part Design body).
2. **Create sketch** on a **base plane** (e.g. **XY plane** of the body’s **Origin**, or **Datum plane**—same idea as Module 2: pick a plane you treat as the **front** of the bezel).
3. Draw a **rectangle** for the **outside** of the printed bezel (the material that will **surround** the window). Keep it **centered** on the origin if you can (easier symmetry later).
4. **Size (parametric):** In **`fx`**, make the outer rectangle **larger** than the screen outline—e.g. **width** `Spreadsheet_Bezel.Screen_W + 20 mm` and **height** `Spreadsheet_Bezel.Screen_H + 20 mm` (about **10 mm** of **frame** beyond the opening on each side; you can change **20** later).
5. Fully constrain the sketch (closed profile, position, dimensions).
6. **Close** the sketch → **Pad** the profile to a **small thickness** (printed plate: often **2–3 mm**; pick one value and stay consistent). Rename the pad if you like (e.g. **`Pad_BezelBase`**).

You should now see a **flat solid plate** in the 3D view.

### 2b — Screen opening (pocket), clearance, spreadsheet

**What “clearance” means here:** The kit’s **outer** size is **`Screen_W` × `Screen_H`**. The **cutout** must be **slightly larger** so the module is not pinched. For this course, use **+1 mm per axis** on the **opening** rectangle:

- **Opening width** = **`Spreadsheet_Bezel.Screen_W + 1 mm`**
- **Opening height** = **`Spreadsheet_Bezel.Screen_H + 1 mm`**

That makes the hole **1 mm wider** and **1 mm taller** than the nominal **165 × 104** outline—about **0.5 mm** gap **per side** if the opening stays **centered** on the outer rectangle. If a real print is tight, increase to **`+ 2 mm`** on one or both axes.

1. Select the **top face** of **the bezel pad** from **2a** (tree name may be **`Pad`**, **`Pad001`**, or **`Pad_BezelBase`** if you renamed it)—the face toward the **LCD**—or the **same plane** as the first sketch—then **Create sketch** (FreeCAD attaches the sketch to that face).
2. Draw a **rectangle** for the **opening** (the **viewing window** through the plate).
3. **Dimensions in `fx`:** set width and height to the expressions above (**`Spreadsheet_Bezel.Screen_W + 1 mm`**, **`Spreadsheet_Bezel.Screen_H + 1 mm`**).
4. **Center** the opening on the outer plate (equal offsets left/right and top/bottom—use **symmetric constraints** or equal dimensions to the plate edges).
5. **Close** the sketch → **Pocket** → **Through all** (or depth **≥** pad thickness) so you get a **clean hole** through the plate. Rename if you like (e.g. **`Pocket_ScreenOpening`**).

**Check:** From the front, you see a **frame** with a **rectangular hole**; recomputing the document changes the hole if you edit **`Screen_W`** / **`Screen_H`** or the **`+ 1 mm`** terms.

**Optional later:** Rounded corners on the opening, mounting lips, or shell mating features can come in **Module 5**; for **`completion.md`**, Step 2 is “done” when the **parametric opening** through a **padded** bezel blank exists.

---

## 📝 Progress Tracking

- After **Step 1** (spreadsheet + aliases): check **Module 3 → Step 1** in **`completion.md`**.
- After **Step 2** (pad + pocket opening as above): check **Module 3 → Step 2**; add a short milestone note if you like.
- When the whole module’s goals are satisfied for you, you can mark **Module 3** complete in **`completion.md`**.
