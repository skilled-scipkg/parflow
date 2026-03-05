# parflow source map: Examples and Tutorials

Generated from source roots:
- `pf-keys`
- `pfnuopc`
- `pfsimulator`
- `pftools`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Fast source navigation
- `rg -n "example_single|default_single|domain_builder|tcl2py|pf_test_file" examples test pftools/python`
- `rg -n "Porosity|PermeabilityFace|Indicator|ReadPFBinary" pfsimulator/parflow_lib`

## Function-level entry points
- `examples/example_single.py` | flow: baseline example and execution arguments
- `examples/example_single.tcl` | flow: baseline TCL example and output checks
- `test/python/default_single.py` | flow: regression comparison pattern with `pf_test_file`
- `test/tcl/default_single.tcl` | flow: TCL regression pattern with `pftestFile`
- `pftools/python/parflow/cli/tcl2py.py` | symbols: `tcl_to_python`
- `pftools/python/parflow/tools/builders.py` | symbols: `DomainBuilder` methods and overland setup helpers
- `pftools/python/parflow/tools/compare.py` | symbols: `pf_test_file`, `pf_test_file_with_abs`
- `pfsimulator/parflow_lib/problem_porosity.c` | symbols: `Porosity`
- `pfsimulator/parflow_lib/permeability_face.c` | symbols: `PermeabilityFace`
- `pfsimulator/parflow_lib/input_porosity.c` | symbols: `InputPorosity`
