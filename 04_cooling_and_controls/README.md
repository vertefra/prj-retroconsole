# Module 4: Cooling and Controls

## What you're building
Two parts of the **user-facing hardware**: a **mount for the iUniker 40 mm fan** (airflow over the Pi) and the **arcade control layout**—hole pattern and spacing for **Qenker-style buttons** on the control surface. Together they define **cooling and input** in the same assembly as the Pi and display.

## Naming in the tree (bodies)

Use **separate Part Design bodies** and **F2** rename, same pattern as **`Body_Pi`** / **`Body_Bezel`** ([architecture.md](../architecture.md) — fan mount as **sub-part** or later part of the shell):

- **`Body_FanMount`** — **Step 1** fan footprint and **M3** pillars.
- **`Body_ControlPanel`** — **Step 2** joystick / button layout on the **control face**.

Create each with **Part Design → Create body**, then rename. Keep **Step 1** sketches and features under **`Body_FanMount`** and **Step 2** under **`Body_ControlPanel`**.

## Step 1: Fan Mounting
- **Action:** Ensure **`Body_FanMount`** is active → sketch a 40x40mm square for the iUniker fan footprint.
- **Action:** Create 32x32mm spaced mounting pillars (M3 size).
- **Goal:** Secure the core cooling system.

## Step 2: Arcade Layout
- **Action:** Ensure **`Body_ControlPanel`** is active → use your drawing tablet to trace your ideal button layout.
- **Action:** Create 30mm holes for main buttons and 24mm for start/select.
- **Goal:** Design a comfortable ergonomic control surface.

---

## 📝 Progress Tracking
- **Action:** Update `completion.md` in the root directory to reflect that you have completed Module 4.
- **Goal:** Maintain an accurate record of your progress.
