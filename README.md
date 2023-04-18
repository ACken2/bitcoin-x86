32-BIT WINDOWS BUILD NOTES
====================

Below are some notes on how to build Bitcoin Core for Windows 32-bit OS.

The only tested and known to work for building Bitcoin Core on this branch is Ubuntu 22 on VirtualBox 
using the Mingw cross compiler tool chain.

WARNING
====================

**I AM NOT A BITCOIN DEV. I HAVE MADE SOME CHANGES TO THE CODE BASE TO MAKE THE COMPILATION WORK ON MY SETUP.  
THE SOFTWARE IS PROVIDED “AS IS”, WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, 
INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.**

Cross-compilation for Ubuntu
====================

The steps below can be performed on Ubuntu or WSL. The depends system
may also work on other Linux distributions, however the commands for
installing the toolchain will be different.

First, install the general dependencies:

    sudo apt update
    sudo apt upgrade
    sudo apt install build-essential libtool autotools-dev automake pkg-config bsdmainutils curl git nsis

## Building for 32-bit Windows

The first step is to install the mingw-i686 cross-compilation tool chain:

```sh
sudo apt install g++-mingw-w64-i686-posix
```

Acquire the source in the usual way:

    git clone https://github.com/ACken2/bitcoin-x86.git
    cd bitcoin-x86
    git checkout 24.0.1

Then build using:

    cd depends
    make HOST=i686-w64-mingw32
    cd ..
    ./autogen.sh
    CONFIG_SITE=$PWD/depends/i686-w64-mingw32/share/config.site ./configure --prefix=/
    make
    make deploy

Installation
-------------

After building, the compiled .EXE files should be present within the /release folder. 
Copy all compiled .EXE files into a 32-bit Windows system, and then run bitcoin-qt.exe.