# ESP8266-MSYS2

Windows install instructions for ESP8266_RTOS_SDK (ESP-IDF style).

## Software

This document is based off of the instructions provided by Espressif [here](https://docs.espressif.com/projects/esp8266-rtos-sdk/en/latest/get-started/).

- Windows prerequisites
  - Download and install the latest version of [MSYS2](https://www.msys2.org/).
  - Download the [latest ESP8266 toolchain](https://dl.espressif.com/dl/xtensa-lx106-elf-gcc8_4_0-esp-2020r3-win32.zip) from Espressif. Extract this file and place the `xtensa-lx106-elf` subfolder in `C:\msys64\opt`.
  - Navigate to `Windows key + pause/break key` -> Advanced system settings -> Advanced -> Environmental Variables. Create a new system environmental variable with the name `IDF_PATH` and value `C:\msys64\home\USERNAME\esp\ESP8266_RTOS_SDK` (with `USERNAME` applicably replaced).
- Update MSYS2 MinGW 32-bit
  - Open MinGW 32-bit
  - `pacman -Syu`
  - Close and reopen MinGW 32-bit
  - `pacman -Syu` (again)
- Install dependencies
  - `pacman -S git base-devel gcc cmake mingw-w64-x86_64-toolchain make mingw-w64-x86_64-cmake python-pip mingw-w64-x86_64-python-cffi libffi-devel libcrypt-devel libcrypt openssl openssl-devel ncurses ncurses-devel winpty`
  - `python -m pip install --user -r $IDF_PATH/requirements.txt`
- Fix environment
  - `echo "export PATH=$PATH:/opt/xtensa-lx106-elf/bin" >> ~/.bashrc`
  - `echo "export MAKEFLAGS="-j" >> ~/.bashrc`
  - `source ~/.bashrc`
  - Open `C:\msys64\home\USERNAME\.local\lib\python3.8\site-packages\serial\tools\list_ports_posix.py` and edit `elif plat == 'cygwin'` to `elif plat == 'cygwin' or plat == 'msys'`
- Download SDK
  - `mkdir ~/esp; cd ~/esp`
  - `git clone --recursive https://github.com/espressif/ESP8266_RTOS_SDK.git`
- Start a project
  - `cp -r $IDF_PATH/examples/get-started/hello_world .; cd hello_world`
  - `make menuconfig`
  - Set Serial flasher config -> Default serial port to `/dev/ttyS#`, with # replaced by the COM port number minus one of the device as listed under Windows Device Manager (e.g. `COM8` -> `/dev/ttyS7`).
  - Configure other options as necessary and save.

  After this point the Eclipse IDE may be used to build and flash projects. Consult Espressif instructions [here](https://docs.espressif.com/projects/esp8266-rtos-sdk/en/latest/get-started/eclipse-setup.html) and [here](https://docs.espressif.com/projects/esp8266-rtos-sdk/en/latest/get-started/eclipse-setup-windows.html). Replace instances of `mingw32` with `mingw64` where applicable. Alternatively, a preconfigured template for Eclipse projects can be found [here](https://github.com/notabucketofspam/esp8266-eclipse-template).

## Additional notes

- If the install location for ESP8266_RTOS_SDK is modified, `IDF_PATH` must be subsequently updated to reflect this change. The same concept applies if MSYS2 is installed in an alternative location.
- In the event that a newer version of the ESP8266 toolchain is released and this document is not updated, the download link can be found in `ESP8266_RTOS_SDK\tools\tools.json`, on approximately line 50.
- Future changes with regards to either the version of Python distributed with MSYS2 or official support for MinGW 64-bit must be taken into account as well.
