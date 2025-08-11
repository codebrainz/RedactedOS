# Building RedactedOS on Ubuntu 24.04

This guide explains how to build RedactedOS on Ubuntu 24.04 using the official ARM GNU toolchain.

## Prerequisites

- Ubuntu 24.04 (or similar)
- Internet connection
- Basic build tools: `make`, `gcc`, `g++`, `tar`, `xz`, `git`

## 1. Get the Source Code

Clone the RedactedOS repository:

```
git clone https://github.com/differrari/RedactedOS.git
cd RedactedOS
```

## 2. Install Required Packages

Open a terminal and run:

```
sudo apt update
sudo apt install build-essential wget tar xz-utils git qemu-system-aarch64
```

## 3. Download and Extract the ARM Toolchain

Download the official ARM GNU toolchain (aarch64-none-elf):

```
wget https://developer.arm.com/-/media/Files/downloads/gnu/14.3.rel1/binrel/arm-gnu-toolchain-14.3.rel1-x86_64-aarch64-none-elf.tar.xz
```

Extract the toolchain:

```
tar xf arm-gnu-toolchain-14.3.rel1-x86_64-aarch64-none-elf.tar.xz
```

## 4. Add the Toolchain to Your PATH

Assuming you extracted to your home directory:

```
export PATH="$HOME/arm-gnu-toolchain-14.3.Rel1-x86_64-aarch64-none-elf/bin:$PATH"
```

To make this change permanent, add the above line to your `~/.bashrc` or `~/.zshrc`.

## 5. Build the Project

From the project root directory, run:

```
make all
```

This will build the kernel and filesystem images required to run RedactedOS.

## 6. Run the Project in QEMU

You can simply run:

```
make run
```

This will build the project (if needed) and launch RedactedOS in QEMU using the default configuration for the virt board.

## 7. Other Useful Commands

- `make all` — Build the OS
- `make clean` — Remove all build artifacts
- `make raspi` — Build for Raspberry Pi
- `make virt` — Build for QEMU virt board
- `make run` — Build and run in virt mode
- `make debug` — Build and run with debugger
- `make dump` — Disassemble kernel.elf
- `make install` — Create Raspberry Pi kernel and mount it on a bootable partition
- `make prepare-fs` — Create directories for the filesystem

## Notes

- The default toolchain prefix is `aarch64-none-elf-`. If you installed the toolchain elsewhere, adjust your `PATH` accordingly.
- QEMU is required for emulation. Install it with `sudo apt install qemu-system-aarch64` if you want to use `make run`.
- For Raspberry Pi deployment, see the `install` target in the Makefile.

---

_Disclaimer: This document was largely written by a Clanker, guided by a sympathizer._
