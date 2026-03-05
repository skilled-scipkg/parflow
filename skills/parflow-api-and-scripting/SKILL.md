---
name: parflow-api-and-scripting
description: This skill should be used when users ask about api and scripting in parflow; it prioritizes documentation references and then source inspection only for unresolved details.
---

# parflow: API and Scripting

## High-Signal Playbook

### Route conditions
- Use this skill for Python/TCL scripting patterns, CLI usage, run object lifecycle, and key-library generation/contribution paths.
- Route to `parflow-inputs-and-modeling` for physical parameter choices and key semantics.
- Route to `parflow-simulation-workflows` for restart/checkpoint/output validation behavior.

### Triage questions
- Are you authoring a new Python script, converting TCL, or debugging an existing run script?
- Do you need direct key assignment, `pfset(...)`, YAML-driven assignment, or all of them?
- Is validation failing before run, or is ParFlow failing at runtime?
- Do you need parity comparison between TCL-generated and Python-generated `.pfidb`?
- Are CLI topology overrides (`-p -q -r`) expected to override script defaults?

### Canonical workflow
1. Start from a known-good test script (`test/python/default_single.py` or `test/python/default_richards.py`).
2. Use `Run("name", __file__)`, set required topology/keys, then run validation.
3. Write `.pfidb` (and optional YAML/JSON) before execution for reproducibility.
4. Execute with explicit working directory and controlled overrides.
5. For TCL migration, use `python3 -m parflow.cli.tcl2py` then patch manual differences.
6. If parity is required, sort and diff `.pfidb` outputs.

### Minimal working example
```shell
# Convert a TCL script scaffold to Python
python3 -m parflow.cli.tcl2py -i test/tcl/default_richards.tcl

# Run a known Python baseline with topology overrides
python3 test/python/default_richards.py -p 1 -q 1 -r 1
```

### Pitfalls and fixes
- Dynamic token names must be declared first (`GeomInput.Names`, `Cycle.Names`, `Phase.Names`).
- Non-Pythonic tokens require bracket syntax (for example `Patch['x-lower']...`).
- `pfset(key, value)` can set non-library keys; use `validate()` to catch mistakes early.
- `tcl2py` conversion leaves commented or approximate lines that require manual cleanup.
- CLI `-p/-q/-r` can override script topology; verify final runtime topology before debugging solver behavior.

### Convergence and validation checks
- `run.validate()` returns cleanly (or only expected warnings).
- Execution writes `.out.txt` and indicates successful solve.
- For migration, sorted `.pfidb` diffs are understood and documented.
- Regression scripts in `test/python` still pass with expected tolerances.

## Scope
- Handle Python package flows, CLI helpers, and Tcl/Python interoperability.
- Keep guidance tied to tested scripts and documented APIs.

## Primary documentation references
- `docs/user_manual/python/index.rst`
- `docs/user_manual/python/getting_started.rst`
- `docs/user_manual/python/run_script.rst`
- `docs/user_manual/python/tutorials/index.rst`
- `docs/user_manual/python/tutorials/tcl2py.rst`
- `docs/user_manual/python/keys_contribution.rst`
- `test/python/README.md`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md`.
- Use `test/python` and `test/tcl` for minimal reproducible examples.
- If ambiguity remains, inspect `references/source_map.md` and the entry points below.

## Source entry points for unresolved issues
- `pftools/python/parflow/__init__.py`
- `pftools/python/parflow/tools/core.py`
- `pftools/python/parflow/tools/compare.py`
- `pftools/python/parflow/cli/tcl2py.py`
- `pftools/python/parflow/cli/pfdist_sort.py`
- `pftools/python/parflow/cli/compare_pdi_pfb.py`
- `pf-keys/generators/pf-python.py`
- `pf-keys/generators/read_the_doc_rst.py`
- `pf-keys/generators/simput/simput_model.py`
