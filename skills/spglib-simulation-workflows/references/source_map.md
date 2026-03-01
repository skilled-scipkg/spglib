# spglib source map: Simulation Workflows

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
- `example`
- `dataset`
- `wyckoff`
- `equivalent_atoms`
- `symprec`

## Fast source navigation
- `rg -n "get_symmetry_dataset|spg_get_dataset|wyckoff|equivalent" test/example example python/spglib src include`

## Function-level behavior checks
- Example APIs and cleanup path:
  `rg -n "spg_get_dataset|get_symmetry_dataset|spg_free_dataset" test/example/c_api/example.c test/example/fortran_api/example.F90 test/example/python_api/example.py`
- Dataset field flow from API to output:
  `rg -n "wyckoff|equivalent_atoms|n_operations|international" include/spglib.h python/spglib/spg.py test/example`
- Build/run linkage for examples:
  `rg -n "find_package\\(Spglib|target_link_libraries|add_executable" test/example/c_api/CMakeLists.txt test/example/fortran_api/CMakeLists.txt`
- Validation checkpoint: example outputs expose stable dataset identifiers and the same API family is visible in docs and source call sites.

## Suggested source entry points
- `test/example/c_api/example.c` | C baseline runnable case
- `test/example/python_api/example.py` | Python baseline runnable case
- `test/example/fortran_api/example.F90` | Fortran baseline runnable case
- `test/example/c_api/CMakeLists.txt` | C example build wiring
- `test/example/fortran_api/CMakeLists.txt` | Fortran example build wiring
- `python/spglib/spg.py` | Python dataset API behavior
- `include/spglib.h` | C dataset struct/function definitions
- `src/spglib.c` | C dataset generation implementation
