# parflow source map: Build and Install

Generated from source roots:
- `pf-keys`
- `pfnuopc`
- `pfsimulator`
- `pftools`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Fast source navigation
- `rg -n "PARFLOW_AMPS_LAYER|PARFLOW_HAVE_CLM|PARFLOW_ENABLE_PYTHON|KOKKOS|CUDA" CMakeLists.txt pfsimulator pftools`
- `rg -n "int main|Run\.run|amps_Init" pfsimulator pftools/python`

## Function-level entry points
- `CMakeLists.txt` | build keys: `PARFLOW_AMPS_LAYER`, `PARFLOW_ACCELERATOR_BACKEND`, `PARFLOW_ENABLE_PYTHON`
- `pfsimulator/CMakeLists.txt` | build graph for simulator libraries and executable
- `pfsimulator/amps/mpi1/amps_init.c` | symbols: `amps_Init`, `amps_Finalize`
- `pfsimulator/amps/cuda/amps_init.c` | symbols: `amps_Init`, `amps_Finalize`
- `pfsimulator/parflow_exe/main.c` | symbols: `main` (backend init, rank/device setup, run dispatch)
- `pfsimulator/parflow_lib/solver.c` | symbols: `Solve` (solver module selection)
- `pftools/python/parflow/tools/core.py` | symbols: `Run.run`, `Run.write`, `Run.dist`
- `pftools/python/parflow/tools/io.py` | symbols: `write_pfb`, `undist`
