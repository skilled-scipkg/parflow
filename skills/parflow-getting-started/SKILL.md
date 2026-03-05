---
name: parflow-getting-started
description: This skill should be used when users ask about getting started in parflow; it prioritizes documentation references and then source inspection only for unresolved details.
---

# parflow: Getting Started

## High-Signal Playbook

### Route conditions
- Use this skill for first successful runs, solver orientation (`Impes` vs `Richards`), and baseline script execution.
- Route to `parflow-build-and-install` for compiler/dependency configuration problems.
- Route to `parflow-inputs-and-modeling` for deep key semantics and domain/property design.

### Triage questions
- Are you running TCL scripts, Python scripts, or both?
- Is `PARFLOW_DIR` already set to a working install?
- Do you need a fully saturated (`Impes`) or variably saturated (`Richards`) baseline?
- What process topology (`P Q R`) and grid size (`NX NY NZ`) are required?
- Are you starting from `test/` baselines or authoring a new run script?

### Canonical workflow
1. Confirm install and environment (`PARFLOW_DIR`, shell/runtime setup).
2. Start from `test/tcl/default_single.tcl` or `test/python/default_single.py` unchanged.
3. Run with `P=Q=R=1` first; expand parallelism only after the baseline passes.
4. Inspect output logs (`.out.log`, `.out.txt`, and `.out.kinsol.log` for Richards).
5. Compare one or more outputs to baseline references (`test/*/correct_output`).
6. Only then adapt geometry, properties, BCs, and solver parameters.

### Minimal working example
```shell
# TCL baseline
cd test/tcl
tclsh default_single.tcl 1 1 1

# Python baseline
cd ../python
python3 default_single.py -p 1 -q 1 -r 1
```

### Pitfalls and fixes
- Missing `PARFLOW_DIR` or wrong shell environment breaks package loading and runtime tools.
- In TCL, omitting ParFlow package import (`lappend auto_path`, `package require parflow`) prevents `pfset`/`pfrun` usage.
- In Python, dynamic names must be declared before use (`GeomInput.Names`, `Cycle.Names`, etc.).
- Non-Pythonic key tokens (hyphens) require bracket access (`Patch['x-lower']...`).
- `P*Q*R` topology mismatch with execution environment causes runtime confusion and poor scaling diagnostics.

### Convergence and validation checks
- Baseline run produces expected core outputs (`press`, `perm_*`, and model-specific fields).
- Log files show solver progress without repeated convergence failure messages.
- At least one baseline file compares cleanly with the reference (`pf_test_file`/`pftestFile`).
- Domain extents are internally consistent (`DX*NX`, `DY*NY`, `DZ*NZ` versus geometry bounds).

## Scope
- Handle first-week setup, quickstarts, and orientation to the main ParFlow run flow.
- Keep responses docs-first and focused on getting a reproducible baseline run.

## Primary documentation references
- `docs/user_manual/intro.rst`
- `docs/user_manual/start.rst`
- `docs/user_manual/pfsystem.rst`
- `docs/user_manual/pftools.rst`
- `docs/user_manual/python/getting_started.rst`
- `docs/user_manual/python/run_script.rst`
- `test/tcl/default_single.tcl`
- `test/python/default_single.py`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md`.
- If ambiguity remains, inspect `references/source_map.md` and the entry points below.
- Cite exact documentation file paths in responses.

## Source entry points for unresolved issues
- `pfsimulator/parflow_exe/main.c`
- `pfsimulator/parflow_lib/solver.c`
- `pfsimulator/parflow_lib/solver_impes.c`
- `pfsimulator/parflow_lib/solver_richards.c`
- `pfsimulator/parflow_lib/select_time_step.c`
- `pftools/python/parflow/tools/core.py`
- `pftools/python/parflow/tools/compare.py`
- `test/tcl/default_single.tcl`
- `test/python/default_single.py`
- `test/tcl/pftest.tcl`
