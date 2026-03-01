# spglib source map: Developer Guide

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
- `architecture`
- `database`
- `test`
- `magnetic`
- `performance`
- `wrapper`
- `binding`

## Fast source navigation
- `rg -n "spg_get_|spgms_|spgat_|SPG_API_TEST" src include test`
- `rg -n "magnetic|msg" src database/msg python/spglib`

## Function-level behavior checks
- Core public API call chain:
  `rg -n "spg_get_dataset|spgat_get_dataset|spgms_get_magnetic_dataset|spg_standardize_cell" include/spglib.h src/spglib.c`
- Magnetic identification flow:
  `rg -n "msg_identify_magnetic_space_group_type|msgdb_get_magnetic_spacegroup_type" src/magnetic_spacegroup.c src/msg_database.c`
- Test exposure and layering:
  `rg -n "SPG_API_TEST|add_subdirectory\\(example|add_subdirectory\\(package" test/CMakeLists.txt`
- Validation checkpoint: symbols touched by a change are covered by at least one targeted `ctest` label path and, when relevant, a Python wrapper call site.

## Suggested source entry points
- `src/spglib.c` | public C API dispatch and compatibility logic
- `src/symmetry.c` | core symmetry search internals
- `src/spacegroup.c` | space-group matching pipeline
- `src/magnetic_spacegroup.c` | magnetic space-group core logic
- `src/msg_database.c` | magnetic database lookup integration
- `include/spglib.h` | public contract and deprecations
- `python/spglib/spg.py` | Python API behavior layer
- `python/spglib/msg.py` | Python magnetic behavior layer
- `test/CMakeLists.txt` | test-layer orchestration
- `database/make_spgtype_db.py` | space-group database generation script
- `database/msg/make_msgtype_db.py` | MSG type table generation
- `database/msg/make_mhall_db.py` | magnetic Hall database generation
