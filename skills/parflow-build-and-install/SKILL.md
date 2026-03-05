---
name: parflow-build-and-install
description: This skill should be used when users ask about build and install in parflow; it prioritizes documentation references and then source inspection only for unresolved details.
---

# parflow: Build and Install

## High-Signal Playbook

### Route conditions
- Use this skill for configure/build/install failures, dependency toggles, and backend selection (`mpi1`, `omp`, `cuda`, `kokkos`).
- Route to `parflow-simulation-workflows` for run/checkpoint/restart behavior after a successful build.
- Route to `parflow-api-and-scripting` for Python/TCL script authoring details.

### Triage questions
- Which branch/tag and platform are you building on?
- Do you need CPU-only, OpenMP, CUDA, or Kokkos?
- Which AMPS layer is required (`seq`, `mpi1`, `cuda`, `smpi`, `oas3`)?
- Do you need CLM, Python, NetCDF, SILO, or KINSOL/SUNDIALS integration?
- Are `PARFLOW_DIR` and dependency roots (`KOKKOS_ROOT`, `UMPIRE_ROOT`, `RMM_ROOT`, etc.) set?
- Is this a clean out-of-source build directory?

### Canonical workflow
1. Set install prefix (`PARFLOW_DIR`) and create a clean build directory.
2. Configure with CMake minimal flags first; add optional modules only after the baseline build works.
3. Select backend and AMPS layer consistently (`mpi1` for standard MPI builds).
4. Build and install (`make`, `make install`).
5. Run a baseline smoke test from `test/tcl`: `tclsh default_single.tcl 1 1 1`.
6. Inspect `<run>.out.log` and `<run>.out.txt` before enabling extra features.

### Minimal working example
```shell
export PARFLOW_DIR=/path/to/parflow-install
mkdir -p build && cd build
cmake .. \
  -DCMAKE_INSTALL_PREFIX="${PARFLOW_DIR}" \
  -DPARFLOW_HAVE_CLM=ON \
  -DPARFLOW_AMPS_LAYER=mpi1
make -j"$(nproc)"
make install
cd ../test/tcl
tclsh default_single.tcl 1 1 1
```

### Pitfalls and fixes
- `PARFLOW_ACCELERATOR_BACKEND=kokkos` without `KOKKOS_ROOT` fails at configure time; set `-DKOKKOS_ROOT=/path/to/Kokkos`.
- `PARFLOW_AMPS_LAYER=cuda` without GPU backend is rejected; pair it with `-DPARFLOW_ACCELERATOR_BACKEND=cuda`.
- `UMPIRE_ROOT` and `RMM_ROOT` cannot both be enabled.
- OpenMP (`omp`) and CUDA workflows are separate; do not combine both accelerator modes.
- Python builds require single-file AMPS I/O; disabling `PARFLOW_AMPS_SEQUENTIAL_IO` is incompatible with Python mode.
- CUDA builds often need explicit architecture (`-DCMAKE_CUDA_ARCHITECTURES=<cc>`) and may need `CUDAHOSTCXX=mpicxx`.

### Convergence and validation checks
- `make install` produces runnable binaries and tool scripts under `PARFLOW_DIR`.
- Baseline `default_single` run completes and writes `default_single.out.log` and `default_single.out.txt`.
- For Richards workflows, verify nonlinear history in `<run>.out.kinsol.log`.
- For accelerator runs, confirm rank/device mapping and compare one baseline output against CPU results within expected tolerance.

## Scope
- Handle questions about build, installation, compilation, and environment setup.
- Keep responses docs-first, then inspect source only for unresolved implementation details.

## Primary documentation references
- `README.md`
- `README-GPU.md`
- `README-OPENMP.md`
- `README-SAMRAI.md`
- `CMakeLists.txt`
- `docs/user_manual/start.rst`
- `docs/user_manual/python/getting_started.rst`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md`.
- If ambiguity remains, inspect `references/source_map.md` and the entry points below.
- Cite exact documentation file paths in responses.

## Source entry points for unresolved issues
- `CMakeLists.txt`
- `pfsimulator/CMakeLists.txt`
- `pfsimulator/amps/mpi1/amps_init.c`
- `pfsimulator/amps/cuda/amps_init.c`
- `pfsimulator/parflow_exe/main.c`
- `pfsimulator/parflow_lib/solver.c`
- `pftools/python/parflow/tools/core.py`
- `pftools/python/parflow/tools/io.py`
