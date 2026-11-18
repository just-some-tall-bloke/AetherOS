# AGENTS.md

## Before changing code
- ReactOS is a clean-room Windows NT-compatible OS. Never consult/use Microsoft Windows source; Wine/3rd-party code is synced (`media/doc/WINESYNC.txt`, `media/doc/3rd Party Files.txt`). Fix synced/upstream code upstream first and don't reformat it.
- Use real name/email in commits (aliases only for media/out-of-code docs).

## Build
- Use the RosBE toolchain/CMake (stock CMake warns and can break). Windows: run `configure.cmd` from RosBE or a VS 2019+ Developer prompt (INSTALL's VS 2010+ note is stale); Unix: `./configure.sh` (requires `ROS_ARCH`). From the repo root, configure creates/enters `output-<env>-<arch>` (e.g. `output-MinGW-i386`, `output-VS-amd64`); build there with `ninja`.
- Windows source paths must contain no spaces.
- CMake presets are an alternative: `cmake --preset mingw-i386-debug` (also `msvc-*`, `clang-*`, `vs2022-sln-*`), then `cmake --build output-MinGW-i386`. They still require the matching toolchain environment.
- Focused build: `ninja <CMake target>` (e.g. `ntoskrnl`, `kernel32`, `kernel32_apitest`, `calc`); group targets include `base/all`, `modules/rostests/all`. Source paths are not always targets; use `ninja -t targets`.
- CI smoke build is `cmake --build <build> -- -k0` then `cmake --build <build> --target bootcd`; `bootcd.iso` lands in the build dir. There is no separate lint/typecheck gate. INSTALL's `ReactOS.iso` name is stale.
- Tests are OFF by default: pass `-DENABLE_ROSTESTS=1` (CI also uses `-DENABLE_ROSAPPS=1`).

## Generated code / toolchain quirks
- Bison and Flex are required by configure. MSVC VS-solution builds also require `M4` and `BISON_PKGDATADIR` at configure time; they are saved into wrappers for VS rebuilds.
- Host tools (`native-*`: `spec2def`, `widl`, `bin2c`, `mkhive`, `cabman`, etc.) are built natively via ExternalProject; generated `.def`/headers/hives/CAB/ISO live in the build dir — edit sources, not outputs. `ninja xdk psdk` refreshes SDK header bundles when needed.
- Adding/removing ISO/CD extras or changing `boot/bootdata/packages/reactos.dff*` requires re-running CMake in the build dir (file lists are built at configure time).
- `DLL_EXPORT_VERSION` defaults to `0x502`; CI also builds `0x600`. Check both when changing API surface/exports.

## Tests
- Tests run inside booted ReactOS, not on the host. Build one with `ninja kernel32_apitest`; build `ninja bootcdregtest` for `bootcdregtest.iso`, whose `regtest.cmd` starts `rosautotest /r /s /n`. Compare results via Testman.
- Don't add tests to `modules/rostests/tests/` (legacy). Fixtures go in `modules/rostests/testdata/` and are copied to `%SystemRoot%\bin\testdata`.

## Style / commits
- C/C++: 100 columns, 4 spaces, Allman braces, PascalCase names, SPDX header, `#pragma once`, `NULL`/`TRUE`/`FALSE`; see `CODING_STYLE.md`. Don't reformat a whole file in a functional commit; use a separate `[FORMATTING]` commit.
- Format only ReactOS-owned C/C++ with `clang-format -style=file`. `sdk/tools/check_code_format.sh` currently references missing `sdk/tools/clang-format-diff.py`; don't rely on it.
- Follow `.gitmessage`: `[MODULE] imperative summary (#PR)`, WHY body, issue IDs at bottom (`git config commit.template .gitmessage`). Keep PRs focused; leave unrelated issues as TODO/JIRA instead of drive-by fixes.
- `CODEOWNERS` `M` is the primary maintainer: assign them and ask directly; don't request everyone listed as `R`.
