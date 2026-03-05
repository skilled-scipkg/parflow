# parflow source map: Inputs and Modeling

Generated from source roots:
- `pf-keys`
- `pfnuopc`
- `pfsimulator`
- `pftools`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Fast source navigation
- `rg -n "Geom\.|Perm\.|Porosity|BCPressure|IndicatorField|TimeCycle" pfsimulator/parflow_lib pf-keys/definitions`
- `rg -n "IDB_Get|NA_NameToIndex|CheckTime|ReadUserGrid" pfsimulator/parflow_lib`

## Function-level entry points
- `pfsimulator/parflow_lib/input_database.c` | symbols: `IDB_GetString`, `IDB_GetDouble`, `IDB_GetInt`, `NA_NameToIndex`
- `pfsimulator/parflow_lib/input_checks.c` | symbols: `CheckTime`
- `pfsimulator/parflow_lib/usergrid_input.c` | symbols: `ReadUserGrid`, `FreeUserGrid`
- `pfsimulator/parflow_lib/geometry.c` | symbols: `GeomReadSolids`, `IntersectLineWithTriangle`
- `pfsimulator/parflow_lib/grgeometry.c` | symbols: `GrGeomSolidFromInd`, `GrGeomSolidFromGeom`
- `pfsimulator/parflow_lib/problem_porosity.c` | symbols: `Porosity`
- `pfsimulator/parflow_lib/permeability_face.c` | symbols: `PermeabilityFace`
- `pfsimulator/parflow_lib/problem_spec_storage.c` | symbols: `SpecStorage`
- `pfsimulator/parflow_lib/problem_phase_rel_perm.c` | symbols: `PhaseRelPerm`
- `pfsimulator/parflow_lib/problem_saturation.c` | symbols: `Saturation`
- `pfsimulator/parflow_lib/problem_bc_pressure.c` | symbols: `BCPressureInitInstanceXtra`
- `pfsimulator/parflow_lib/time_cycle_data.c` | symbols: `TimeCycleDataComputeIntervalNumber`, `TimeCycleDataComputeNextTransition`
- `pf-keys/definitions/solver.yaml` | entry: solver key schema used by Python/TCL interfaces
