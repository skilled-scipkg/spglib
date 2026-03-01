# spglib source map: API and Scripting

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
- `spg_get_dataset`
- `spg_get_error_code`
- `spg_get_error_message`
- `spg_get_magnetic_dataset`
- `get_symmetry_dataset`
- `get_magnetic_symmetry_dataset`
- `SpglibDataset`
- `SpglibMagneticDataset`

## Fast source navigation
- `rg -n "spg_get_dataset|spg_get_error|spg_get_magnetic_dataset|spg_standardize_cell" include/spglib.h src/spglib.c`
- `rg -n "def get_symmetry|def get_magnetic_symmetry|def standardize_cell|SpglibError" python/spglib`

## Function-level behavior checks
- C API signatures and ownership:
  `rg -n "spg_get_dataset|spgat_get_dataset|spg_get_magnetic_dataset|spg_free_dataset|spg_free_magnetic_dataset" include/spglib.h src/spglib.c`
- Python wrappers and binding boundary:
  `rg -n "def get_symmetry_dataset|def get_magnetic_symmetry_dataset|_spglib\\." python/spglib/spg.py python/spglib/msg.py`
- Error propagation path:
  `rg -n "spg_get_error_code|spg_get_error_message|SpglibError" include/spglib.h src/spglib.c python/spglib/error.py`
- Validation checkpoint: function families match across header declarations, C implementation, and Python wrappers.

## Suggested source entry points
- `include/spglib.h` | canonical C API signatures and struct definitions
- `src/spglib.c` | C API implementation and error code plumbing
- `src/spglib_f.c` | Fortran-facing C wrapper implementation
- `python/_spglib.cpp` | pybind/c-extension boundary
- `python/py_bindings.cpp` | python binding glue logic
- `python/spglib/spg.py` | non-magnetic Python API behavior
- `python/spglib/msg.py` | magnetic Python API behavior
- `python/spglib/cell.py` | standardization/primitive helpers
- `python/spglib/error.py` | exception model and compatibility toggles
- `python/spglib/utils.py` | cell expansion and input validation
