# spglib source map: Variable

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
- `rotation`
- `translation`
- `symprec`
- `angle_tolerance`
- `mag_symprec`

## Fast source navigation
- `rg -n "symprec|angle_tolerance|mag_symprec|rotation|translation" include/spglib.h src/spglib.c python/spglib`

## Function-level behavior checks
- Variable/tolerance API variants:
  `rg -n "spg_get_dataset|spgat_get_dataset|spg_get_magnetic_dataset|spgms_get_magnetic_dataset|symprec|angle_tolerance|mag_symprec" include/spglib.h src/spglib.c`
- Python variable normalization path:
  `rg -n "_expand_cell|get_symmetry_dataset|get_magnetic_symmetry_dataset" python/spglib/utils.py python/spglib/spg.py python/spglib/msg.py`
- Symmetry operation container semantics:
  `rg -n "rotations|translations|equivalent_atoms" docs/variable.md include/spglib.h`
- Validation checkpoint: variable names and array-shape assumptions are consistent across docs, header structs, and wrapper usage.

## Suggested source entry points
- `include/spglib.h` | variable conventions, structs, and tolerance-bearing APIs
- `src/spglib.c` | runtime handling of tolerance variants and API wrappers
- `src/symmetry.c` | symmetry operation representation details
- `python/spglib/utils.py` | Python cell/shape validation and conversion
- `python/spglib/spg.py` | Python symmetry API variable handling
- `python/spglib/msg.py` | Python magnetic variable handling
