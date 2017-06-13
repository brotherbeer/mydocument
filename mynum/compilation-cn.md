<h1>编译</h1>

mynum的代码目前可以用g++、MSVC (2008及以上版本)、clang编译。

如果用MSVC，需要：
* _BitScanReverse
* _BitScanForward
* __emulu
* _umul128

如果用g++，需要:
* __uint128_t
* __builtin_ctz
* __builtin_clz

请使用支持上述intrinsic函数或类型的编译器进行编译，如果编译器不支持，也可以定义全局宏`NO_INTRINSIC`，将采用纯标准C++实现，但对性能有一定影响，如：

`g++ -Wall -DNO_INTRINSIC mynum.cpp test.cpp -o test`

其它编译器或许也可以进行编译，但作者尚未测试。

也可以将mynum编译成动态库，如：

`g++ -fPIC -shared -O2 -DNDEBUG mynum.cpp -o mynum.so`

当你的产品需要发布时，别忘了定义NDEBUG来去掉所有的assert。