# parflow source map: Analysis and Output

Generated from source roots:
- `pf-keys`
- `pfnuopc`
- `pfsimulator`
- `pftools`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Fast source navigation
- `rg -n "ReadPFBinary|ReadPFNC|WriteCLMNC|Print.*Overland|NetCDF" pfsimulator/parflow_lib`
- `rg -n "read_pfb|read_pfb_sequence|calculate_overland_flow|pf_test_file" pftools/python/parflow/tools`

## Function-level entry points
- `pfsimulator/parflow_lib/read_parflow_binary.c` | symbols: `ReadPFBinary`, `ReadPFBinary_Subvector`
- `pfsimulator/parflow_lib/read_parflow_netcdf.c` | symbols: `ReadPFNC`, `OpenNCFile`, `ReadNCFile`
- `pfsimulator/parflow_lib/write_clm_netcdf.c` | symbols: `WriteCLMNC`, `PutCLMDataInNC`, `CloseCLMNC`
- `pfsimulator/parflow_lib/solver_richards.c` | symbols: `SolverRichards` output/write paths
- `pftools/python/parflow/tools/io.py` | symbols: `read_pfb`, `read_pfb_sequence`, `undist`
- `pftools/python/parflow/tools/hydrology.py` | symbols: `calculate_subsurface_storage`, `calculate_overland_flow`
- `pftools/python/parflow/tools/compare.py` | symbols: `pf_test_file`, `pf_test_file_with_abs`
- `test/tcl/pftest.tcl` | symbols: `pftestFile`, `pftestFileWithAbs`
- `pftools/prepostproc/pfb2nc.py` | entry: script-level PFB-to-NetCDF conversion flow
