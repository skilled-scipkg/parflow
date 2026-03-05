---
name: parflow-simulation-workflows
description: This skill should be used when users ask about simulation workflows in parflow; it prioritizes documentation references and then source inspection only for unresolved details.
---

# parflow: Simulation Workflows

## High-Signal Workflow

### Route conditions
- Use this skill for prepare-run-checkpoint-restart operations, output expectations, and baseline regression verification.
- Route to `parflow-inputs-and-modeling` for key semantics and physical parameterization choices.
- Route to `parflow-api-and-scripting` for Python/TCL syntax and automation tooling details.

### Triage questions
- Are you running TCL or Python scripts?
- Is the run fresh, resumed from checkpoint, or CLM-coupled restart?
- What output cadence is required (`TimingInfo.DumpInterval`, CLM dump interval)?
- Which baseline should results be compared against (`test/tcl`, `test/python`, `examples`)?
- Are distributed inputs/outputs (`pfdist`/`pfundist` or `Run.dist`) part of the flow?

### Canonical workflow
1. Start from a baseline script (`default_single` or `default_richards`) and run unchanged.
2. Confirm topology/grid and required input files are in place.
3. Execute run and inspect `.out.log`, `.out.txt`, and `.out.kinsol.log` (Richards).
4. Validate expected outputs (`press`, `satur`, `perm_*`, plus model-specific outputs).
5. For restart: use last complete timed dump, set `StartCount`/`StartTime`, and update IC pressure input.
6. For CLM restart: set `Solver.CLM.IstepStart` consistently with restart point.
7. Compare against test baselines using tolerance-aware checks.

### Minimal working example
```shell
# Python baseline with regression checks embedded in script
python3 test/python/default_richards.py -p 1 -q 1 -r 1

# TCL baseline
tclsh test/tcl/default_richards.tcl 1 1 1
```

### Pitfalls and fixes
- Restarting from incomplete timed-dump files leads to inconsistent state; use the last complete dump.
- Restart requires both sequence index and physical time alignment (`StartCount`, `StartTime`).
- CLM restart requires `Solver.CLM.IstepStart` update and aligned CLM driver state.
- Forgetting `pfundist` can leave output handling inconsistent on some systems.
- ParFlow dump interval and CLM dump interval are separate controls.

### Convergence and validation checks
- Nonlinear residual trajectories in `.out.kinsol.log` are stable.
- Output sequence numbers and file counts match configured timing.
- Core output fields compare to baseline references within expected tolerance.
- Velocity, pressure, and saturation fields are free of obvious nonphysical artifacts.

## Scope
- Handle operational simulation lifecycle questions from first run through restart and baseline verification.

## Primary documentation references
- `docs/user_manual/pfsystem.rst`
- `docs/user_manual/python/run_script.rst`
- `docs/user_manual/python/getting_started.rst`
- `test/tcl/default_single.tcl`
- `test/tcl/default_richards.tcl`
- `test/python/default_single.py`
- `test/python/default_richards.py`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md`.
- Use test scripts as regression baselines for expected outputs.
- If ambiguity remains, inspect `references/source_map.md` and entry points below.

## Source entry points for unresolved issues
- `pfsimulator/parflow_lib/select_time_step.c`
- `pfsimulator/parflow_lib/time_cycle_data.c`
- `pfsimulator/parflow_lib/solver_richards.c`
- `pfsimulator/parflow_lib/solver_impes.c`
- `pfsimulator/parflow_lib/solver_lb.c`
- `pfsimulator/parflow_lib/kinsol_nonlin_solver.c`
- `pfsimulator/clm/endrun.F90`
- `test/tcl/default_richards.tcl`
- `test/python/default_richards.py`
