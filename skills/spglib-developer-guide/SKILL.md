---
name: spglib-developer-guide
description: Use this skill for spglib contributor workflows across architecture, database generation, testing layers, and performance/magnetic development notes.
---

# spglib: Developer Guide

## High-Signal Playbook

### Route conditions
- Use `spglib-build-and-install` for user-facing install support rather than contributor workflows.
- Use `spglib-api-and-scripting` for end-user API call semantics.
- Use `spglib-simulation-workflows` for example-first reproduction.

### Triage questions
- Which subsystem is touched: core C (`src`), bindings (`python`, `fortran`), or build/packaging (`cmake`)?
- Is behavior change in non-magnetic symmetry, magnetic symmetry, or packaging?
- Which test layer is failing: unit, integration, functional, example, package, pytest, tmt?
- Is database regeneration required (`database/msg/*` scripts)?
- Is this correctness work, performance work, or both?

### Canonical workflow
1. Map requested change to subsystem boundaries (`docs/index.md`, directory layout).
2. Apply focused implementation updates in core/binding/build components.
3. Build with explicit test flags (`SPGLIB_WITH_TESTS`, optional Fortran/Python).
4. Execute targeted `ctest` subsets first (`-L` labels), then broad pass (`test/README.md`).
5. Run Python tests (`pytest`) for binding-sensitive changes (`python/README.rst`, `test/README.md`).
6. For magnetic behavior changes, re-check flag semantics and dataset expectations (`docs/development/magnetic_symmetry_flags.md`).
7. For performance changes, run benchmark command and compare trend (`docs/development/performance.md`).

### Minimal working example
```bash
cmake -B ./build -DSPGLIB_WITH_TESTS=ON -DSPGLIB_WITH_Fortran=ON
cmake --build ./build
ctest --test-dir ./build -L unit_tests --output-on-failure
ctest --test-dir ./build -L functional_tests --output-on-failure
pytest
```

### Pitfalls and fixes
- `SPG_API_TEST` exposure is needed for some unit-test internals (`test/README.md`).
- Sanitizer mode is compiler-dependent and may warn unsupported (`test/CMakeLists.txt`).
- Fortran interface keeps C memory order by transposed dimension usage (`fortran/README.md`).
- Magnetic flags (`with_time_reversal`, `is_axial`, `tensor_rank`) are easy to regress; always cross-check doc behavior matrix (`docs/development/magnetic_symmetry_flags.md`).
- Database scripts can diverge from committed generated tables if regeneration steps are partial (`database/README.md`, `database/msg/*`).

### Convergence and validation checks
- All impacted test layers pass (`ctest` labels + `pytest`).
- Example and package tests still discover/link targets correctly (`test/example`, `test/package`).
- Benchmark command remains within expected regression envelope for touched paths.
- Magnetic workflows preserve expected operation counts/flags for representative cells.

## Scope
- Developer architecture, extension points, test strategy, and maintenance workflows.

## Primary documentation references
- `docs/development/develop.md`
- `docs/development/performance.md`
- `docs/development/magnetic_symmetry_flags.md`
- `docs/index.md`
- `test/README.md`
- `database/README.md`

## Workflow
- Start from primary references.
- Escalate to `references/doc_map.md` for inventory-level context.
- Escalate to `references/source_map.md` for implementation-level behavior.
- Cite exact file paths used.

## Tutorials and examples
- `example`
- `test/example`

## Test references
- `test`
- `.distro/tests`

## Source entry points for unresolved issues
- `src/spglib.c`
- `src/spglib_f.c`
- `src/symmetry.c`
- `src/spacegroup.c`
- `src/magnetic_spacegroup.c`
- `src/msg_database.c`
- `include/spglib.h`
- `test/CMakeLists.txt`
- `database/make_spgtype_db.py`
- `database/msg/make_msgtype_db.py`
- `database/msg/make_mhall_db.py`
