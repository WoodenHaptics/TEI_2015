# Onshape import bundle + verification

Artifacts for importing the SolidWorks `Mechanics/` model into
[Onshape](https://cad.onshape.com), and screenshots confirming it worked.

## `woodenhaptics.zip`
A **flat** archive of every SolidWorks part/assembly in `Mechanics/`
(`.SLDPRT` / `.SLDASM` / `.SLDDRW`), **excluding** `lasercut_drawings/`.

Onshape's SolidWorks importer requires that the zip contain **no folders** and
that its **filename matches the root assembly** — here `woodenhaptics.SLDASM`.
Regenerate from `Mechanics/` with:

```sh
cd Mechanics
find . -path ./lasercut_drawings -prune -o \
  -type f \( -name '*.SLDPRT' -o -name '*.SLDASM' -o -name '*.SLDDRW' \) -print |
  while read f; do zip -jq ../woodenhaptics.zip "$f"; done
```

(108 files; the part/assembly basenames are unique, so flattening is collision-free.)

## `screenshots/`
The bundle imported cleanly into Onshape. Each shot highlights one subassembly
(yellow) — this is also the rigid-body breakdown used by the FreeCAD migration
(`../../freecad-migration-plan.md`):

| File | Shows |
|---|---|
| `tei2015-woody.png` | full assembly (import tree on the left) |
| `tei2015-woody-base.png` | `base` — fixed to world (frame N) |
| `tei2015-woody-a.png` | `body_a` — θa, rotates on base |
| `tei2015-woody-b.png` | `body_b` — θb |
| `tei2015-woody-c.png` | `body_c` — driven by the four-bar |
| `tei2015-woody-c-prim.png` | `body_c_prim` — θc, the parallelogram link |
