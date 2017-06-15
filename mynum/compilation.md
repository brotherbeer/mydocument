<h1>Compilation</h1>

The source code is currently applicable to g++, MSVC (2008 and above versions) and clang.

When using MSVC, the following intrinsic functions are required:
 * _BitScanReverse
 * _BitScanForward
 * _BitScanReverse64
 * _BitScanForward64
 * __emulu
 * _umul128

When using g++, the following types or functions are required:
 * __uint128_t
 * __builtin_ctz
 * __builtin_clz
 * __builtin_popcount

Please use the compiler which supports above intrinsic functions or types. If your compiler does not support the requirements, you can define a global macro `NO_INTRINSIC` to enable the standard C++ implementation, but the performance may be slower.

Other compilers may do the compilation, but the author has not yet tested.

mynum can also be compiled into a dynamic library, for example:

`g++ -fPIC -shared -O2 -DNDEBUG mynum.cpp -o mynum.so`

When your product is released, don't forget to define `NDEBUG`, drop all the assertions.