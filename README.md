# A proprietary free SCuM SDK

[![CI][ci-badge]][ci-link]
[![License][license-badge]][license-link]

This repository is an attempt to provide a proprietary free support for the
SCuM chip.
Most of the drivers (UART, Radio, Timer, SPI) are taken from the
[scum-test-code](https://github.com/PisterLab/scum-test-code) repository.

### Requirements

So far this repository has only been tested on Linux.

What is needed to build a firmware for SCuM:
- [CMake](https://cmake.org/)
- [Ninja](https://ninja-build.org/)
- [GNU ARM Embedded toolchain](https://developer.arm.com/downloads/-/arm-gnu-toolchain-downloads)

Make sure that the ARM toolchain GCC program is available in your PATH.

### Get the code

Use Git:
```
git clone https://github.com/aabadie/scum-sdk.git
```

### Usage

So far, only the original `hello_world` example application is available. To
build this application, from the repository base directory, simply run
(for Windows users adapt the path separators to "\"):

```
cmake -S samples/hello_world -B samples/hello_world/build -GNinja -DCMAKE_BUILD_TYPE=MinSizeRel
ninja -C samples/hello_world/build
```

The generated firmwares (elf, hex, bin) are located in the `samples/hello_world/build` directory.

### Load the firmware on SCuM

Once the SCuM chip is properly connected to an nRF52840-DK programmer, use the
SCuM programmer script available at https://github.com/aabadie/SCuM-programmer/tree/develop_12_refactor.

The build system proposes a `load` target to automatically call the SCuM programmer
script.
If not found automatically by CMake, the path to the programmer script can be set
manually using CMake:

```
cmake -DSCUM_PROGRAMMER=path/to/programmer.py samples/hello_world/build/
```

Then the programmer can be called using:

```
ninja -C samples/hello_world/build load
```

[ci-badge]: https://github.com/aabadie/scum-sdk/workflows/CI/badge.svg
[ci-link]: https://github.com/aabadie/scum-sdk/actions?query=workflow%3ACI+branch%3Amain
[license-badge]: https://img.shields.io/github/license/aabadie/scum-sdk
[license-link]: https://github.com/aabadie/scum-sdk/blob/main/LICENSE.txt
