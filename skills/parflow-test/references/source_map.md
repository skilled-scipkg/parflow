# parflow source map: Test

Generated from source roots:
- `pf-keys`
- `pfnuopc`
- `pfsimulator`
- `pftools`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Fast source navigation
- `rg -n "pftestFile|pf_test_file|sig_digits|abs_value" test pftools/python/parflow/tools`
- `rg -n "ReadPFBinary|SolverRichards|ComputeDomain|ComputeSurfaceStorage" pfsimulator/parflow_lib pftools`

## Function-level entry points
- `test/tcl/pftest.tcl` | symbols: `pftestFile`, `pftestFileWithAbs`
- `pftools/python/parflow/tools/compare.py` | symbols: `pf_test_equal`, `pf_test_file`, `pf_test_file_with_abs`
- `pftools/python/parflow/tools/core.py` | symbols: `Run.run`, `Run.dist`
- `pftools/compute_domain.c` | symbols: `ComputeDomain`, `Extract2DDomain`
- `pftools/water_balance.c` | symbols: `ComputeSurfaceStorage`, `ComputeSubsurfaceStorage`, `ComputeSurfaceRunoff`
- `pftools/velocity.c` | symbols: `CompCellVel`, `CompVertVel`, `CompBFCVel`, `CompVMag`
- `pfsimulator/parflow_lib/solver_richards.c` | symbols: `SolverRichards` output/diagnostic writes
- `pfsimulator/parflow_lib/read_parflow_binary.c` | symbols: `ReadPFBinary`
- `pfsimulator/parflow_lib/timing.c` | symbols: `RegisterTiming`, `PrintTiming`
