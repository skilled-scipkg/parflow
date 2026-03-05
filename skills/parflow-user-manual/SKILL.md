---
name: parflow-user-manual
description: This skill should be used when users ask for user-manual navigation and chapter-backed answers in parflow; it prioritizes manual chapters first and escalates to source only when needed.
---

# parflow: User Manual

## High-Signal Playbook

### Route conditions
- Use this skill when the user asks “where in the manual” or needs chapter-level guidance/citations across topics.
- Route to `parflow-build-and-install`, `parflow-inputs-and-modeling`, `parflow-api-and-scripting`, or `parflow-simulation-workflows` for deep technical execution.
- Route to `parflow-advanced-topics` for design-doc process and release-process content.

### Triage questions
- Is the user at install, setup, modeling, execution, or analysis stage?
- Do they need TCL, Python, or both?
- Are they asking for conceptual equations, key definitions, or file-format behavior?
- Do they need a runnable snippet or just chapter references?
- Do they need manual build instructions for local docs?

### Canonical workflow
1. Start from `docs/user_manual/index.rst` to locate the correct chapter.
2. Resolve specifics in chapter docs (`docs/user_manual/start.rst`, `docs/user_manual/pfsystem.rst`, `docs/user_manual/models.rst`, `docs/user_manual/files.rst`, `docs/user_manual/keys.rst`, `docs/user_manual/pftools.rst`, `docs/user_manual/python/*`).
3. If key syntax is unclear, cross-check with Python run-script docs and test scripts.
4. If chapter content is insufficient, escalate to source entry links in `references/source_map.md`.
5. Keep final answers chapter-cited and minimally sufficient.

### Minimal working example
```shell
# Build local user manual docs
cd docs/user_manual
python3 -m pip install -r requirements.txt
make html
```

### Pitfalls and fixes
- Mixing chapter intent causes incorrect routing (for example, using `docs/user_manual/models.rst` for scripting syntax questions).
- Manual examples are often TCL-first; Python equivalents may require `docs/user_manual/python/*`.
- Missing Sphinx dependencies blocks local manual builds.
- Key usage without checking chapter context can miss required companion keys.
- Release workflow and RFC process are outside the core manual and belong to `parflow-advanced-topics`.

### Convergence and validation checks
- Every answer cites at least one concrete chapter file path.
- Key-setting guidance is consistent with `docs/user_manual/keys.rst` and script examples.
- Runnable guidance maps to an existing script in `test/` or `examples/`.
- Escalation to source occurs only after chapter coverage is exhausted.

## Scope
- Handle manual chapter routing and cross-topic synthesis.
- Keep responses chapter-backed, compact, and executable when requested.

## Primary documentation references
- `docs/user_manual/index.rst`
- `docs/user_manual/intro.rst`
- `docs/user_manual/start.rst`
- `docs/user_manual/pfsystem.rst`
- `docs/user_manual/models.rst`
- `docs/user_manual/files.rst`
- `docs/user_manual/keys.rst`
- `docs/user_manual/pftools.rst`
- `docs/user_manual/python/index.rst`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md`.
- If unresolved after docs, inspect `references/source_map.md` and entry points below.
- Route design/release content to `parflow-advanced-topics`.

## Source entry points for unresolved issues
- `pftools/usergrid.c`
- `pfsimulator/parflow_lib/usergrid_input.c`
- `pfsimulator/parflow_lib/distribute_usergrid.c`
- `pftools/compute_domain.c`
- `pftools/geometry.h`
- `pftools/water_table.c`
- `pftools/water_balance.c`
- `pftools/velocity.c`
