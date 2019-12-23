## Introduction

This is a standalone integration of v8-inspector with chrome-devtools front end, to debug any standalone java script code.

This code is inspired (read as copied and ripped apart) from node.js and v8 code base.

This was mainly done to enable debugging of [couchbase eventing functions](https://github.com/couchbase/eventing/tree/master/third_party/inspector)

## Library Dependencies
This project depends on following libraries
* V8 5.9
* ICU 59
* libuv 1.8
* libz
* libcrypto

## Build Instructions
```shell
$ mkdir build && cd build
$ cmake ..
$ make
# To run the binary
$ ./inspector ../sample.js
```

## 3rd Partdy Dependencies / Windows libraries:
libuv
download from https://dist.libuv.org/dist/v1.10.0/
rename to .zip and unpack at google_v8\v8Inspector\libuv_1_10\x86\
includes prebuild binaries

icu
Download from https://github.com/unicode-org/icu/releases/tag/release-59-2
Install at v8Inspector\icu
Includes a Visual Studio Solution at google_v8\v8Inspector\icu\source\allinone\allinone.sln
This required installing some updates for VC2017. 

lz4
Download project from https://github.com/lz4/lz4
Unpack at v8Inspector\lz4-dev
Includes a VC2017 solution at google_v8\v8Inspector\lz4-dev\visual\VS2017\lz4.sln

openssl
Donload binary distribution at https://kb.firedaemon.com/support/solutions/articles/4000121705
Unpack to google_v8\v8Inspector\openssl

zlib
Download from https://www.nuget.org/packages/zlib128-vc140-static-32_64/
Rename to zip and Unpack at google_v8\v8Inspector\zlib\

v8 libraries
Download prebuild from 
https://www.nuget.org/packages/v8-v140-x64/7.1.302.4
https://www.nuget.org/packages/v8.redist-v140-x86/7.1.302.4
and unpack to google_v8 dir


Your directory Structure should now look like this:
google_v8\v8-v141-x64.7.1.302.4
google_v8\v8-v141-x86.7.1.302.4
google_v8\v8Inspector\icu
google_v8\v8Inspector\libuv_1_10
google_v8\v8Inspector\lz4-dev
google_v8\v8Inspector\openssl
google_v8\v8Inspector\v8inspector
google_v8\v8Inspector\zlib


I had to copy the follwing files from v8-v141-x64.7.1.302.4 to inthe build directory v8Inspector\v8inspector\build\Debug\ order to make things run:
natives_blob.bin
snapshot_blob.bin
icudtl.dat
icui18n.dll
icuuc.dll
v8.dll
v8_libbase.dll
v8_libplatform.dll

This project has set the preprocessor definition:
_ITERATOR_DEBUG_LEVEL=0
in all configurations as i need this for my projet.
Your progra will probably fail if you use the DLL and this setting is not the same for all modules. So you should either set that too, or remove it from the project
