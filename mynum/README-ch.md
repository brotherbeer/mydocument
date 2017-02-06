![logo](https://github.com/brotherbeer/mydocument/blob/master/mynum/mynum-logo.png?raw=true)

Mynum是一个轻便的大数算法库，致力于为数论、密码学等研究提供便利。

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
 * [比较](https://github.com/brotherbeer/mydocument/blob/master/mynum/Comparison-cn.md)
 * [位运算](https://github.com/brotherbeer/mydocument/blob/master/mynum/Bitwise-operation-cn.md)
 * [其它](https://github.com/brotherbeer/mydocument/blob/master/mynum/Other-utils-cn.md)

Mynum的性能并不逊于GMP等名库太多，而其接口却简便得多，相比于java、python等语言的内置大数库，mynum在某些方面的效率甚至更高。

作者希望mynum能够有用，但不作任何保证，并对mynum源码的传播与修改不作任何限制，如有疑问请联系 <brotherbeer@163.com>

[mynumheaderfile]: https://github.com/brotherbeer/mynum/blob/master/mynum.h
[mynumcppfile]: https://github.com/brotherbeer/mynum/blob/master/mynum.cpp
[myoperatorheaderfile]: https://github.com/brotherbeer/mynum/blob/master/operators.h
[testcppfile]: https://github.com/brotherbeer/mynum/blob/master/test.cpp

##安装与编译
[mynum.h][mynumheaderfile]和[mynum.cpp][mynumcppfile] 是mynum的核心文件，其它文件为功能扩展。在你的项目中引入[mynum.h][mynumheaderfile]和[mynum.cpp][mynumcppfile]即可，命名空间即是mynum。

[myoperators.h][myoperatorheaderfile] 重载了相关的C++运算符。

[test.cpp][testcppfile]中为测试用例。

源码目前适用于g++、clang、MSVC(2008及以上版本)编译，请参见《[mynum的编译](https://github.com/brotherbeer/mydocument/blob/master/mynum/compilation-cn.md)》。

##联系方式

 * 如果需要帮助，欢迎来信 <brotherbeer@163.com>
 * 如果发现可复现的bug，请开启一个issue
 * 如果需要添加新功能，请开启一个issue
 * 如果想提交代码，可以提交一个pull request
