---
name: parflow-inputs-and-modeling
description: This skill should be used when users ask about inputs and modeling in parflow; it prioritizes documentation references and then source inspection only for unresolved details.
---

# parflow: Inputs and Modeling

## High-Signal Playbook

### Route conditions
- Use this skill for run definition: computational grid, geometry, permeability/porosity/storage, BCs, phases, and solver-related key structures.
- Route to `parflow-simulation-workflows` for operational restart/checkpoint/output behavior.
- Route to `parflow-api-and-scripting` for Python/TCL syntax and automation mechanics.

### Triage questions
- Is the domain defined by `Box`, `IndicatorField`, `SolidFile`, or mixed geometry inputs?
- Which solver mode is targeted (`Impes`, `Richards`, overland, CLM-coupled)?
- Are properties constant or file-driven (`PFBFile` / `NCFile`)?
- Which geometries must receive parameter values (`Geom.Perm.Names`, `Geom.Porosity.GeomNames`)?
- Which boundary condition types are required per patch and cycle?
- Are restart/initial-condition files part of the setup?

### Canonical workflow
1. Set `Process.Topology` and `ComputationalGrid`.
2. Declare `GeomInput.Names` and define domain geometry + patches.
3. Define sub-geometries/material regions (box or indicator-based).
4. Assign `Perm`, `Porosity`, and `SpecificStorage` by geometry names.
5. Define phases, relative permeability/saturation models, and gravity.
6. Configure cycles and patch BCs.
7. Set timing, timestep, IC pressure, and solver tolerances.
8. Validate against at least one known test script before large modifications.

### Minimal working example
```tcl
pfset Process.Topology.P 1
pfset Process.Topology.Q 1
pfset Process.Topology.R 1
pfset ComputationalGrid.DX 1.0
pfset ComputationalGrid.DY 1.0
pfset ComputationalGrid.DZ 1.0
pfset ComputationalGrid.NX 10
pfset ComputationalGrid.NY 10
pfset ComputationalGrid.NZ 5
pfset GeomInput.Names "domain_input"
pfset GeomInput.domain_input.InputType Box
pfset GeomInput.domain_input.GeomName domain
pfset Geom.domain.Patches "left right front back bottom top"
pfset Geom.Perm.Names "domain"
pfset Geom.domain.Perm.Type Constant
pfset Geom.domain.Perm.Value 1.0
pfset Geom.Porosity.GeomNames "domain"
pfset Geom.domain.Porosity.Type Constant
pfset Geom.domain.Porosity.Value 0.25
pfset Domain.GeomName domain
```

### Pitfalls and fixes
- Geometry extents must match computational grid extents (`Upper-Lower == D* N`) for each axis.
- Every geometry listed in `Geom.Perm.Names` or `Geom.Porosity.GeomNames` needs a complete assignment.
- For TurnBands/heterogeneous workflows, `Sigma` is standard deviation (not variance).
- `BCPressure.PatchNames` must align with declared domain patches exactly.
- Indicator/PFB files must match domain dimensions and indexing assumptions.
- In Python scripts, declare dynamic name lists before setting child keys.

### Convergence and validation checks
- Output fields for core properties (`perm_*`, `porosity`, `specific_storage`) are generated and physically plausible.
- For Richards runs, `.out.kinsol.log` shows stable nonlinear progress.
- Sensitivity checks on `TimeStep.Value`, grid resolution, and nonlinear/linear tolerances are bounded.
- Initial pressure and BCs produce expected early-time behavior (no immediate divergence).

## Scope
- Handle key input structures and modeling parameterization workflows.
- Keep guidance tied to user-manual keys and test-proven script patterns.

## Primary documentation references
- `docs/user_manual/pfsystem.rst`
- `docs/user_manual/models.rst`
- `docs/user_manual/keys.rst`
- `docs/user_manual/files.rst`
- `docs/user_manual/PfkeysExample/permeability/key1.rst`
- `docs/user_manual/PfkeysExample/permeability/key2.rst`
- `docs/user_manual/PfkeysExample/permeability/key3.rst`
- `docs/user_manual/PfkeysExample/porosity/key1.rst`
- `docs/user_manual/PfkeysExample/porosity/key2.rst`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md`.
- Use `test/input` artifacts and baseline scripts for concrete value patterns.
- If ambiguity remains, inspect `references/source_map.md` and the entry points below.

## Source entry points for unresolved issues
- `pfsimulator/parflow_lib/input_database.c`
- `pfsimulator/parflow_lib/input_checks.c`
- `pfsimulator/parflow_lib/usergrid_input.c`
- `pfsimulator/parflow_lib/geometry.c`
- `pfsimulator/parflow_lib/grgeometry.c`
- `pfsimulator/parflow_lib/time_cycle_data.c`
- `pfsimulator/parflow_lib/permeability_face.c`
- `pfsimulator/parflow_lib/input_porosity.c`
- `pf-keys/definitions`
- `pf-keys/generators/simput/simput_model.py`
