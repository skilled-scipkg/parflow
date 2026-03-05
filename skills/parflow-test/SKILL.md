---
name: parflow-test
description: This skill should be used when users ask about regression tests, test failures, tolerance mismatches, or test automation in ParFlow.
---

# parflow: Test

## High-Signal Playbook

### Route conditions
- Use this skill for reproducing and debugging test failures in TCL/Python/parflow-tools test suites.
- Route to `parflow-build-and-install` for compile/configure failures before tests run.
- Route to `parflow-analysis-and-output` for deep output interpretation after mismatch is identified.

### Triage questions
- Which test path failed (`test/tcl`, `test/python`, `pftools/test`, `performance_tests`)?
- Is failure from missing outputs, tolerance mismatch, or runtime crash?
- Are you running serial (`P=Q=R=1`) or parallel topology?
- Is the failure reproducible in a single focused test script?

### Canonical workflow
1. Reproduce with one baseline script first.
2. Capture first failing comparison message and exact file/timestep.
3. Compare only the failing field against `correct_output` before broad reruns.
4. If still unclear, inspect comparison helper implementations and relevant solver output code.
5. Promote fix only after baseline tests pass again.

### Minimal working example
```shell
# TCL regression script with built-in comparisons
cd test/tcl
tclsh default_single.tcl 1 1 1

# Python regression script with built-in comparisons
cd ../python
python3 default_single.py -p 1 -q 1 -r 1
```

### Pitfalls and fixes
- Running from the wrong working directory causes `correct_output` path mismatches.
- Comparing distributed and undistributed files without normalization yields false failures.
- Changing multiple model keys at once obscures the root cause of regressions.
- Tolerance values may need absolute thresholds for near-zero velocity fields.

### Convergence and validation checks
- Regression script exits with `PASSED` and no comparison failures.
- Failing field/timestep is isolated and reproducible.
- Updated run retains expected outputs (`press`, `satur`, `vel*`, `perm_*`) under baseline settings.

## Scope
- Handle regression test execution, failure isolation, and comparator behavior.
- Keep test-debug cycles short and reproducible.

## Primary documentation references
- `test/CMakeLists.txt`
- `test/tcl/Makefile`
- `test/tcl/pftest.tcl`
- `test/python/README.md`
- `test/python/Makefile`
- `test/tcl/default_single.tcl`
- `test/python/default_single.py`
- `pftools/test/CMakeLists.txt`
- `performance_tests/inactive_active_time/Makefile`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md`.
- If ambiguity remains, inspect `references/source_map.md` for comparator and solver entry points.

## Source entry points for unresolved issues
- `test/tcl/pftest.tcl`
- `pftools/python/parflow/tools/compare.py`
- `pftools/python/parflow/tools/core.py`
- `pftools/compute_domain.c`
- `pftools/water_balance.c`
- `pftools/velocity.c`
- `pfsimulator/parflow_lib/solver_richards.c`
- `pfsimulator/parflow_lib/read_parflow_binary.c`
