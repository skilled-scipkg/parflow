---
name: parflow-examples-and-tutorials
description: This skill should be used when users ask about examples and tutorials in parflow; it prioritizes documentation references and then source inspection only for unresolved details.
---

# parflow: Examples and Tutorials

## High-Signal Playbook

### Route conditions
- Use this skill to pick and adapt a runnable baseline example (TCL or Python) with minimal edits.
- Route to `parflow-inputs-and-modeling` when the request is about model/key semantics rather than example selection.
- Route to `parflow-api-and-scripting` for converter/tooling details (`tcl2py`, `pfdist_sort`, etc.).

### Triage questions
- Do you need a fully saturated, Richards, overland, or CLM-oriented baseline?
- Do you want TCL-first, Python-first, or dual-language parity?
- Are you validating against `examples/correct_output` or `test/*/correct_output`?
- Are required auxiliary files (`.pfb`, `.pfsol`) already available in the run directory?
- Is the goal learning, regression parity, or production run bootstrapping?

### Canonical workflow
1. Choose the closest baseline from `examples/` or `test/`.
2. Run it unchanged once and confirm baseline parity.
3. Edit one block at a time (topology, geometry, properties, BCs, solver).
4. Re-run and compare selected outputs to reference outputs.
5. Keep a changelog of key edits so differences remain attributable.

### Minimal working example
```shell
# Python baseline from examples/
cd examples
python3 example_single.py

# TCL baseline from examples/
tclsh example_single.tcl
```

### Pitfalls and fixes
- Copying a script without companion input/reference files causes false failures.
- Large multi-parameter edits in one pass hide the true source of regressions.
- `tcl2py` output is a starting point; manual edits are expected for full parity.
- Floating-point differences need tolerance-based comparison, not exact byte-equality.
- Baselines may use specific naming conventions for outputs and working directories.

### Convergence and validation checks
- Unmodified baseline example runs successfully before adaptation.
- At least one pressure/saturation/permeability output matches the reference within tolerance.
- Output file naming and dump cadence stay consistent after edits.
- Reproducibility check: second run with same inputs matches first run behavior (allowing documented GPU nondeterminism caveats).

## Scope
- Handle worked examples and tutorial-driven onboarding workflows.
- Prefer smallest reproducible script that demonstrates the requested behavior.

## Primary documentation references
- `docs/user_manual/README.md`
- `docs/user_manual/PfkeysExample/index.rst`
- `docs/user_manual/PfkeysExample/permeability/index.rst`
- `docs/user_manual/PfkeysExample/porosity/index.rst`
- `docs/user_manual/python/tutorials/index.rst`
- `docs/user_manual/python/tutorials/tcl2py.rst`
- `examples/example_single.py`
- `examples/example_single.tcl`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md`.
- Use `examples/correct_output` and `test/*/correct_output` for regression anchors.
- If ambiguity remains, inspect `references/source_map.md` and entry points below.

## Source entry points for unresolved issues
- `examples/example_single.py`
- `examples/example_single.tcl`
- `test/tcl/default_single.tcl`
- `test/tcl/default_richards.tcl`
- `test/python/default_single.py`
- `test/python/default_richards.py`
- `pfsimulator/parflow_lib/problem_porosity.c`
- `pfsimulator/parflow_lib/permeability_face.c`
- `pfsimulator/parflow_lib/input_porosity.c`
