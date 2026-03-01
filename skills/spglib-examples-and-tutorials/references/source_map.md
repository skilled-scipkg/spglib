# spglib source map: Examples and Tutorials

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
- `symmetry`

## Fast source navigation
- `rg -n "get_symmetry_dataset|spg_get_dataset|example" example test/example python/spglib src include`

## Function-level behavior checks
- Example call sites by language:
  `rg -n "spg_get_dataset|get_symmetry_dataset" test/example/c_api/example.c test/example/fortran_api/example.F90 test/example/python_api/example.py`
- Dataset fields used in examples:
  `rg -n "equivalent_atoms|international|spacegroup|hall" test/example/c_api/example.c test/example/python_api/example.py`
- Build wiring for runnable binaries:
  `rg -n "add_executable|target_link_libraries|find_package\\(Spglib" test/example/c_api/CMakeLists.txt test/example/fortran_api/CMakeLists.txt`
- Validation checkpoint: each example calls a documented dataset API and prints at least one stable symmetry-identifying field.

## Suggested source entry points
- `test/example/c_api/example.c`
- `test/example/python_api/example.py`
- `test/example/fortran_api/example.F90`
- `test/example/c_api/CMakeLists.txt`
- `test/example/fortran_api/CMakeLists.txt`
- `python/spglib/spg.py`
- `include/spglib.h`
