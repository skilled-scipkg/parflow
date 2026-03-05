---
name: parflow-analysis-and-output
description: This skill should be used when users ask about output inspection, field comparison, diagnostics, or post-processing in ParFlow runs.
---

# parflow: Analysis and Output

## High-Signal Playbook

### Route conditions
- Use this skill for output formats, field-level checks, post-processing, and tolerance-based comparisons.
- Route to `parflow-simulation-workflows` for run/restart orchestration.
- Route to `parflow-inputs-and-modeling` if failures are caused by key/physics setup.

### Triage questions
- Which outputs are required (`press`, `satur`, `vel*`, CLM, NetCDF, PFB)?
- Are you comparing against `test/correct_output` or `examples/correct_output` baselines?
- Do you need Python (`parflow.tools.io`, `compare`, `hydrology`) or TCL tooling?
- Is the issue file generation, file content mismatch, or post-processing interpretation?

### Canonical workflow
1. Run a known baseline script unchanged.
2. Confirm expected output files exist with correct timestep cadence.
3. Compare a small representative subset first (for example `perm_x`, one `press`, one `satur`).
4. Use tolerance-aware comparison (`pf_test_file` / `pftestFileWithAbs`) for floating-point outputs.
5. Escalate to source-level read/write routines only when mismatch origin is unclear.

### Minimal working example
```shell
# Python regression with built-in output checks
python3 test/python/default_richards.py -p 1 -q 1 -r 1
```

### Pitfalls and fixes
- Exact byte comparisons often fail for valid floating-point differences; use significant-digit checks.
- Mixed output formats (`PFB`, `NetCDF`, CLM variables) require matching readers and dimensions.
- Distributed output handling requires consistent dist/undist assumptions before comparison.
- Output mismatch at early timesteps usually indicates setup drift, not post-processing bugs.

### Convergence and validation checks
- `.out.log`, `.out.txt`, and for Richards `.out.kinsol.log` exist and are internally consistent.
- Baseline comparison utilities report pass on representative variables/timesteps.
- Post-processed metrics (water table, storage, overland flow) are physically plausible and stable.

## Scope
- Handle output interpretation, comparison, and post-processing workflows.
- Prefer minimal reproducible checks before broad post-processing.

## Primary documentation references
- `docs/user_manual/files.rst`
- `docs/user_manual/pftools.rst`
- `docs/user_manual/python/tutorials/pfb.rst`
- `docs/user_manual/python/tutorials/hydrology.rst`
- `docs/user_manual/python/tutorials/data_accessor.rst`
- `test/python/default_richards.py`
- `test/python/LW_var_dz.py`
- `test/correct_output/LW_var_dz.out.log`
- `test/correct_output/LW_var_dz.out.kinsol.log`
- `test/correct_output/LW_var_dz.out.txt`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md`.
- If ambiguity remains, inspect `references/source_map.md` for function-level entry points.

## Source entry points for unresolved issues
- `pfsimulator/parflow_lib/read_parflow_binary.c`
- `pfsimulator/parflow_lib/read_parflow_netcdf.c`
- `pfsimulator/parflow_lib/write_clm_netcdf.c`
- `pfsimulator/parflow_lib/solver_richards.c`
- `pftools/python/parflow/tools/io.py`
- `pftools/python/parflow/tools/hydrology.py`
- `pftools/python/parflow/tools/compare.py`
- `test/tcl/pftest.tcl`
