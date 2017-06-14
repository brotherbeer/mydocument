![logo](https://github.com/brotherbeer/mydocument/blob/master/mynum/mynum-logo.png?raw=true)

Mynum(multiprecision binary number)是一个轻便的C++大数算法库，致力于为数论、密码学等研究提供便利。

文档：

 * [编译](https://github.com/brotherbeer/mydocument/blob/master/mynum/compilation-cn.md)
 * [数据存储方式](https://github.com/brotherbeer/mydocument/blob/master/mynum/Storage-ch.md)
 * [初始化](https://github.com/brotherbeer/mydocument/blob/master/mynum/Initialization-ch.md)
 * [字符串转换](https://github.com/brotherbeer/mydocument/blob/master/mynum/String-conversion-cn.md)
 * [整型变量转换](https://github.com/brotherbeer/mydocument/blob/master/mynum/To-basic-integer-cn.md)
 * [格式化字符串转大整数](https://github.com/brotherbeer/mydocument/blob/master/mynum/Formatted-input-ch.md)
 * [大整数转格式化字符串](https://github.com/brotherbeer/mydocument/blob/master/mynum/Formatted-output-ch.md)
 * [加法](https://github.com/brotherbeer/mydocument/blob/master/mynum/Addition-cn.md)
 * [减法](https://github.com/brotherbeer/mydocument/blob/master/mynum/Subtraction-cn.md)
 * [乘法](https://github.com/brotherbeer/mydocument/blob/master/mynum/Multiplication-cn.md)
 * [除法](https://github.com/brotherbeer/mydocument/blob/master/mynum/Division-cn.md)
 * [模运算](https://github.com/brotherbeer/mydocument/blob/master/mynum/Modulo-operation-cn.md)
 * [乘方](https://github.com/brotherbeer/mydocument/blob/master/mynum/Exponentiation-cn.md)
 * [幂取模](https://github.com/brotherbeer/mydocument/blob/master/mynum/Modular-exponentiation-cn.md)
 * [素性测试](https://github.com/brotherbeer/mydocument/blob/master/mynum/Primality-test-cn.md)
 * [数论函数](https://github.com/brotherbeer/mydocument/blob/master/mynum/Number-theory-cn.md)
 * [随机数](https://github.com/brotherbeer/mydocument/blob/master/mynum/Random-number-cn.md)
 * [比较](https://github.com/brotherbeer/mydocument/blob/master/mynum/Comparison-cn.md)
 * [位运算](https://github.com/brotherbeer/mydocument/blob/master/mynum/Bitwise-operation-cn.md)
 * [其它](https://github.com/brotherbeer/mydocument/blob/master/mynum/Other-utils-cn.md)
 * [字符串](https://github.com/brotherbeer/mydocument/blob/master/mynum/string-cn.md)

Mynum用纯粹的C++实现，配以现代编译器的intrinsic技术，在保证高效运算的同时将接口易用作为首要理念。

作者希望mynum能够有用，并对mynum源码的传播与修改不作任何限制，但不作任何保证，如有疑问请联系 <brotherbeer@163.com>

[mynumheaderfile]: https://github.com/brotherbeer/mynum/blob/master/mynum.h
[mynumcppfile]: https://github.com/brotherbeer/mynum/blob/master/mynum.cpp
[mytheoryheaderfile]: https://github.com/brotherbeer/mynum/blob/master/mytheory.h
[mytheorycppfile]: https://github.com/brotherbeer/mynum/blob/master/mytheory.cpp
[myoperatorheaderfile]: https://github.com/brotherbeer/mynum/blob/master/myoperators.h
[testcppfile]: https://github.com/brotherbeer/mynum/blob/master/test.cpp

##安装与编译

所需文件:

 * [mynum.cpp][mynumcppfile] 实现大数的基本四则运算及字符串格式化输入输出等功能，对应头文件[mynum.h][mynumheaderfile] 
 * [mytheory.cpp][mytheorycppfile] 实现数论相关的功能，如最大公约数等功能，对应头文件[mytheory.h][mytheoryheaderfile] 
 * [myoperators.h][myoperatorheaderfile] 重载了相关的C++运算符。

将这些文件拷贝到你的工程空间，在需要进行大数运算的文件中，引入[mynum.h][mynumheaderfile]、[mytheory.h][mytheoryheaderfile]或者[myoperators.h][myoperatorheaderfile]即可，mynum的命名空间即为`mynum`。

 * [test.cpp][testcppfile]中为测试用例及简单示例。

源码目前适用于g++、clang、MSVC(2008及以上版本)编译，请参见《[mynum的编译](https://github.com/brotherbeer/mydocument/blob/master/mynum/compilation-cn.md)》。

##联系方式

 * 如果需要帮助，欢迎来信 <brotherbeer@163.com>
 * 如果发现可复现的bug，请开启一个issue
 * 如果需要添加新功能，请开启一个issue
 * 如果想提交代码，可以提交一个pull request
