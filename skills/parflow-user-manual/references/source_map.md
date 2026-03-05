# parflow source map: User Manual

Generated from source roots:
- `pf-keys`
- `pfnuopc`
- `pfsimulator`
- `pftools`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Fast source navigation
- `rg -n "Run\.|pfset|validate|SolverRichards|SolverImpes|ReadPFBinary" pftools/python pfsimulator/parflow_lib`
- `rg -n "ComputeDomain|CompCellVel|ComputeSurfaceStorage" pftools`

## Function-level entry points
- `pfsimulator/parflow_lib/input_database.c` | symbols: `IDB_GetString`, `IDB_GetDouble`, `NA_NameToIndex`
- `pfsimulator/parflow_lib/solver_impes.c` | symbols: `SolverImpes`
- `pfsimulator/parflow_lib/solver_richards.c` | symbols: `SolverRichards`
- `pfsimulator/parflow_lib/problem_bc_pressure.c` | symbols: `BCPressureInitInstanceXtra`
- `pfsimulator/parflow_lib/read_parflow_binary.c` | symbols: `ReadPFBinary`
- `pftools/python/parflow/tools/core.py` | symbols: `Run.write`, `Run.run`, `Run.dist`
- `pftools/python/parflow/tools/io.py` | symbols: `read_pfb`, `write_pfb`, `read_pfidb`
- `pftools/compute_domain.c` | symbols: `ComputeDomain`
- `pftools/water_balance.c` | symbols: `ComputeSurfaceStorage`, `ComputeSubsurfaceStorage`
- `pftools/velocity.c` | symbols: `CompCellVel`, `CompVMag`
