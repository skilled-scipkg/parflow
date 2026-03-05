# parflow source map: API and Scripting

Generated from source roots:
- `pf-keys`
- `pfnuopc`
- `pfsimulator`
- `pftools`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Fast source navigation
- `rg -n "class Run|def run\(|def dist\(|def write\(|def pfset\(" pftools/python/parflow/tools`
- `rg -n "tcl_to_python|write_sorted_pfidb|pf_test_file" pftools/python/parflow`

## Function-level entry points
- `pftools/python/parflow/__init__.py` | entry: exported API surface (`Run`, comparison helpers)
- `pftools/python/parflow/tools/core.py` | symbols: `Run.write`, `Run.clone`, `Run.run`, `Run.dist`
- `pftools/python/parflow/tools/database/core.py` | symbols: key-tree objects and validation support
- `pftools/python/parflow/tools/compare.py` | symbols: `pf_test_file`, `pf_test_file_with_abs`
- `pftools/python/parflow/tools/io.py` | symbols: `read_pfb`, `write_pfb`, `read_pfidb`, `read_yaml`
- `pftools/python/parflow/cli/tcl2py.py` | symbols: `tcl_to_python`
- `pftools/python/parflow/cli/pfdist_sort.py` | symbols: `write_sorted_pfidb`
- `pftools/python/parflow/cli/compare_pdi_pfb.py` | entry: CLI-level PDI/PFB comparison
- `pf-keys/generators/pf-python.py` | symbols: `generate_module_from_definitions`
- `pf-keys/generators/read_the_doc_rst.py` | symbols: `generate_module_from_definitions`
- `pf-keys/generators/simput/simput_model.py` | symbols: `create_parameters`, `cli`
