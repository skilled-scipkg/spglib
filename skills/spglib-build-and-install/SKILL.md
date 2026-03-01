---
name: spglib-build-and-install
description: Use this skill for building, installing, linking, and validating spglib across C, Python, and Fortran workflows.
---

# spglib: Build and Install

## High-Signal Playbook

### Route conditions
- Use `spglib-api-and-scripting` when the request is about API semantics, not toolchain setup.
- Use `spglib-simulation-workflows` when the user mainly needs runnable examples.
- Use `spglib-developer-guide` for contributor testing matrix or benchmark workflow.

### Triage questions
- Which interface is needed: C only, Python, Fortran, or mixed?
- Are they consuming a release package (`pip`/`conda`) or building from source?
- Do they need shared or static libs?
- Is `SPGLIB_WITH_Fortran` and/or `SPGLIB_WITH_Python` required?
- Do they need test-enabled builds (`SPGLIB_WITH_TESTS=ON`)?
- Is runtime library discovery failing (`LD_LIBRARY_PATH`/`DYLD_LIBRARY_PATH`)?

### Canonical workflow
1. Pick distribution path first (`pip`/`conda`) when no local C/Fortran customization is needed (`README.md`, `docs/python-interface.md`).
2. For source builds, configure with CMake from repo root (`README.md`, `docs/install.md`, `cmake/README.md`).
3. Enable interfaces explicitly with flags (`SPGLIB_WITH_Fortran`, `SPGLIB_WITH_Python`) from `CMakeLists.txt`.
4. Build and install (`cmake --build`, `cmake --install`).
5. Validate package discovery through `find_package(Spglib)` or `pkg-config` (`cmake/README.md`, `test/example/*/README.md`).
6. Run smoke checks: `ctest --test-dir ./build`, then `pytest` for Python when installed with test extras (`test/README.md`, `python/README.rst`).

### Minimal working example
```bash
cmake -B ./build -DSPGLIB_WITH_Fortran=ON -DSPGLIB_WITH_TESTS=ON
cmake --build ./build
cmake --install ./build
ctest --test-dir ./build --output-on-failure

pip install .[test]
pytest
```

### Pitfalls and fixes
- `C11` is required by core C build: use a compiler/toolchain that supports it (`README.md`, `docs/index.md`).
- Fortran array orientation differs from C: use transposed layout in Fortran examples (`fortran/README.md`, `test/example/fortran_api/example.F90`).
- Python binding may load system `libsymspg` first; adjust `LD_LIBRARY_PATH`/`DYLD_LIBRARY_PATH` if wrong ABI is loaded (`python/README.rst`, `docs/python-interface.md`).
- `SPGLIB_WITH_TESTS` defaults depend on top-level/project mode; set explicitly in scripted CI (`CMakeLists.txt`).
- Sanitizers are compiler-limited; Intel/MSVC path warns unsupported (`test/CMakeLists.txt`).

### Convergence and validation checks
- `ctest --test-dir ./build -N` lists expected test inventory (`test/README.md`).
- Example binaries run and print dataset fields (`test/example/c_api/example.c`, `test/example/fortran_api/example.F90`).
- Python import succeeds and returns version (`python/README.rst`, `python/spglib/utils.py`).
- `find_package(Spglib)` resolves targets (`Spglib::symspg`, `Spglib::fortran`) where expected (`cmake/README.md`).

## Scope
- Build, installation, compilation, linking, packaging, and environment setup.

## Primary documentation references
- `README.md`
- `docs/install.md`
- `cmake/README.md`
- `docs/python-interface.md`
- `python/README.rst`
- `fortran/README.md`
- `test/README.md`
- `test/example/c_api/README.md`
- `test/example/fortran_api/README.md`

## Workflow
- Start from primary references.
- Escalate to `references/doc_map.md` for additional docs in topic scope.
- Escalate to `references/source_map.md` for implementation-level behavior.
- Cite exact file paths used.

## Tutorials and examples
- `example`
- `test/example`

## Test references
- `test`
- `.distro/tests`

## Source entry points for unresolved issues
- `CMakeLists.txt`
- `cmake/README.md`
- `cmake/SpglibConfig.cmake.in`
- `cmake/spglib.pc.in`
- `fortran/CMakeLists.txt`
- `fortran/spglib_f08.F90`
- `python/CMakeLists.txt`
- `pyproject.toml`
- `test/CMakeLists.txt`
