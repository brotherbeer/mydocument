MYNUM
-------------

mynum 是一个轻便的大数算法库，致力于为数论、密码学等研究提供便利。

mynum 目前只适用于小尾序机型。

目前mynum 提供：

 * [Initialization](#initialization)
 * [Addition](#addition)
 * [Subtraction](#subtraction)
 * [Multiplication](#multiplication)
 * [Division](#division)
 * [Modulo operation](#modulo-operation)
 * [Exponentiation](#exponentiation)
 * [Modular exponentiation](#modular-exponentiation)
 * [Comparison](#comparison)
 * [Bits operations](#bits-operations)
 * [String convertion](#string-convertion)
 * [Other utils](#other-utils)

示例:

 * [Greatest common divisor](#greatest-common-divisor)
 * [Compute PI](#compute-pi)
 * [Compute the natural logarithms base](#compute-the-natural-logarithms-base)

mynum的性能并不逊于GMP等名库太多，而其接口却简便得多，相比于java、python等语言的内置大数库，mynum在某些方面的效率甚至更高。

作者希望mynum能够有用，但不作任何保证，并对mynum源码的传播与修改不作任何限制，如有疑问请联系 <brotherbeer@163.com>

[mynumheaderfile]: https://github.com/brotherbeer/mynum/blob/master/mynum.h
[mynumcppfile]: https://github.com/brotherbeer/mynum/blob/master/mynum.cpp
[myoperatorheaderfile]: https://github.com/brotherbeer/mynum/blob/master/operators.h
[testcppfile]: https://github.com/brotherbeer/mynum/blob/master/test.cpp

##Installation
[mynum.h][mynumheaderfile]和[mynum.cpp][mynumcppfile] 是mynum的核心文件，其它文件为功能扩展。在项目中引入[mynum.h][mynumheaderfile]和[mynum.cpp][mynumcppfile]即可。

[myoperators.h][myoperatorheaderfile] 重载了相关的C++运算符。

[test.cpp][testcppfile]包含了测试用试。

也可将mynum编译成动态库，如：

`g++ -fPIC -shared -O2 -DNDEBUG mynum.cpp -o mynum.so`

源码目前适用于g++或MSVC(2008 and above versions)编译。

##Initialization
```C++
#include "mynum.h"
using namespace mynum;      // the namespace of mynum

number_t a = 123, b(789L);  // 用基本类型的变量构造
number_t c("27182818284");  // 用表示10进制数的字符串构造
number_t d("-abcdef", 16);  // 用表示16进制数的字符串构造
number_t e("1234567", 8);   // 用表示8进制数的字符串构造
number_t f("1111100", 2);   // 用表示2进制数的字符串构造
```
用表示16进制数的字符串构造对象时，效率是最高的。

为了更高的效率，由字符串构造大整数对象时，mynum不考虑任何前缀，如"0x"、"0b"等，也不考虑字符串的格式是否正确。
如果字符串中有错误，那么构造的对象的值也是错误的，但不至于让程序崩溃。
有效字符只有[0-9a-zA-Z]，'a' 和'A'表示10，'b'和'B'表示11，…， 'z'和'Z'表示35
如果一个字符表示的数值大于指定的进制，大整数对象的值也将是错误的。
```C++
number_t x("123456789", 8);   // 在8进制数中, '8'和'9'是非法的，所以x的值将是错误的
number_t y("1,234,567", 8);   // 标点符号是不允许的
number_t z("1 234 567", 8);   // 空白符也是不允许的
```
在后续版本中，mynum会优化字符串相关的处理。

如果需要检查字符串是否正确，可以用check函数，如：
```C++
const char* s = "1234567890";
assert(check(s, 10) > 0); // 如果s表示10进制数，s是正确的
assert(check(s, 8) == 0); // 如果s表示8进制数，s是错误的
```
哪果字符串是正确的，check返回字符串长度，否则返回0。

当时制大于10时，'a'表示10，'b'表示11，...，'z'表示35, 最大进制为36，各字符不区分大小写。

由默认构造函数构造的对象值为0
```C++
number_t a;
assert(a == 0);   // == 定义在myoperators.h中
```

number_t对象在堆上分配内存，用clear函数回收内存：
```C++
number_t a(123456LL);
a.clear();
assert(a == 0);
```

##Addition
```C++
number_t a = 123, b = 456, c;
add(a, b, c);  // add a and b, c is the result

c.add(a);      // add a to c

c = add(a, b); // return result as an object

c = a + b;     // overloaded operator +, need myoperators.h

c += a;        // overloaded operator +=

++c++;         // increase 1
```

##Subtraction
```C++
number_t a = 123, b = 456, c;
sub(a, b, c);  // c is the result of a - b

c.sub(a);      // the same to c -= a

c = sub(a, b); // return object

c = a - b;     // overloaded operator -, need myoperators.h

c -= a;

--c--;         // decrease 1
```

##Multiplication
```C++
number_t a = 123, b = 456, c;
mul(a, b, c);  // c is the result of a * b

c.mul(a);      // the same to c *= a

kmul(a, b, c); // using karatsuba algorithm

c = mul(a, b);

c = a * b;     // overloaded operator *, using kmul

c *= a;
```

##Division
```C++
number_t a = 123, b = 456, q, r;
div(a, b, q);     // a is the dividend, b is the divisor, q is the quotient

div(a, b, q, r);  // r is the remainder

a.div(b);

a.div(b, r);

q = div(a, b);   // return object

q = a / b;       // overloaded operator /, need myoperators.h

a /= b;
```

##Modulo operation
```C++
number_t a = 123, b = 456, q, r;

mod(a, b, r);    // r is the remainder after division of a by b

r = mod(a, b);   // return object

r = a % b;       // overloaded operator %, need myoperators.h

a %= b;
```

##Exponentiation
```C++
number_t a = 123, b = 456, c;

sqr(a, c);      // set c to a * a;

ksqr(a, c);     // using karatsuba algorithm

pow(a, b, c);   // set c to a raised to the power of b, it is required that b > 0

c = pow(a, b);
```

##Modular exponentiation
```C++
number_t a = 123, b = 456, c = 678, d;

pom(a, b, c, d);  // set d to a raised to b modulo c
```

##Comparison
```C++
number_t a = 123, b = 456;
cmp(a, b) < 0;   // a < b
cmp(a, b) > 0;   // a > b
cmp(a, b) == 0;  // a == b 

eq(a, b);        // equal
lt(a, b);        // less than
gt(a, b);        // greater than
elt(a, b);       // equal or less than
egt(a, b);       // equal or greater than

a < b;           // overloaded operators, need myoperators.h
a > b;
a == b;
a >= b;
a <= b;
```

##Bits operations
```C++
number_t a = 123, b = 456, c;
bit_and(a, b, c);  // bitwise and, c is the result
bit_or(a, b, c);   // bitwise or
bit_xor(a, b, c);  // bitwise exclusive or
bit_not(a, c);     // bitwise not

a.bit_and(b);
a.bit_or(b);
a.bit_xor(b);
a.bit_not();

c = a & b;         // overloaded operators, need myoperators.h
c = a | b;
c = a ^ b;
c = ~a;

a &= b;
a |= b;
a ^= b;

shl(a, 5, c);     // left shift 5 bits
shr(a, 5, c);     // right shift 5 bits 

c = a << 5;       // overloaded operators, need myoperators.h
c = a >> 5;
a <<= 5;
a >>= 5;
```

##String convertion
```C++
number_t a = 123;

a.to_string(36);  // convert a to base-36 string
a.to_string(19);  // convert a to base-19 string
a.to_string(16);  // convert a to base-16 string
a.to_string(10);  // convert a to base-10 string
a.to_string(8);   // convert a to base-8 string
a.to_string(2);   // convert a to base-2 string
```
Use follow methods for higher efficiency:

 * to_bin_string() to get base-2 string
 * to_oct_string() to get base-8 string
 * to_dec_string() to get base-10 string
 * to_hex_string() to get base-16 string

in the above methods, the efficiency of to_hex_string() is the highest.

Currently, the max base supported is 36, it will be extended in the subsequent version,
you can use max_base() to obtain the max base supported

`NOTICE!! never use a.to_string(0), a.to_string(1) and a base larger than max_base() returned`

##Other utils
####Absolute value
```C++
number_t a = -123;
number_t b = abs(a);  // set b to the absolute value of a

b = a.abs();    // equals to abs(a)

a.set_abs();    // set a to its absolute value
```

####Negative value
```C++
number_t a = -123;
number_t b = neg(a);

b = a.neg();

a.set_neg();
```

####Number property
```C++
number_t a = 123, b = a;
a.is_even();   // return true if a is an even number

a.is_not(b);   // return true if a and b are not same object

a.is_odd();    // return true if a is an odd number

a.is_one();    // return true if a is 1

a.is_po2();    // return true if a is the n-th power of 2 (n >= 0)

a.is_zero();   // return true if a is 0
```

####String
```C++
number_t a = 0xABCD;
string_t s;                // define a string object
s = a.to_hex_string();     // return the object, lower efficiency
assert(s == "abcd");             // lowercase is default
assert(s.to_upper() == "ABCD");  // to upper case

a.to_bin_string(s);  // to string based 2

a.to_oct_string(s);  // to string based 8

a.to_dec_string(s);  // to string based 10

a.to_hex_string(s);  // to string based 16

a.to_string(s);      // convert the value to string, base 10 is default 

a.to_string(s, x);   // convert the value to string based x 
```

####Swap and sign
```C++
number_t a = 123, b = 456;

swap(a, b);      // swap a and b, after this function called, a is 456, b is 123

a.steal(b);      // a steals the data of b, so a gets the memory of b, and b is set 0

a.set_one();     // set a 1

a.set_zero();    // set a 0

a.set_sign(x);   // if x is 1 then set a to be positive, if x is -1 then set a to be negative

sign(a);         // if a > 0 return 1 else return -1

same_sign(a, b); // if a and b have the same sign, return 1, else return 0
```

#Examples:

##Greatest common divisor 
```C++
#include "myoperators.h"
using namespace mynum;

/*
 * compute the greatest common divisor with division algorithm
 */
void gcd_example()
{
    number_t m("3149916521386303663457"), n("97950481"), t;
    while (m % n != 0)
    {
        mod(m, n, t);
        m.steal(n);
        n.steal(t);
    }
    assert(n == 19937);
}
```

##Compute PI
```C++
#include "myoperators.h"
using namespace mynum;

/*
 * rearctan1 and rearctan2 have the same function,
 * they use Maclaurin expansion to get the product of arctan(1/x) and the n-th power of 10
 *
 * rearctan1 uses the overloaded operators, rearctan1 uses the normal APIs
 * operator overloading makes the source code briefer, but the efficiency is slightly lower
 * the two functions are used by PI_example() to compute the circumference ratio PI
 * the example obtaines 100 decimal places of PI, readers can set n to their interested value,
 * and get the result
 */
void rearctan1(int x, int n, number_t& res);
void rearctan2(int x, int n, number_t& res);

/*
 *  Use Machin's formula to compute PI
 *  PI = 16 * arctan(1/5) - 4 * arctan(1/239)
 *  The last few decimal places may be wrong, increase n to obtain higher accuracy
 */
void PI_example()
{
    int n = 100;
    number_t t0, t1;

    rearctan1(5, n, t0);
    t0 <<= 2;
    rearctan2(239, n, t1);
    t0 -= t1;
    t0 <<= 2;

    // the result
    assert (t0.to_dec_string() == "31415926535897932384626433832795028841971693993751058209749445923078164062862089986280348253421170712");
}

void rearctan1(int x, int n, number_t& res)
{
    int k = 1;
    number_t u, v, xx(x * x);

    res = 10;
    res.pow(n).div(x);
    u = res;

    do
    {
        u /= xx;
        v = u / (2 * k + 1);
        v *= ((k & 1) * -1) | 1;
        res += v;
        k++;
    } while (v);
}

void rearctan2(int x, int n, number_t& res)
{
    int k = 1;
    number_t u, v, xx(x * x);

    res = 10;
    res.pow(n).div(x);
    u = res;

    do
    {
        u.div(xx);
        div(u, 2 * k + 1, v);
        v.set_sign(0 - (k & 1));
        res.add(v);
        k++;
    } while (v);
}
```

##Compute the natural logarithms base
```C++
#include "myoperators.h"
using namespace mynum;

/*
 *  This example computes the decimal places of the natural logarithms base E
 *  The last few decimal places may be wrong, increase n to obtain higher accuracy
 */
void E_example()
{
    // unit_t is the basic computing unit type of mynum
    // on 64bit systems, unit_t is unsigned int
    // on 32bit systems, unit_t is unsigned short
    // so the value of the unit_t type variable is between [0, 4294967295] on 64bit systems,
    // or [0, 65535] on 32bits systems
    // when the computing relates to small integers which can be hold by unit_t,
    // unit_t operations will be more efficient

    unit_t n = 100, i = 2;
    number_t x = 10, e;
    x.pow(n);

    while (x)
    {
        x.div_unit(i++);  // faster than x.div(i++)
        e.add(x);
    }

    // the result
    assert(e.to_string() == "7182818284590452353602874713526624977572470936999595749669676277240766303535475945713821785251664238");
}
```

more examples in [test.cpp][testcppfile]
