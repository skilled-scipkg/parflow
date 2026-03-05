---
name: parflow-index
description: This skill should be used when users ask how to use parflow and the correct generated documentation skill must be selected before going deeper into source code.
---

# parflow Skills Index

## Route the request
- Use docs-first routing. Start in the narrowest topic skill; do not jump to source unless docs and examples are insufficient.
- Build, configuration, dependency, accelerator backend, and toolchain issues -> `parflow-build-and-install`.
- First-run setup, solver orientation, and baseline script execution -> `parflow-getting-started`.
- Input keys, geometry/material/boundary parameterization -> `parflow-inputs-and-modeling`.
- Runnable examples/tutorial adaptation -> `parflow-examples-and-tutorials`.
- Python/TCL scripting, CLI, key-generation workflow -> `parflow-api-and-scripting`.
- Prepare-run-checkpoint-restart-output sequence and regression checks -> `parflow-simulation-workflows`.
- Output interpretation and analysis workflows -> `parflow-analysis-and-output`.
- Test suite behavior and regression harness details -> `parflow-test`.
- User manual chapter navigation and citation strategy -> `parflow-user-manual`.
- Release process and design-document process topics -> `parflow-advanced-topics`.

## Escalation path (strict)
- Step 1: answer from the selected skill `SKILL.md` and its primary docs.
- Step 2: if details are missing, open the same skill `references/doc_map.md`.
- Step 3: if docs are still insufficient, open the same skill `references/source_map.md`.
- Step 4: run targeted source lookup only in core source roots:
  - `rg -n "<symbol_or_keyword>" pf-keys pfnuopc pfsimulator pftools`

## Coverage map
- Documentation roots: `docs`, `docs/user_manual`, `docs/user_manual/python`, `docs/user_manual/python/tutorials`.
- Tutorial and examples roots: `examples`, `test/tcl`, `test/python`.
- Regression and behavior roots: `test`, `pftools/test`, `pfsimulator/amps/test`, `performance_tests`.
- Source escalation roots: `pf-keys`, `pfnuopc`, `pfsimulator`, `pftools`.

## Generated topic skills
- `parflow-build-and-install`
- `parflow-getting-started`
- `parflow-inputs-and-modeling`
- `parflow-examples-and-tutorials`
- `parflow-api-and-scripting`
- `parflow-simulation-workflows`
- `parflow-analysis-and-output`
- `parflow-test`
- `parflow-user-manual`
- `parflow-advanced-topics`
