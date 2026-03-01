# spglib source map: Inputs and Modeling

Generated from source roots:
- `cmake`
- `database`
- `fortran`
- `include`
- `python`
- `ruby`
- `src`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Topic query tokens
- `lattice`
- `position`
- `types`
- `symprec`
- `angle_tolerance`
- `mag_symprec`
- `transformation_matrix`
- `origin_shift`

## Fast source navigation
- `rg -n "symprec|angle_tolerance|mag_symprec|standardize|primitive" include/spglib.h src/spglib.c python/spglib`
- `rg -n "_expand_cell|TypeError|SpglibError|lattice" python/spglib/utils.py python/spglib/cell.py`

## Function-level behavior checks
- Tolerance-bearing C entry points:
  `rg -n "spg_get_dataset|spgat_get_dataset|spg_get_magnetic_dataset|spgms_get_magnetic_dataset|symprec|angle_tolerance|mag_symprec" include/spglib.h src/spglib.c`
- Python cell-shape and conversion path:
  `rg -n "_expand_cell|standardize_cell|refine_cell|find_primitive" python/spglib/utils.py python/spglib/cell.py`
- Basis/change-of-basis helpers:
  `rg -n "transformation|change_of_basis|origin_shift" docs/definition.md database/change_of_basis.py`
- Validation checkpoint: input-shape guards and tolerance parameters are aligned between docs, Python prechecks, and C API signatures.

## Suggested source entry points
- `include/spglib.h` | C variable conventions and API signatures
- `src/spglib.c` | tolerance plumbing and standardization entry points
- `src/cell.c` | core cell manipulation routines
- `src/refinement.c` | refinement and standardized-cell internals
- `src/symmetry.c` | symmetry-search implementation details
- `python/spglib/utils.py` | Python cell-shape/type validation and conversion
- `python/spglib/cell.py` | Python wrappers for primitive/refine/standardize
- `database/change_of_basis.py` | explicit basis-change helpers used in db tooling
