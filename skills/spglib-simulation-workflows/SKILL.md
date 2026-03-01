---
name: spglib-simulation-workflows
description: Use this skill for runnable spglib example workflows (C, Python, Fortran) and quick correctness checks.
---

# spglib: Simulation Workflows

## High-Signal Playbook

### Route conditions
- Use `spglib-build-and-install` if build/link/install steps fail before running examples.
- Use `spglib-api-and-scripting` for API-level interpretation beyond example flow.
- Use `spglib-inputs-and-modeling` for cell-convention or tolerance-interpretation issues.

### Triage questions
- Which language example is needed (C, Python, Fortran)?
- Running from `test/example/*` or `example/*` tree?
- Is spglib already installed/discoverable by CMake or Python?
- Is the goal smoke validation, or adaptation to a new structure?
- Which output fields are required for acceptance (symbol, number, Wyckoff, ops)?

### Canonical workflow
1. Start from `example/README.md` to choose language path.
2. For C/Fortran examples, follow `test/example/*/README.md` CMake flows.
3. For Python, run `python example.py` after confirming package importability (`test/example/python_api/README.md`).
4. Validate expected dataset-style output fields (symbol, Hall symbol, equivalent atoms).
5. Replace only lattice/positions/types and re-run with same tolerance to reproduce user structure.
6. Escalate to API docs when interpreting nontrivial fields (`docs/api.md`, `docs/dataset.md`).

### Minimal working example
```bash
# C and Fortran example builds
cmake -B ./build
cmake --build ./build
./build/example_c
./build/example_f

# Python example
python test/example/python_api/example.py
```

### Pitfalls and fixes
- Python and C lattice orientations differ; copy data in the correct convention before comparing outputs (`docs/python-interface.md`, `docs/variable.md`).
- Manual compile paths need correct include/lib flags (`test/example/c_api/README.md`, `test/example/fortran_api/README.md`).
- Fortran examples require `Spglib::fortran` target or `spglib_f08` pkg-config path, not only `symspg` (`test/example/fortran_api/CMakeLists.txt`).
- CMake find-package failures usually indicate missing install prefix/runtime paths.

### Convergence and validation checks
- Example runs print consistent space-group metadata for Wurtzite test cell.
- Operation count and equivalent-atom mapping are non-empty and plausible.
- Re-running with identical input is deterministic.
- Adapted input changes outputs in expected ways when tolerance changes are controlled.

## Scope
- Simulation setup, execution flow, and runtime validation using official examples.

## Primary documentation references
- `example/README.md`
- `test/example/c_api/README.md`
- `test/example/python_api/README.md`
- `test/example/fortran_api/README.md`
- `docs/api.md`
- `docs/dataset.md`

## Workflow
- Start from primary references.
- Use `references/doc_map.md` for additional example docs.
- Use `references/source_map.md` for implementation-level behavior differences.
- Cite exact file paths used.

## Tutorials and examples
- `example`
- `test/example`

## Test references
- `test`
- `.distro/tests`

## Source entry points for unresolved issues
- `test/example/c_api/example.c`
- `test/example/fortran_api/example.F90`
- `test/example/python_api/example.py`
- `test/example/c_api/CMakeLists.txt`
- `test/example/fortran_api/CMakeLists.txt`
- `python/spglib/spg.py`
- `include/spglib.h`
