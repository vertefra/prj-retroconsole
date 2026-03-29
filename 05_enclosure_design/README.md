# Module 5: Enclosure Design

## What you're building
The **outer shell** of arci: a **hollowed body** with chosen **wall thickness** and **cutouts** for ports (USB, power, etc.). This is the part that **wraps** the Pi, screen, fan, and controls into one **printable or fabricable** enclosure.

## Naming in the tree

Model the enclosure in a Part Design body renamed **`Body_Shell`**. It **mates** in intent with **`Body_Bezel`**, **`Body_FanMount`**, **`Body_ControlPanel`**, and the Pi reference from earlier modules ([architecture.md](../architecture.md)).

## Step 1: Shelling
- **Action:** With **`Body_Shell`** active, use the `Thickness` tool in `PartDesign` to hollow out your main solid.
- **Action:** Set the wall thickness to 3mm (ideal for 3D printing).
- **Goal:** Create internal volume for electronics.

## Step 2: Port Cutouts
- **Action:** With **`Body_Shell`** active, reference `component_specs.md` to create the USB and Power cutouts.
- **Goal:** External connectivity.

---

## 📝 Progress Tracking
- **Action:** Update `completion.md` in the root directory to reflect that you have completed Module 5.
- **Goal:** Maintain an accurate record of your progress.
