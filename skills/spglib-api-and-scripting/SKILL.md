---
name: spglib-api-and-scripting
description: Use this skill for C/Python API usage, call patterns, error handling, and source-backed behavior checks.
---

# spglib: API and Scripting

## High-Signal Playbook

### Route conditions
- Use `spglib-build-and-install` for compiler/linker/package-manager failures.
- Use `spglib-inputs-and-modeling` for data-shape and convention questions before API invocation.
- Use `spglib-variable` for precise tolerance-variable semantics.
- Use `spglib-simulation-workflows` for runnable end-to-end examples.

### Triage questions
- C API or Python API?
- Non-magnetic or magnetic workflow?
- Need full dataset (`*_get_dataset`) or only symmetry operations?
- Is failure a null/None return, deprecation warning, or exception?
- Is hall-number-specific setting required?
- Which version behavior is expected (deprecated/experimental interfaces)?

### Canonical workflow
1. Validate cell layout and types before calls (`docs/variable.md`, `docs/python-interface.md`).
2. Start with dataset calls (`spg_get_dataset` / `get_symmetry_dataset`) for robust metadata (`docs/api.md`, `python/spglib/spg.py`).
3. For magnetic workflows, use magnetic APIs directly (`spg_get_magnetic_dataset`, `get_magnetic_symmetry_dataset`) (`docs/releases.md`, `python/spglib/msg.py`).
4. Handle errors explicitly: C via `spg_get_error_code` + `spg_get_error_message`; Python via `spglib.error.SpglibError` path (`docs/api.md`, `docs/exceptions/python.md`, `python/spglib/error.py`).
5. Free C datasets with `spg_free_dataset`/`spg_free_magnetic_dataset` (`docs/api.md`, `include/spglib.h`).
6. Escalate to `include/spglib.h` and `src/spglib.c` for exact signatures/lifetimes.

### Minimal working example
```c
SpglibDataset *dataset = spg_get_dataset(lattice, position, types, num_atom, 1e-5);
if (!dataset) {
    SpglibError err = spg_get_error_code();
    printf("spglib failed: %s\n", spg_get_error_message(err));
    return 1;
}
printf("%s (%d)\n", dataset->international_symbol, dataset->spacegroup_number);
spg_free_dataset(dataset);
```

```python
import spglib
cell = (lattice, positions, numbers)
dataset = spglib.get_symmetry_dataset(cell, symprec=1e-5)
print(dataset.international, dataset.number)
```

### Pitfalls and fixes
- C `spg_get_error_message` path is not thread-safe; serialize per-process error polling (`docs/api.md`).
- Python `get_symmetry(..., is_magnetic=True)` is deprecated; use magnetic-specific APIs (`docs/releases.md`, `docs/development/magnetic_symmetry_flags.md`).
- C and Python lattice conventions differ in orientation; confirm before blaming API (`docs/variable.md`, `docs/python-interface.md`, `python/spglib/utils.py`).
- Hall-number mismatch can return invalid dataset (`spacegroup_number == 0` / failure) (`docs/api.md`).
- Forgetting C dataset free causes leaks (`docs/api.md`, `test/example/c_api/example.c`).

### Convergence and validation checks
- Dataset is non-null / non-None and `n_operations > 0`.
- Reported space-group number/symbol is stable for small `symprec` sweeps.
- `equivalent_atoms` length matches `n_atoms` and indexing assumptions.
- Magnetic workflows verify `time_reversals` content when `with_time_reversal` toggles (`python/spglib/msg.py`).

## Scope
- Language bindings, APIs, and programmatic interfaces.

## Primary documentation references
- `docs/api.md`
- `docs/api/index.md`
- `docs/interface.md`
- `docs/python-interface.md`
- `docs/exceptions/index.md`
- `docs/exceptions/python.md`
- `docs/development/magnetic_symmetry_flags.md`
- `docs/releases.md`

## Workflow
- Start from primary references.
- Use `references/doc_map.md` when API details are spread across docs.
- Use `references/source_map.md` for unresolved implementation details.
- Cite exact file paths used.

## Tutorials and examples
- `example`
- `test/example`

## Test references
- `test`
- `.distro/tests`

## Source entry points for unresolved issues
- `include/spglib.h`
- `src/spglib.c`
- `src/spglib_f.c`
- `python/_spglib.cpp`
- `python/py_bindings.cpp`
- `python/spglib/spg.py`
- `python/spglib/msg.py`
- `python/spglib/cell.py`
- `python/spglib/error.py`
- `python/spglib/utils.py`
