Compilation
-------------

The source code is currently applicable to g++, MSVC (2008 and above versions) and clang.

When using MSVC, the following functions are required:
* _BitScanReverse
* _BitScanForward
* __emulu
* _umul128

When using g++, the following functions or types are required:
* __uint128_t
* __builtin_ctz
* __builtin_clz

Please use the compiler which supports above intrinsic functions or types. if your compiler does not support the requirements, you can define a global macro `NO_INTRINSIC` to enable the standard C++ implementation, but the performance may be slower.

Other compilers may do the compilation, but the author has not yet tested.

mynum can also be compiled into a dynamic library, for example:

`g++ -fPIC -shared -O2 -DNDEBUG mynum.cpp -o mynum.so`

When your product is released, don't forget to define `NDEBUG`, drop all the assertions.