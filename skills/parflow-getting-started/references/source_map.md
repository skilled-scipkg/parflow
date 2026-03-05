# parflow source map: Getting Started

Generated from source roots:
- `pf-keys`
- `pfnuopc`
- `pfsimulator`
- `pftools`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Fast source navigation
- `rg -n "Run\.|pf_test_file|pftestFile|default_single" test pftools/python`
- `rg -n "SolverImpes|SolverRichards|SelectTimeStep" pfsimulator/parflow_lib`

## Function-level entry points
- `pfsimulator/parflow_exe/main.c` | symbols: `main`
- `pfsimulator/parflow_lib/solver.c` | symbols: `Solve`
- `pfsimulator/parflow_lib/solver_impes.c` | symbols: `SolverImpes`
- `pfsimulator/parflow_lib/solver_richards.c` | symbols: `SolverRichards`
- `pfsimulator/parflow_lib/select_time_step.c` | symbols: `SelectTimeStep`
- `pftools/python/parflow/tools/core.py` | symbols: `Run.run`, `Run.dist`, `Run.write`
- `pftools/python/parflow/tools/compare.py` | symbols: `pf_test_file`, `pf_test_file_with_abs`
- `test/tcl/pftest.tcl` | symbols: `pftestFile`, `pftestFileWithAbs`
