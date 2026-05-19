# WoodenHaptics → FreeCAD Migration Plan

## Goal
Publish an articulated FreeCAD model of the reference design so the community can open, inspect, and modify the device without proprietary software. End-effector point P can be moved by dragging; the RRR linkage and the C/C' four-bar respond correctly.

## Scope
**In:** Geometry of all parts, subassembly grouping, three revolute DOFs (θa, θb, θc), parallelogram closure, gravity-correct orientation.
**Out:** Motor→body cable ratios, cable rope geometry as a kinematic element, lasercut drawings, electronics box, software/firmware, FEA.

## Subassembly mapping
Each Mechanics/ subfolder becomes one FreeCAD document. Parts inside are rigidly fixed (no internal joints — treat each subassembly as one solid body).

| Folder | FreeCAD file | Role |
|---|---|---|
| `base/` | `base.FCStd` | Fixed to world (frame N) |
| `body_a/` | `body_a.FCStd` | Rotates θa about vertical axis on base |
| `body_b/` | `body_b.FCStd` | Rotates θb about horizontal axis on body_a |
| `body_c_prim/` | `body_c_prim.FCStd` | Rotates θc about horizontal axis on body_a |
| `body_c/` | `body_c.FCStd` | Driven via four-bar (parallel to body_b) |
| `other/` (RE40) | reuse as needed | Visual only, place inside relevant subassembly |
| top level | `woodenhaptics.FCStd` | Links the five subassemblies + joints |

## Migration steps

**1. Export from Onshape (one-time)**
Once the Onshape import lands (using the zip we built), export each subassembly separately as STEP AP242:
- `base.step`, `body_a.step`, `body_b.step`, `body_c.step`, `body_c_prim.step`
- Plus `woodenhaptics_full.step` as a sanity reference for poses.

**2. Build subassembly documents**
For each STEP:
- Open in FreeCAD → save as `.FCStd`
- Verify it imports as a single Compound or as a set of solids in their assembled positions
- If multiple solids: group under one `App::Part` container so the whole subassembly behaves as one rigid body in the top-level assembly
- No internal joints needed

**3. Build top-level assembly (`woodenhaptics.FCStd`)**
- New document, Assembly workbench
- Insert each subassembly as a linked document (File → Link)
- Ground `base` (fixed joint to origin)
- Add joints (see below)

**4. Define joints**

| Joint | Type | Between | Axis |
|---|---|---|---|
| J1 (θa) | Revolute | base ↔ body_a | Vertical (Z in N frame) through the body_a turntable center |
| J2 (θb) | Revolute | body_a ↔ body_b | Horizontal, through body_b's shaft bearings on body_a |
| J3 (θc) | Revolute | body_a ↔ body_c_prim | Horizontal, parallel to J2, through body_c_prim's shaft |
| J4 | Revolute | body_b ↔ body_c | Horizontal, at the far end of body_b |
| J5 | Revolute | body_c_prim ↔ body_c | Horizontal, at the far end of body_c_prim (closes the four-bar) |

J4 + J5 close the loop. The OndselSolver should resolve this as a single DOF along θc once θa and θb are fixed. If it struggles to converge, pin θc as the driver on J3 and let J5 float (or vice versa) — pick whichever solves cleanly.

**5. Verify articulation**
- Drag body_a around vertical axis → whole arm sweeps (θa works)
- Drag body_b → body_c stays parallel to it as the four-bar pivots (θb works, parallelogram correct)
- Drag body_c_prim → body_c translates parallel to body_b (θc works)
- Confirm end-point P traces a workspace consistent with eq. (1) in the paper

**6. Polish for publication**
- Set materials/colors (plywood color on structural parts, dark on motors/bearings)
- Add a simple `README.md` explaining the joint structure and noting what is *not* modelled (cable ratios)
- Save with FreeCAD 1.0+ format; document the minimum FreeCAD version in README

## Deliverables
- `freecad/` directory in the repo with the six `.FCStd` files
- `freecad/README.md` covering versions, how to open, known limitations
- An exported `woodenhaptics_articulated.step` for users who want to consume it in other tools

## Risks / open questions
- **Four-bar convergence**: if OndselSolver chokes on the closed loop, fallback is to omit J5 and just animate body_c manually parallel to body_b via a single expression (`body_c.Placement = body_b.Placement` with offset). Less elegant but visually identical.
- **STEP per-subassembly vs. one big STEP**: exporting subassemblies separately preserves the grouping we want; exporting one big STEP and re-splitting in FreeCAD is more work. Go with separate exports if Onshape allows it cleanly.
- **Motor placement**: paper says motors B and C mount on body_a. If they're geometrically inside `body_a/` already in your SLDASM, no extra work. If they live in `other/`, decide which subassembly they belong to before exporting.

## Suggested order of work
1. Get the Onshape import working (already in motion)
2. Export the five subassembly STEPs
3. Build `base.FCStd` and `body_a.FCStd`, prove J1 works in a minimal two-body assembly
4. Add body_b + J2, verify
5. Add body_c_prim + J3
6. Close the loop with body_c + J4 + J5
7. Polish, write README, commit

Roughly a half-day of focused work if the STEP imports cleanly; a full day if the four-bar needs coaxing.
