# XMRig Compile Guide for AMD

[![Github All Releases](https://img.shields.io/github/downloads/xmrig/xmrig/total.svg)](https://github.com/xmrig/xmrig/releases)
[![GitHub release](https://img.shields.io/github/release/xmrig/xmrig/all.svg)](https://github.com/xmrig/xmrig/releases)
[![GitHub Release Date](https://img.shields.io/github/release-date/xmrig/xmrig.svg)](https://github.com/xmrig/xmrig/releases)
[![GitHub license](https://img.shields.io/github/license/xmrig/xmrig.svg)](https://github.com/xmrig/xmrig/blob/master/LICENSE)
[![GitHub stars](https://img.shields.io/github/stars/xmrig/xmrig.svg)](https://github.com/xmrig/xmrig/stargazers)
[![GitHub forks](https://img.shields.io/github/forks/xmrig/xmrig.svg)](https://github.com/xmrig/xmrig/network)

This is a compile guide for optimized AMD builds. 
XMRig is a high performance, open source, cross platform RandomX, KawPow, CryptoNight and AstroBWT unified CPU/GPU miner and [RandomX benchmark](https://xmrig.com/benchmark).

Feedback and mining discussion: https://discord.gg/5xqtAFMu4R

# Build XMRig
Download and install the AMD compiler:

Go to https://developer.amd.com/amd-aocc/ and install the AMD optimized clang version.

Download aocc-compiler-<version>.tar to the directory of your choice, say <compdir>
Installation with tar file does not require root or sudo permission.

		$ cd <compdir>
		$ tar -xvf aocc-compiler-<version>.tar
		$ cd aocc-compiler-<version>
		$ bash install.sh
This will install the compiler and display the AOCC setup instructions.

		$ source <compdir>/setenv_AOCC.sh
This will set up a shell environment for using AOCC C, C++, and Fortran compilers in the shell environment,
where the above command was executed.

Download and install the XMrig dependencies:

           $ sudo apt-get install git build-essential cmake automake libtool autoconf
           $ git clone https://github.com/xmrig/xmrig.git
           $ mkdir xmrig/build && cd xmrig/scripts
           $ ./build_deps.sh && cd ../build

Build XMRig with following CMake settings (use your path to the compiler). If your shell environment setup is correct, you just can write clang and
clang++ :
```
       $ cmake .. -D CMAKE_C_COMPILER=/home/ubuntu/Downloads/aocc-compiler-3.2.0/bin/clang -D CMAKE_CXX_COMPILER=/home/Ubuntu/Downloads/aocc-compiler-3.2.0/bin/clang++ -DXMRIG_DEPS=scripts/deps
```
```
       $ make -j$(nproc)
```
  
You can bech your build with: 
```
       $ sudo ./xmrig --bench=1M --submit
```   
  
You can put   
```
SET (CMAKE_CXX_FLAGS "-O3")
SET (CMAKE_C_FLAGS "-O3") 
```  
or  
```  
SET (CMAKE_CXX_FLAGS "-Ofast")
SET (CMAKE_C_FLAGS "-Ofast")
```  
in your cmake file for more optimizations.  
  
