---
name: spglib-index
description: This skill routes spglib requests by intent, enforces docs-first resolution, and escalates to concrete source entry points only when needed.
---

# spglib Skills Index

## Route the request
- `spglib-build-and-install`: CMake configuration, packaging, installation, linking, toolchain issues.
- `spglib-api-and-scripting`: C/Python/Fortran API usage, dataset access, error handling, compatibility behavior.
- `spglib-simulation-workflows`: Runnable C/Python/Fortran example flows and quick correctness checks.
- `spglib-inputs-and-modeling`: Cell conventions, tolerances, coordinate/basis definitions, transformation semantics.
- `spglib-developer-guide`: repository architecture, generated database components, test layers, performance and magnetic dev notes.
- `spglib-examples-and-tutorials`: where examples live and how to map them to API docs.
- `spglib-variable`: variable-level meanings (`lattice`, `position`, `types`, tolerances) and C vs Python orientation.
- `spglib-advanced-topics`: low-frequency topics merged from one-doc skills (dataset reference details, magnetic dataset reference details, codespell wordlist, startup/testing pointers, performance note).
- Testing and CI questions: route to `spglib-developer-guide` first, then `spglib-build-and-install` for environment-specific build/test failures.

## Docs-first workflow (mandatory)
- Start from topic skill `## Primary documentation references`.
- If insufficient, inspect that topic skill's doc map in its `references` folder.
- Escalate to that topic skill's source map only for unresolved behavior details.
- Prefer targeted symbol lookup before broad source reading:
  - `rg -n "<symbol_or_keyword>" cmake database fortran include python ruby src`

## Fast simulation start
1. Build and run baseline checks:
```bash
cmake -B ./build -DSPGLIB_WITH_Fortran=ON -DSPGLIB_WITH_TESTS=ON
cmake --build ./build
ctest --test-dir ./build --output-on-failure
```
2. Run language examples:
```bash
./build/example_c
./build/example_f
python test/example/python_api/example.py
```
3. Validate checkpoints before deeper debugging:
- C/Python/Fortran outputs report a valid space-group symbol/number.
- Dataset-style fields (`equivalent_atoms`, operation count) are non-empty.
- Re-running with identical inputs is deterministic.

## Canonical roots
- Documentation roots: `README.md`, `docs/index.md`, `docs`, `python/README.rst`.
- Tutorial/example roots: `example`, `test/example`.
- Test roots: `test`, `.distro/tests`.
- Source roots: `cmake`, `database`, `fortran`, `include`, `python`, `ruby`, `src`.

## Fast escalation entry points
- Build/install behavior: `CMakeLists.txt`, `cmake/README.md`, `fortran/CMakeLists.txt`, `python/CMakeLists.txt`.
- C API signatures and lifetimes: `include/spglib.h`, `src/spglib.c`, `src/spglib_f.c`.
- Python binding behavior: `python/spglib/spg.py`, `python/spglib/msg.py`, `python/spglib/cell.py`, `python/spglib/error.py`, `python/spglib/utils.py`.
- Example truth set: `test/example/c_api/example.c`, `test/example/python_api/example.py`, `test/example/fortran_api/example.F90`.
- Developer/testing architecture: `docs/development/develop.md`, `test/README.md`, `test/CMakeLists.txt`, `database/README.md`.
