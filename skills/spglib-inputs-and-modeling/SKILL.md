---
name: spglib-inputs-and-modeling
description: Use this skill for cell/tolerance conventions, coordinate transforms, and input-shape validation for spglib calls.
---

# spglib: Inputs and Modeling

## High-Signal Playbook

### Route conditions
- Use `spglib-api-and-scripting` when choosing exact API functions and return structures.
- Use `spglib-build-and-install` for compiler/environment issues.
- Use `spglib-variable` for terse variable-only reminders.

### Triage questions
- C/Fortran arrays or Python tuple input?
- Are atomic positions fractional (not Cartesian)?
- Are lattice vectors oriented correctly for the chosen API?
- Are `positions`, `types`, and optional `magmoms` lengths consistent?
- Is this magnetic (`magmoms`) or non-magnetic?
- Are tolerances (`symprec`, `angle_tolerance`, `mag_symprec`) physically reasonable for distortion scale?

### Canonical workflow
1. Build a valid cell object with documented orientation conventions (`docs/variable.md`, `docs/python-interface.md`, `docs/definition.md`).
2. Start with default `symprec=1e-5`; keep `angle_tolerance<0` unless debugging difficult cases (`docs/variable.md`, `python/spglib/msg.py`).
3. Run `get_symmetry_dataset`/`spg_get_dataset` as baseline classification.
4. If needed, standardize/refine/primitive transforms via API shorthands (`docs/api.md`, `python/spglib/cell.py`).
5. For magnetic cells, set `mag_symprec` and validate `is_axial`/`with_time_reversal` assumptions (`docs/development/magnetic_symmetry_flags.md`, `python/spglib/msg.py`).
6. Cross-check transformation-matrix vs rotation semantics (`docs/definition.md`).

### Minimal working example
```python
import spglib

cell = (
    [[3.111, 0, 0], [-1.5555, 2.6942050311733885, 0], [0, 0, 4.988]],
    [[1/3, 2/3, 0.0], [2/3, 1/3, 0.5], [1/3, 2/3, 0.6181], [2/3, 1/3, 0.1181]],
    [1, 1, 2, 2],
)

dset = spglib.get_symmetry_dataset(cell, symprec=1e-5)
print(dset.number, dset.international)
```

### Pitfalls and fixes
- C `lattice` uses column-vector convention; Python input lattice is row-wise (`docs/variable.md`, `docs/python-interface.md`).
- `positions` must be fractional; Cartesian coordinates silently yield wrong symmetry interpretation (`docs/variable.md`, `docs/definition.md`).
- `numbers` length must match atom count; Python will raise validation errors (`python/spglib/utils.py`).
- Overly tight `symprec` causes false failures; loosen progressively with explicit logging (`docs/variable.md`, `python/spglib/error.py`).
- `angle_tolerance` behavior differs from default optimized routine; keep negative unless justified (`docs/variable.md`).

### Convergence and validation checks
- Space-group identification is stable over a small tolerance window.
- `equivalent_atoms` partitions match chemical intuition for symmetrically identical sites.
- `transformation_matrix`/`origin_shift` produce consistent standardized cell mapping (`docs/dataset.md`, `docs/definition.md`).
- Magnetic and non-magnetic outputs differ only where expected when toggling magnetic options.

## Scope
- Inputs, system setup, conventions, and physically meaningful tolerance choices.

## Primary documentation references
- `docs/variable.md`
- `docs/definition.md`
- `docs/python-interface.md`
- `docs/api.md`
- `docs/releases.md`
- `docs/development/magnetic_symmetry_flags.md`
- `docs/references.md`

## Workflow
- Start from primary references.
- Use `references/doc_map.md` for full topic inventory.
- Use `references/source_map.md` for implementation-level ambiguity.
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
- `src/cell.c`
- `src/symmetry.c`
- `src/refinement.c`
- `python/spglib/utils.py`
- `python/spglib/cell.py`
- `database/change_of_basis.py`
