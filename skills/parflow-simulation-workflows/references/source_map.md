# parflow source map: Simulation Workflows

Generated from source roots:
- `pf-keys`
- `pfnuopc`
- `pfsimulator`
- `pftools`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Fast source navigation
- `rg -n "SolverRichards|SolverImpes|SelectTimeStep|KinsolNonlinSolver|Restart" pfsimulator/parflow_lib`
- `rg -n "OverlandFlowEval|BCPressurePackageUsingOverlandFlow|WriteCLMNC" pfsimulator/parflow_lib`

## Function-level entry points
- `pfsimulator/parflow_lib/solver.c` | symbols: `Solve`
- `pfsimulator/parflow_lib/select_time_step.c` | symbols: `SelectTimeStep`
- `pfsimulator/parflow_lib/time_cycle_data.c` | symbols: `TimeCycleDataComputeIntervalNumber`, `TimeCycleDataComputeNextTransition`
- `pfsimulator/parflow_lib/solver_impes.c` | symbols: `SolverImpes`
- `pfsimulator/parflow_lib/solver_richards.c` | symbols: `SolverRichards`, `SolverRichardsInitInstanceXtra`
- `pfsimulator/parflow_lib/kinsol_nonlin_solver.c` | symbols: `KinsolNonlinSolver`
- `pfsimulator/parflow_lib/bc_pressure_package.c` | symbols: `BCPressurePackage`, `BCPressurePackageUsingOverlandFlow`
- `pfsimulator/parflow_lib/overlandflow_eval.c` | symbols: `OverlandFlowEval`
- `pfsimulator/parflow_lib/overlandflow_eval_Kin.c` | symbols: `OverlandFlowEvalKin`
- `pfsimulator/parflow_lib/overlandflow_eval_diffusive.c` | symbols: `OverlandFlowEvalDiff`
- `pfsimulator/parflow_lib/read_parflow_binary.c` | symbols: `ReadPFBinary`
- `pfsimulator/parflow_lib/read_parflow_netcdf.c` | symbols: `ReadPFNC`, `ReadNCFile`
- `pfsimulator/parflow_lib/write_clm_netcdf.c` | symbols: `WriteCLMNC`, `PutCLMDataInNC`
