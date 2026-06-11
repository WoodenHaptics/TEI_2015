# WoodenHaptics — 2026 Consolidation Plan

A handoff/planning doc for gathering everything WoodenHaptics into a single,
canonical 2026 repository. Written so the work can be picked up from any
computer — **everything referenced here is committed and pushed; the local
working copy can be dropped.**

Status: **draft / basis for discussion.** The big open decision (which GitHub
home) is deliberately left open — see "Open decision" below.

---

## Why consolidate
The project's material is currently scattered across several repos and editions
with overlapping, partly-stale content. The paper explicitly invites the
community to build on the kit; a single front-door repo, framed from a 2026
perspective, makes that realistic. The goal is **one repo** that holds the
2015 reference design, the never-released 2017 revision, the electronics/
software, and the forward-looking FreeCAD model — clearly separated by edition,
with a top-level README that orients a newcomer.

---

## Current GitHub landscape (verified 2026-05-19)

| Repo | State | Holds | Verdict |
|---|---|---|---|
| **`WoodenHaptics/TEI_2015`** (this repo) | active, pushed today | SolidWorks `Mechanics/`, lasercut DXF/AI, BOM v1.0, the TEI 2015 paper PDF, `2017-edition/`, `freecad-migration-plan.md`, Electronics/Software/Docs | richest mechanical source; **best basis** |
| **`WoodenHaptics/woody-experimental`** | 2019, "do not use" | PCB **v0.4** (`woodenHaptics_v_0_4.brd/.sch`), `mbed-code`, `chai3d-3.0.0-woody`, `daq-direct`, `websim`, `woodenhaptics_2016ed.json`, `woodenhaptics_aluhaptics_2017-03-16.json` | **valuable** — this is the 2016/2017 electronics + code the 2017 README points to |
| **`forsslund/WoodenHaptics`** | **fork** of MobileLifeCentre, pushed **Dec 2014** | `woodenHaptics_v_0_1`, `Sensoray_DAQ`, `DAQ_Extension_Board_December`, `woddenHaptics_Egle_files` | historical v0.1 only; it's a stale fork → poor base |
| **`MobileLifeCentre/WoodenHaptics`** | upstream original, Jan 2015 | the true origin of the fork above | historical root |

**Implication:** the substance lives in `TEI_2015` (mechanics + 2017 edition)
and `woody-experimental` (electronics + code). The personal/MobileLife repos are
mostly historical v0.1 material.

---

## Open decision — which GitHub home

Three options, with trade-offs:

1. **New repo `WoodenHaptics/woodenhaptics` (org, lowercase) — recommended.**
   Clean canonical name, lives in the org so multiple maintainers and the
   `woodenhaptics.org` identity align, and no awkward fork relationship. Pull
   `TEI_2015` and `woody-experimental` content in under `editions/` and
   `electronics/`+`software/`; then **archive** the old repos with a README
   pointer. Most work, cleanest result.

2. **Continue from `forsslund/WoodenHaptics`.** It already exists and is
   personally owned, but it's a **2014 fork of MobileLifeCentre** containing only
   v0.1-era files — the fork lineage and stale content make it a weak base. Would
   need a heavy rewrite anyway. Not recommended unless you specifically want it
   under your personal account rather than the org.

3. **Keep building inside `WoodenHaptics/TEI_2015` and rename it.** Lowest
   effort — it's already the richest repo. But the name `TEI_2015` is tied to the
   paper/citation; renaming it muddies that link, and a rename leaves redirect
   baggage. Better to keep `TEI_2015` as the frozen, citable 2015 artifact.

**Recommendation:** option 1. Keep `TEI_2015` frozen as the paper's citable
snapshot; make a fresh org repo the living home. Decide org-vs-personal
(`WoodenHaptics/` vs `forsslund/`) as a governance question — the org is the
better long-term community home, but that's yours to call.

---

## Proposed structure for the new repo

```
woodenhaptics/
├── README.md                 ← 2026 framing: what it is, editions, how to start, links to paper & woodenhaptics.org
├── LICENSE.md                ← carry over (open-source/open-hardware)
├── paper/
│   └── woodenhaptics-tei-2015-paper.pdf
├── editions/
│   ├── tei-2015/             ← from TEI_2015: Mechanics/ (SolidWorks), lasercut DXF/AI, BOM v1.0
│   │   └── README.md         ← "the citable reference design; RE40 motors"
│   └── 2017/                 ← from TEI_2015/2017-edition: RE30 lasercut, BOM v1.1, the detailed timeline README
├── cad-freecad/              ← output of freecad-migration-plan.md (articulated open-source model)
├── electronics/              ← from woody-experimental: PCB v0.4 (.brd/.sch), DAQ boards
├── software/                 ← from woody-experimental: mbed-code, chai3d-3.0.0-woody, daq-direct, websim, config JSONs
├── docs/                     ← assembly notes, build videos pointer (woodenhaptics.org/build.html)
└── archive/                  ← optional: v0.1-era material from forsslund/MobileLifeCentre if worth preserving
```

Principles:
- **Editions are folders, never branches** (additive snapshots, never merged).
- One top-level README is the front door; each edition keeps its own README
  (the 2017 one is already excellent and self-documenting).
- Bring CAD source where it exists; where it doesn't (the 2017 arm, which is
  Onshape-only — see `2017-edition/README.md`), keep the link + flat vectors and
  flag the gap.

---

## Migration checklist

- [ ] **Decide the GitHub home** (open decision above).
- [ ] Create the new repo + `README.md` skeleton with the structure above.
- [ ] Import `TEI_2015` mechanical content → `editions/tei-2015/` (preserve history
      via `git subtree`/`filter-repo` if history matters, else a clean copy).
- [ ] Move `2017-edition/` → `editions/2017/`.
- [ ] Import `woody-experimental` electronics → `electronics/`, code → `software/`.
- [ ] Run the FreeCAD migration (`freecad-migration-plan.md`) → `cad-freecad/`.
- [ ] Triage `forsslund/WoodenHaptics` + `MobileLifeCentre` v0.1 → `archive/` or drop.
- [ ] Write the 2026 front-door README (framing, editions table, getting-started,
      links to paper + woodenhaptics.org).
- [ ] **Archive** `TEI_2015` and `woody-experimental` on GitHub with a README
      pointer to the new repo (keep them — `TEI_2015` is the paper's citation target).
- [ ] Cross-check BOMs (RE40 v1.0 vs RE30 v1.1) and reconcile the open TODOs in
      `2017-edition/README.md` (editable arm CAD, motor-holder lamination, coupler,
      handle, electronics changes).

---

## Local working copy — what's here and what's safe to drop

After the commits accompanying this plan, **everything important is in git and
pushed.** This local checkout can be deleted.

- **Committed & pushed:** all of `2017-edition/`, `freecad-migration-plan.md`,
  the paper PDF, this plan, and the existing repo contents.
- **Local-only, regenerable — NOT committed (safe to discard):**
  - `woodenhaptics.zip` — flat Onshape-import bundle; regenerate from `Mechanics/`
    (flat zip of all `.SLD*`, named to match root assembly `woodenhaptics.SLDASM`).
  - `Mechanics/tei2015-woody-*.png` — render exports; not part of the deliverable.
  - Duplicate root CSVs were removed (byte-identical copies already live in the
    repo: TEI-2015 BOM at repo root, 2017 BOM under `2017-edition/bom/`).
- **External, not in any repo — don't lose:** the 2017 arm parametric CAD lives
  only on Onshape (link in `2017-edition/README.md`); the original Inkscape source
  `kirimoto-inkskape-body-c-a4.svg` is already missing.

---

## Related docs
- `freecad-migration-plan.md` — the articulated open-source CAD effort that feeds
  `cad-freecad/` in the new repo.
- `2017-edition/README.md` — detailed, source-verified timeline and provenance of
  the 2017 revision, plus its own TODO toward a packaged release.
