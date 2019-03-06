# ccminer

Based on Christian Buchner's &amp; Christian H.'s CUDA project, no more active on github since 2014.

Check the [README.txt](README.txt) for the additions

BTC donation address: 1AJdfCpLWPNoAMDfHF1wD5y8VgKSSTHxPo (tpruvot)

A part of the recent algos were originally written by [djm34](https://github.com/djm34) and [alexis78](https://github.com/alexis78)

This variant was tested and built on Linux (ubuntu server 14.04, 16.04, Fedora 22 to 25)
It is also built for Windows 7 to 10 with VStudio 2013, to stay compatible with Windows 7 and Vista.

Note that the x86 releases are generally faster than x64 ones on Windows, but that tend to change with the recent drivers.

The recommended CUDA Toolkit version was the [6.5.19](http://developer.download.nvidia.com/compute/cuda/6_5/rel/installers/cuda_6.5.19_windows_general_64.exe), but some light algos could be faster with the version 7.5 and 8.0 (like lbry, decred and skein).

About source code dependencies
------------------------------

This project requires some libraries to be built :

- OpenSSL (prebuilt for win)
- Curl (prebuilt for win)
- pthreads (prebuilt for win)

The tree now contains recent prebuilt openssl and curl .lib for both x86 and x64 platforms (windows).

To rebuild them, you need to clone this repository and its submodules :
    git clone https://github.com/JCMais/curl-for-windows.git compat/curl-for-windows


Compile on Linux
----------------

Please see [INSTALL](https://github.com/tpruvot/ccminer/blob/linux/INSTALL) file or [project Wiki](https://github.com/tpruvot/ccminer/wiki/Compatibility)



Build Errors
----------------
1. internal error with "inflate.c" in zlib

When build for Windows 10 (x64) with Visual Studio 2017 Community for release only, I got "fatal error C1001: An internal error has occurred in the compiler" when it was trying to generate code for "inflate.c" in zlib. The error occured on line 625, which is the starting bracket ("{") for "int ZEXPORT inflate(strm, flush)" definition. The "Debug" version build without such error thought. It seems to be something wrong with the zlib built (zlib.lib), however, the reason hasn't been found.

The workaround solution would be to use the version in a NuGet package. There are "zlib-msvc14-x86" or "zlib-msvc14-x64" which are compatible with both VS 2015 Update 3 and VS 2017:
- zlib-msvc14-x86	https://www.nuget.org/packages/zlib-msvc14-x86/ 
- zlib-msvc14-x64	https://www.nuget.org/packages/zlib-msvc14-x64/

Extract (e.g. using 7zip) the static library in the NuGet package and replace the "zlib.lib" file will probably solved the issue.
