---
name: parflow-advanced-topics
description: This skill should be used when users ask about ParFlow release-process or design-document workflows that are low-frequency and outside the core run/build/modeling path.
---

# parflow: Advanced Topics

## Scope
- Consolidated low-frequency docs topics to reduce routing noise.
- Covers design-document workflow and release-process workflow.

## Route the request
- RFC/design proposal lifecycle and statuses -> `docs/design_documents/README.md`.
- Release cut, version-file updates, release notes, and package publish process -> `docs/manuals/release_process.md`.
- If the request shifts to build/runtime behavior, route back to core skills (`parflow-build-and-install`, `parflow-simulation-workflows`, `parflow-api-and-scripting`).

## Primary documentation references
- `docs/design_documents/README.md`
- `docs/manuals/release_process.md`

## Workflow
- Start from the two primary docs above.
- If details are missing, inspect `references/doc_map.md`.
- If implementation detail is required (process-grid internals or tooling hooks), inspect `references/source_map.md`.
- Cite exact file paths in responses.

## Source entry points for unresolved issues
- `pfsimulator/parflow_lib/process_grid.c`
- `pfsimulator/parflow_lib/line_process.c`
- `pftools/compute_domain.c`
- `pftools/resource.h`
- `pftools/geometry.h`
