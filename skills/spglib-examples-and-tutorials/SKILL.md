---
name: spglib-examples-and-tutorials
description: Use this skill to locate runnable spglib examples and map them to API documentation quickly.
---

# spglib: Examples and Tutorials

## High-Signal Playbook

### Route conditions
- Use `spglib-build-and-install` if build, linker, or import discovery fails.
- Use `spglib-api-and-scripting` when interpreting API behavior beyond example usage.
- Use `spglib-inputs-and-modeling` when adapting example inputs to new structures.

### Triage questions
- Which path is required first: C, Python, or Fortran?
- Is the user running from source tree (`test/example/*`) or an installed package?
- Is the goal smoke validation or adapting to custom lattice/positions/types?
- Which output fields are required (`international`, `number`, `equivalent_atoms`)?

### Canonical workflow
1. Choose language flow from `example/README.md`.
2. Build C/Fortran examples with CMake when needed (`test/example/c_api/README.md`, `test/example/fortran_api/README.md`).
3. Run Python example directly and confirm importability (`test/example/python_api/README.md`).
4. Map each called function to API docs (`docs/api.md`, `docs/python-interface.md`).
5. Adapt only input cell arrays and keep tolerance fixed for first comparison.

### Minimal working example
```bash
cmake -B ./build
cmake --build ./build
./build/example_c
./build/example_f
python test/example/python_api/example.py
```

### Convergence and validation checks
- Output includes valid space-group identity (symbol/number) for baseline cells.
- `equivalent_atoms` or equivalent partitioning fields are non-empty.
- C/Python/Fortran outputs are qualitatively consistent for the same test structure.
- Re-running identical inputs yields identical outputs.

## Scope
- Locate and run canonical C, Python, and Fortran examples.
- Map each example directly to its API surface and docs.

## Primary documentation references
- `example/README.md`
- `test/example/c_api/README.md`
- `test/example/python_api/README.md`
- `test/example/fortran_api/README.md`
- `docs/api.md`
- `docs/python-interface.md`
- `docs/interface.md`

## Quick mapping
- C example: `test/example/c_api/example.c` -> C API docs in `docs/api.md`.
- Python example: `test/example/python_api/example.py` -> Python API docs in `docs/python-interface.md` and autodoc pages.
- Fortran example: `test/example/fortran_api/example.F90` -> interface notes in `docs/interface.md` and `fortran/README.md`.

## Workflow
- Start from the primary references above.
- If details are missing, inspect `references/doc_map.md` for the full inventory.
- Use `references/source_map.md` to jump to implementation files only for unresolved behavior.
- Cite exact file paths in responses.

## Tutorials and examples
- `example`
- `test/example`

## Test references
- `test`
- `.distro/tests`

## Source entry points for unresolved issues
- `test/example/c_api/example.c`
- `test/example/python_api/example.py`
- `test/example/fortran_api/example.F90`
- `test/example/c_api/CMakeLists.txt`
- `test/example/fortran_api/CMakeLists.txt`
- `python/spglib/spg.py`
- `include/spglib.h`
