# arci Hardware Component Specifications

Use these dimensions for creating your 3D models and cutouts in FreeCAD.

> [!IMPORTANT]
> Always verify dimensions with physical calipers if possible, as manufacturer revisions may vary.

## 1. Raspberry Pi 4 Model B
- **PCB Dimensions:** 85.0 mm x 56.0 mm (nominal rectangle; actual outline has **rounded corners**).
- **PCB corner radius:** 3.0 mm (per [mechanical drawing](https://datasheets.raspberrypi.com/rpi4/raspberry-pi-4-mechanical-drawing.pdf)).
- **Mounting Holes:**
  - Diameter: 2.75 mm (Standard for M2.5 screws)
  - Horizontal Spacing: 58.0 mm (center-to-center between columns)
  - Vertical Spacing: 49.0 mm (center-to-center between rows)
  - **Edge insets (hole center to nearest PCB edge), per [Raspberry Pi 4 mechanical drawing](https://datasheets.raspberrypi.com/rpi4/raspberry-pi-4-mechanical-drawing.pdf):**
    - **Along the 56 mm sides:** **3.5 mm** (bottom row to bottom edge, top row to top edge).
    - **Along the 85 mm sides (asymmetric):** **3.5 mm** from one long edge to the **near** hole column, and **23.5 mm** from the **opposite** long edge to the **other** column — **not** 13.5 mm on both sides. Check the PDF against your board (e.g. USB/Ethernet side) so your CAD “left/right” matches reality.
- **Max Height:** ~21.0 mm

## 2. HMTECH 7" Display (HTC6070V P01)
- **External Width:** ~165.0 mm
- **External Height:** ~104.0 mm
- **Depth (Thickness):** ~10.0 mm
- **Active Area:** Standard 7" 16:9 ratio.
- **Mounting:** Usually via a custom bezel or friction fit.

## 3. iUniker Pi Fan (4010)
- **Dimensions:** 40.0 mm x 40.0 mm
- **Thickness:** 10.0 mm
- **Mounting Hole Centers:** 32.0 mm x 32.0 mm spacing (standard for 40mm fans).
- **Screw Diameter:** 3.0 mm - 3.5 mm (M3).

## 4. Arcade Controls (Sanwa JLF Style)
### Joystick (JLF-TP-8YT)
- **Mounting Plate:** 95.0 mm x 53.0 mm
- **Mounting Holes:** 85.0 mm (Horizontal) x 40.0 mm (Vertical)
- **Required Depth:** ~40.0 mm below panel.

### Buttons
- **Main Buttons (30mm):**
  - Hole Diameter: 30.0 mm
  - Body Depth: ~35.0 mm
  - Bezel Diameter: ~33.0 mm
- **Auxiliary Buttons (24mm) (Start/Select):**
  - Hole Diameter: 24.0 mm
  - Body Depth: ~30.0 mm
  - Bezel Diameter: ~27.0 mm

## 5. USB Panel Mount Port
### [RECOMMENDED] Option A: All-in-One Extension Cable
- **Type:** USB-A Female to USB-A Male (approx. 30cm / 1ft length).
- **Mounting Holes:** 30.0 mm pitch (center-to-center).
- **Screw Type:** M3.
- **Why:** Plugs directly into your Pi 4; no extra internal cables needed. Matches the "Adafruit-style" standard.

### Option B: Chassis Coupler / Bulkhead Connector
- **Type:** Female-to-Female Coupler (like the XIWAI pack).
- **Mounting Holes:** Usually 28.0 mm pitch (center-to-center).
- **Why:** Very compact, but requires an additional USB-A to USB-A cable inside the case.
