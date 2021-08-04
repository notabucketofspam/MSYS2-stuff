# MSYS2-stuff

Solutions for Unix things that aren't intended to work on Windows.

All projects tested on Windows 10 (build 2004).

## Prerequisites

- Download and install the latest version of [MSYS2](https://www.msys2.org/).
  - Note: if MinGW 64-bit doesn't show up in the start menu, it can be run with `Windows key + r` -> `C:\msys64\msys2_shell.cmd -mingw64`
- Update MSYS2
  - Open MinGW 64-bit.
  - `pacman -Syyu && exit`
  - Reopen MinGW 64-bit.
  - `pacman -Syu` (again)
- Install basic build tools
  - `pacman -S  base-devel msys2-devel mingw-w64-x86_64-toolchain sys-utils git`
- Fix environment
  - `echo "export MAKEFLAGS="-j" >> ~/.bashrc && source ~/.bashrc`
