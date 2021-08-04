# Redis

Steps to build a mostly-functioning Redis server on Windows.

## Method

Note: this project uses MinGW 64-bit

- Install dependencies
  - `pacman -S tcl`
- Create build directory
  - `mkdir ~/redis && cd ~/redis`
- Download dlfcn-win32
  - `git clone https://github.com/dlfcn-win32/dlfcn-win32.git`
  - Note: there's an MSYS2 package available for this repository (`mingw64/mingw-w64-x86_64-dlfcn`), however `make` doesn't seem to acknowledge it when compiling.
- Download Redis
  - `wget https://github.com/redis/redis/archive/unstable.tar.gz && cd redis-unstable`
  - The unstable branch is used because, at the time of writing (2021-08-04), Redis version 6.2.5 fails to build.
- Build and test
  - `make CFLAGS="-I $(realpath ../dlfcn-win32/src)"`
  - `make test`
  - If either step fails, run `make distclean` and start over; this may take a few tries.
  - Any errors raised by `make test` can (probably) be ignored.

## Notes

- To be honest, this entire process is redundant at best. It's significantly easier to install Windows Subsystem for Linux (WSL) and download Ubuntu from the Microsoft Store, then follow the directions [here](https://redis.io/download#from-the-official-ubuntu-ppa). Use this method only in an environment where WSL is unavailable, but MSYS2 is.
