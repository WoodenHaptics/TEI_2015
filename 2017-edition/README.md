# WoodenHaptics — 2017 Edition (notes & version history after 2015)

**Status: never formally released.** The original public release is the *Version 1.0 — TEI 2015 Edition* (Maxon RE40 motors). During 2016–2017 the kit was revised toward smaller motors and a few other improvements, but the changes were never compiled into a packaged release. This folder is a retroactive attempt to gather what exists so a proper "2017 Edition" can be assembled.

Dates below were verified from the embedded file metadata (Adobe XMP `CreateDate`/`ModifyDate`), the two bills of materials, and the 17 Jan 2017 mailing-list announcement (quoted below). Items marked *(recollection)* are from memory and should be double-checked before release.

---

## Timeline

| When | What | Source |
|---|---|---|
| Jan–Jun 2015 | **Version 1.0 (TEI 2015 Edition).** SolidWorks CAD (`Mechanics/`), DXF export (`lasercut_drawings/dxf/`), Illustrator laser files, BOM v1.0. Motor: **Maxon RE40 (Ø40 mm, 148877)**. | repo, `lasercut_drawings/README.md` (Jan 5 2015), BOM v1.0 |
| 2015-06 / 2015-10 | Illustrator laser sheets prepared from the DXFs on cutlasercut.com templates and verified for cutting. `body_a` last tweaked Oct 2015. | XMP dates, `illustrator/README.md` (Jun 2 2016) |
| **2016-10-07** | Laser-cut order: the four `Birch_Plywood_6mm_600mmx600mm_*_updated.ai` sheets **plus a separate `kirimoto-inkskape-body-c-a4.svg`** (an Inkscape A4 sheet for an experimental new *body c* / arm). *(order record)* | order info |
| **2017-01-17** | Mailing-list announcement of the updated kit (full text below): red ball handle, **smaller 30 mm motors (Maxon RE30)**, 19.5 V supply (laptop chargers), beta USB, new *body c* on Onshape, PCB v0.4, assembly videos. | email |
| **2017-05-09** | New arm brought into Illustrator: `new_body_c.ai` (exported via a **Mac**) and the combined `…body_b_and_c_updated_2017.ai/.pdf` (the lighter arm — larger triangular lightening cut-outs). | XMP dates |
| **2017-05-11** | Re-nested onto 500 × 450 mm sheets: `500x450_6mm_4_och_en_halv_skivor.ai` (+ `_uppdaterad.pdf`). | XMP dates |
| **2017-05-15** | **`Birch_Plywood_6mm_A2_four_sheets.pdf`** — final re-nest onto four A2 sheets; this is the file that was **actually ordered / cut** on this date. BOM **v1.1 "with 30 mm motors and USB"**. | XMP dates, order info, BOM v1.1 |

---

## What changed vs. the 2015 (RE40) edition

### Mechanics — RE40 → RE30
The structural design did **not** change. Verified findings:

- **Motor mount is shared.** The motor bolts to the wood with **M3 screws on a Ø22 bolt circle**, and **both RE40 and RE30 use that pattern** — so no plate needed to be re-drawn. (BOM v1.0 already lists 40 / 30 / 25 mm Maxon motors as interchangeable alternatives with the same `M3x10` screws.) The `base` / `body_a` / `body_b` laser geometry is unchanged 2015 geometry.
- **Only the arm (`body c`) was re-drawn**, to lighten it (lower inertia for the smaller motors) — `new_body_c.ai` / `…body_b_and_c_updated_2017`.

The practical RE40 → RE30 conversion is therefore just:

1. **Coupler:** `CPL25-6-10` → **`CPL12-4-5`** (RE30 has a 5 mm shaft; the new coupler is also shorter).
2. **Remove one wooden lamination** from the motor-holder stack to take up the shorter coupler/motor length. *(recollection — the motor holder is a laminated plate stack; using one layer fewer of an existing part, no new geometry.)*
3. **Motor:** `148877` (40 mm) → **`310009`** (30 mm), with 500 CPR encoder.
4. Use the **lightened arm** (`body c`).

### Electronics / system (from the 2017 announcement)
- **Red ball handle** (kitchen-drawer knob) for clearer affordance.
- **19.5 V** supply so a standard laptop charger works (e.g. Innergie PowerGear 90) — replaces the 48 V supply.
- **USB support** (beta at the time).
- **PCB v0.4.**
- Code on the `experimental` branch of the GitHub repo; assembly videos at <http://woodenhaptics.org/build.html>.

---

## Contents of this folder

```
2017-edition/
├── README.md                     ← this file
├── bom/
│   └── WoodenHaptics Bill of Materials - 2017 Edition (Ver 1.1 with 30mm motors and USB).csv
└── lasercut/
    ├── Birch_Plywood_6mm_A2_four_sheets.pdf                         ← THE production cut file (A2 ×4, 15 May 2017)
    ├── new_body_c.ai                                                ← lightened arm, exported from Onshape (Mac)
    ├── Birch Plywood_6mm_600mmx600mm_body_b_and_c_updated_2017.ai   ← combined new-arm sheet (600×600 master)
    ├── Birch Plywood_6mm_600mmx600mm_body_b_and_c_updated_2017.pdf
    ├── 500x450_6mm_4_och_en_halv_skivor.ai / _uppdaterad.pdf        ← intermediate 500×450 re-nest (11 May 2017)
    ├── Birch Plywood_6mm_600mmx600mm_base_1_of_2_updated.pdf        ← unchanged 2015 geometry (RE40 = RE30)
    ├── Birch Plywood_6mm_600mmx600mm_base_2_of_2_updated.pdf        ← unchanged 2015 geometry
    └── Birch Plywood_6mm_600mmx600mm_body_a_updated.pdf             ← unchanged 2015 geometry
```

All sheets: **6 mm birch plywood**, red (RGB 255,0,0) = cut-through, black = engrave ~1.5–2.5 mm (same conventions as `Mechanics/lasercut_drawings/`).

**If you only cut one thing, cut `Birch_Plywood_6mm_A2_four_sheets.pdf`** — it is the complete, as-built four-sheet layout (incl. the lightened arm), sized for an A2 (594 × 420 mm) laser bed.

---

## Provenance & gaps (important before a release)

- **The parametric CAD for the new arm is NOT in this repo.** It was authored in **Onshape**:
  <https://cad.onshape.com/documents/3a7c6140b3b524fe2e399f10/w/c1ea1269244ce72f85bc9402/e/6f0b243d8c0c198195d363ae>
  Locally the arm survives only as **flat laser vectors** (`new_body_c.ai`, and inside the A2 PDF). The original Inkscape source `kirimoto-inkskape-body-c-a4.svg` could not be found on any local disk.
- The RE40 parametric CAD is complete in `../Mechanics/` (SolidWorks). To make the RE30 arm editable again, either re-export from Onshape, or trace/convert `new_body_c.ai` → DXF/SVG and re-integrate.
- These 2017 laser files previously lived only in a loose `Woody-May-2017` working folder, not under version control — copied here so they are not lost.

## TODO toward a packaged 2017 Edition
- [ ] Recover or re-create editable arm CAD (Onshape export, or convert `new_body_c.ai`).
- [ ] Confirm the "remove one lamination" step and document the motor-holder stack-up for RE30 (drawing or photo).
- [ ] Add the RE30 coupler (`CPL12-4-5`) and red ball handle to a parts drawing / BOM cross-check.
- [ ] Capture the electronics changes (PCB v0.4, 19.5 V, USB) from the `experimental` branch into this edition.
- [ ] Decide whether this supersedes or sits alongside the TEI 2015 Edition, and tag a release.

---

### Appendix — 17 Jan 2017 mailing-list announcement (verbatim)

> I have been working on updating woodenhaptics kit in an attempt to make it more complete and slightly reduce cost. I propose the following changes:
> * Red ball handle (kitchen drawer knob) improves affordance i.e. makes it clear where to hold
> * Smaller motors (30 mm, Maxon RE30) are cheaper and lighter which lowers inertia.
> * Switching to 19.5V power supply so we can use standard laptop chargers, I have successfully used the Innergie Powergear 90
> * USB support working (but still beta)
>
> CAD models for new body c (arm) can be found on onshape (the collaborative, free-to-use cad software I use now)
> https://cad.onshape.com/documents/3a7c6140b3b524fe2e399f10/w/c1ea1269244ce72f85bc9402/e/6f0b243d8c0c198195d363ae
>
> Code for mbed and computer side is shared on the experimental-branch of the github. […] Updated PCB:s are also there (version 0.4).
>
> I have also made some assembly instruction videos covering the whole process […] http://woodenhaptics.org/build.html
>
> Jonas
