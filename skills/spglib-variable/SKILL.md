---
name: spglib-variable
description: Use this skill for variable-level semantics, tolerance controls, and C/Python convention differences in spglib inputs and outputs.
---

# spglib: Variable

## High-Signal Playbook

### Route conditions
- Use `spglib-inputs-and-modeling` for broader modeling workflow decisions.
- Use `spglib-api-and-scripting` for function selection and language-binding behavior.
- Use `spglib-advanced-topics` for deep dataset-field reference details.

### Triage questions
- Is the user in C/Fortran or Python?
- Do they mean input cell variables or returned dataset variables?
- Are they using magnetic variables (`magmoms`, `mag_symprec`) or non-magnetic only?
- Is `angle_tolerance` explicitly needed, or should default optimized behavior be kept?
- Are they confusing transformation matrix with rotation matrix semantics?

### Canonical workflow
1. Normalize variable definitions from `docs/variable.md` (`lattice`, `position`, `types`, symmetry outputs).
2. Confirm language-specific orientation differences (`docs/python-interface.md`, `python/spglib/utils.py`).
3. Pick tolerance family: `symprec` always; add `angle_tolerance`/`mag_symprec` only when needed.
4. Select matching API family (`spg_*`, `spgat_*`, `spgms_*`) consistent with tolerance intent (`docs/api.md`, `include/spglib.h`).
5. Validate output arrays (`rotations`, `translations`, `equivalent_atoms`) against expected shapes and counts.

### Minimal working example
```c
double lattice[3][3] = {{ax,bx,cx},{ay,by,cy},{az,bz,cz}};
double position[][3] = {{x1,y1,z1}, {x2,y2,z2}}; /* fractional */
int types[] = {1, 1};
SpglibDataset *d = spg_get_dataset(lattice, position, types, 2, 1e-5);
/* ... inspect d->rotations, d->translations ... */
spg_free_dataset(d);
```

### Pitfalls and fixes
- Supplying Cartesian positions instead of fractional coordinates breaks interpretation (`docs/variable.md`, `docs/definition.md`).
- Python lattice is row-wise while C docs describe column-vector form; convert intentionally (`docs/python-interface.md`, `docs/variable.md`).
- `angle_tolerance` is only used by `spgat_*`/related paths, not by default APIs (`docs/variable.md`, `include/spglib.h`).
- Negative `mag_symprec` reuses `symprec`; explicit value is needed when moment noise scale differs (`docs/variable.md`, `python/spglib/msg.py`).
- Deprecated magnetic paths can mislead expectations; prefer current APIs from releases notes (`docs/releases.md`).

### Convergence and validation checks
- `positions` and `types` lengths match exactly.
- All fractional coordinates are normalized (or intentionally wrapped) in `[0, 1)`.
- Symmetry operation arrays have consistent paired lengths.
- Small tolerance sweeps do not flip classification unexpectedly for clean structures.

## Scope
- Variable semantics and tolerance controls used across C/Python interfaces.

## Primary documentation references
- `docs/variable.md`
- `docs/definition.md`
- `docs/python-interface.md`
- `docs/api.md`
- `docs/releases.md`

## Workflow
- Start from primary references.
- Use `references/doc_map.md` when chasing related field definitions.
- Use `references/source_map.md` for implementation specifics.
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
- `src/symmetry.c`
- `python/spglib/utils.py`
- `python/spglib/spg.py`
- `python/spglib/msg.py`
