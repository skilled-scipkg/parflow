# parflow source map: Advanced Topics

Generated from source roots:
- `pf-keys`
- `pfnuopc`
- `pfsimulator`
- `pftools`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Fast source navigation
- `rg -n "<symbol_or_keyword>" pf-keys pfnuopc pfsimulator pftools`
- `rg -n "release|version|design|process|rfc" docs pf-keys pfsimulator pftools`

## Function-level entry points
- `pf-keys/generators/pf-python.py` | symbols: `generate_module_from_definitions`, `generate_clm_key_dict`
- `pf-keys/generators/read_the_doc_rst.py` | symbols: `handle_domain`, `generate_module_from_definitions`
- `pf-keys/generators/simput/simput_model.py` | symbols: `create_parameters`, `attach_hooks`, `cli`
- `pfsimulator/parflow_lib/process_grid.c` | symbols: `ReadProcessGrid`, `FreeProcessGrid`
- `pfsimulator/parflow_lib/line_process.c` | symbols: `LineProc`
- `pfsimulator/parflow_lib/timing.c` | symbols: `RegisterTiming`, `PrintTiming`
- `pftools/compute_domain.c` | symbols: `ComputeDomain`, `Extract2DDomain`
