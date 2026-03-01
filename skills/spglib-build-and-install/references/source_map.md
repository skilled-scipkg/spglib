# spglib source map: Build and Install

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
- `cmake`
- `install`
- `find_package`
- `pkg-config`
- `fortran`
- `python`
- `SPGLIB_WITH_`
- `SPGLIB_USE_OMP`
- `SPGLIB_WITH_TESTS`

## Fast source navigation
- `rg -n "SPGLIB_WITH_|SPGLIB_USE_OMP|install|find_package|pkg" CMakeLists.txt cmake fortran python test`
- `rg -n "Spglib::symspg|Spglib::fortran|spglib_f08|spglib.pc" cmake fortran test example`

## Function-level behavior checks
- Build-option definitions:
  `rg -n "option\\(SPGLIB_WITH_|SPGLIB_USE_OMP|SPGLIB_WITH_TESTS" CMakeLists.txt test/CMakeLists.txt`
- Install/export pipeline:
  `rg -n "install\\(|export\\(|SpglibConfig|pkg-config|spglib\\.pc" CMakeLists.txt cmake/SpglibConfig.cmake.in cmake/spglib.pc.in`
- Interface target wiring:
  `rg -n "Spglib::symspg|Spglib::fortran|spglib_f08" cmake/README.md fortran/CMakeLists.txt test/example`
- Validation checkpoint: enabled options in top-level CMake propagate into generated package metadata and expected imported targets.

## Suggested source entry points
- `CMakeLists.txt` | top-level options and install/export logic
- `cmake/README.md` | CMake usage contract and exported targets
- `cmake/SpglibConfig.cmake.in` | installed package config behavior
- `cmake/spglib.pc.in` | C pkg-config metadata
- `fortran/CMakeLists.txt` | Fortran target build/install and module paths
- `fortran/spglib_f08.pc.in` | Fortran pkg-config metadata
- `python/CMakeLists.txt` | CMake-controlled python build path
- `pyproject.toml` | scikit-build-core defaults and Python requirements
- `test/CMakeLists.txt` | test build toggles, sanitizer/coverage knobs
