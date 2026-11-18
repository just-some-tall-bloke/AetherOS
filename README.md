# AetherOS

AetherOS is a fork of [ReactOS](https://reactos.org/): a free and open-source operating system built for compatibility with applications and drivers written for the Microsoft® Windows™ NT family of operating systems (NT 4, 2000, XP, 2003, Vista, 7).

It is a clean-room implementation, not a wrapper around Linux and not a skin over Windows. Its user-mode is largely based on WINE, and the ReactOS and WINE teams have cooperated closely.

[![Build](https://github.com/just-some-tall-bloke/AetherOS/workflows/Build/badge.svg)](https://github.com/just-some-tall-bloke/AetherOS/actions) [![License: GPL-2.0](https://img.shields.io/badge/license-GNU_GPL_2.0-0688CB.svg)](COPYING)

### Product quality warning

**AetherOS inherits ReactOS's alpha quality.** Expect incomplete or broken functionality, and test in a virtual machine or on a machine with no sensitive or critical data.

## Quick links

[Source](https://github.com/just-some-tall-bloke/AetherOS) &bull;
[Upstream ReactOS](https://reactos.org/) &bull;
[Upstream wiki](https://reactos.org/wiki/) &bull;
[Upstream JIRA](https://jira.reactos.org/issues/) &bull;
[Testman](https://reactos.org/testman/)

## Building

Building is strongly advised with the _ReactOS Build Environment (RosBE)_. Up-to-date Windows and Unix/GNU-Linux versions are available from the upstream ["Build Environment"](https://reactos.org/wiki/Build_Environment) page.

Alternatively, Microsoft Visual C++ 2019+ can be used; see ["Visual Studio or Microsoft Visual C++"](https://reactos.org/wiki/CMake#Visual_Studio_or_Microsoft_Visual_C.2B.2B). The upstream ["Building ReactOS"](https://reactos.org/wiki/Building_ReactOS) article has further details, and the local [AGENTS.md](AGENTS.md) summarizes the toolchain and build commands used in this fork.

To build, run `configure.cmd` (Windows) or `configure.sh` (Unix) in a build directory, then `ninja <modulename>` or `ninja` for everything.

### Bootable images

From the build directory, run `ninja bootcd` to produce `bootcd.iso`. Fresh upstream binaries are available on the ["Daily builds"](https://reactos.org/getbuilds/) page.

## Installing

By default, AetherOS (like ReactOS) can only be installed on a machine with a FAT16 or FAT32 active (bootable) partition; the target partition must also be FAT16 or FAT32. Setup can format partitions if needed.

Since 0.4.10, installation on BtrFS is supported experimentally and may exhibit regressions not seen on FAT.

To install from the bootable CD distribution, extract the archive, burn the image, boot from it, and follow the instructions. See the upstream ["Installing ReactOS"](https://reactos.org/wiki/Installing_ReactOS) wiki page or the local [INSTALL](INSTALL) file for more details.

## Testing

If you find an AetherOS-specific bug, please open an issue in [this repository](https://github.com/just-some-tall-bloke/AetherOS/issues), with logs and as much detail as possible. For bugs inherited from upstream, search the [ReactOS JIRA](https://jira.reactos.org/issues/) first — they may already be reported. See upstream's ["File Bugs"](https://reactos.org/wiki/File_Bugs) guide.

Issue trackers are for bugs, not discussions; use the [upstream chat](https://chat.reactos.org/) or [forum](https://reactos.org/forum/) for discussion.

## Contributing

We are always looking for developers! See [CONTRIBUTING.md](CONTRIBUTING.md) for how to contribute.

__Legal notice__: If you have seen proprietary Microsoft Windows source code (including but not limited to the leaked Windows NT 3.5, NT 4, 2000 source code and the Windows Research Kernel), your contribution cannot be accepted because of potential copyright violation.

## Upstream and credits

AetherOS is derived from ReactOS, which is maintained by the [ReactOS project](https://reactos.org/). Upstream development happens on [GitHub](https://github.com/reactos/reactos), with an [alternative mirror](https://git.reactos.org/?p=reactos.git) and an obsolete [SVN archive](https://svn.reactos.org/reactos/) kept for historical purposes.

Upstream active developers are listed in the [GitHub organization](https://github.com/orgs/reactos/people). See [CREDITS](CREDITS) for the full list of contributors.

Cloud-based development is available through [Gitpod](https://gitpod.io/#https://github.com/just-some-tall-bloke/AetherOS).

Also see the [media/doc](/media/doc/) subdirectory for sparse additional notes.
