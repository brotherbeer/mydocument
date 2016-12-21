Initialization
-------------

 * [Functions](#functions)
 * [Attentions](#attentions)
 * [Examples](#examples)
 * [Algorithms](#algorithms)

##Functions

Default constructor, the value of the object is 0
```C++
number_t::number_t();
```

Construct a new big integer, and initialize from an int variable 
```C++
number_t::number_t(int);
```

Construct a new big integer, and initialize from a long variable 
```C++
number_t::number_t(long);
```

Construct a new big integer, and initialize from a long long variable 
```C++
number_t::number_t(long long);
```

Construct a new big integer, and initialize from an unsigned int variable 
```C++
number_t::number_t(unsigned int);
```

Construct a new big integer, and initialize from an unsigned long variable 
```C++
number_t::number_t(unsigned long);
```

Construct a new big integer, and initialize from an unsigned long long variable 
```C++
number_t::number_t(unsigned long long);
```

Construct a new big integer, and initialize from a string, which denotes a decimal integer
```C++
number_t::number_t(const char*);
```

Construct a new big integer, and initialize from a string, which denotes a _base_ based integer (2 <= _base_ <= 36)
```C++
number_t::number_t(const char*, int base);
```

Construct a new big integer, and initialize from a string, which is _length_ long, and denotes an _base_ based integer ((2 <= _base_ <= 36))
```C++
number_t::number_t(const char*, size_t length, int base);
```

Construct a new big integer, and initialize from a string_t object, which denotes a decimal integer
```C++
number_t::number_t(const string_t&);
```

Construct a new big integer, and initialize from a string_t object, which denotes a _base_ based integer (2 <= _base_ <= 36)
```C++
number_t::number_t(const string_t&, int base);
```

Construct a new big integer, and initialize from a string_t object, which is _length_ long, and denotes a _base_ based integer (2 <= _base_ <= 36)
```C++
number_t::number_t(const string_t&, size_t length, int base);
```

The copy Constructor
```C++
number_t::number_t(const number_t&);
```

##Attentions
In order to achieve a higher efficiency, when constructing from string, mynum does not consider any prefixes, such as "0x", "0b", and all the constructors donot detect any wrong char in the string parameter.
If the string parameter is wrong, the value of the object is wrong too, but the program will not crash.
The chars in the string parameter are only [0-9a-zA-Z], 'a' and 'A' mean 10, 'b' and 'B' mean 11, and so on, 'z' and 'Z' mean 35.
If a digit denoted by a char is bigger than the specified base, the value of the big integer object is wrong. 

When using a string that denotes a hexadecimal intger, the efficiency is the highest.

##Examples
```C++
#include "mynum.h"
using namespace mynum;        // the namespace of mynum

number_t a = 123, b(789L);    // use basic integer type to initialize number_t objects
number_t c("271828182845");   // use a decimal string to initialize the object
number_t d("abcdef", 16);     // use a hexadecimal number to initialize the object
number_t e("1234567", 8);     // use an octal string to initialize the object
number_t f("1111100", 2);     // use a binary string to initialize the object
number_t g("abcdefg", 17);    // use a string denotes 17 based integer

number_t x("123456789", 8);   // in octal number, '8' and '9' are wrong, so the value of x is wrong
number_t y("1,234,567", 8);   // ',' and other punctuations are not acceptable
number_t z("1 234 567", 8);   // the blank spaces are not acceptable
```

If you want to test the correctness of the string, you can use the 'check' function, for example:
The function 'check' returns the string length if the string is right, or 0 if the string is wrong.
```C++
const char* s = "1234567890";
assert(check(s, 10) > 0);     // if s denotes a decimal number, then s is correct
assert(check(s, 8) == 0);     // if s denotes an octal number, then s is wrong
```

##Algorithms

下列论述中的常量如BASE、MASK等可参见上一章[The data storage model of mynum]

###Construct from strings

设某个字符串s有n个字符，表示b进制的数，可用s构造一个number_t对象o，o与s表示的值相同。

首先要确定o需要多少内存才能装下s表示的数。

显然，n位b进制数的最大值为b<sup>n</sup>-1，设o需要m个单元才能装下这个数，则m需要满足如下等式(设ln表示自然对数，ceil表示向上取整)：

BASE<sup>m</sup>-1 = b<sup>n</sup>-1

ln(BASE<sup>m</sup>) = ln(b<sup>n</sup>)

m = ceil(n * ln(b) / ln(BASE))

由此可求出需要分配的内存空间为m * sizeof(unit_t)个字节。

设S为s的字符序列对应的数值序列，s表示的整数可由下式表式：

S[0]\*b<sup>n-1</sup> + S[1]\*b<sup>n-2</sup> + ... + S[n-1]\*b<sup>0</sup>

伪代码如下：
```C++
number_t::construct_from_string(const char* s, int b)
{
    int n = strlen(s)
    allocate_units(ceil(n * ln(b) / ln(BASE)))  // allocate m units
    for (i = 0; i < n; i++)
    {
        mul_unit(b)
        add_unit(char_to_int(s[i]))   // char_to_int converts a char to int, S[i] is char_to_int(s[i])
    }
}
```
在for循环中，i为0时将o的值设为S[0]，以后每次用mul_unit方法将o的值乘以b再用add_unit方法将其加S[i]，循环n次后即完成了对象的初始化，
关于mul_unit和add_unit方法请参见上一章 [The data storage model of mynum]
至此，将字符串转为number_t对象的原理已经说明，但在效率上可以改进。

设inner_digits是可以使b<sup>inner_digits</sup> <= MASK成立的最大值（MASK为计算单元的最大值）
inner_base = b<sup>inner_digits</sup>
在for循环中，每次将inner_digits个字符转成一个单元进行处理，有效减少了乘法和加法的次数。

可以得到更高效的方法：
```C++
number_t::construct_from_string(const char* s, int b)
{
    int n = strlen(s), i = 0
    allocate_units(ceil(n * ln(b) / ln(BASE)))
    int inner_base = get_inner_base(b)
    int inner_digits = get_inner_digits(b)
    for (; i < n - n % inner_digits; i += inner_digits)
    {
        mul_unit(inner_base)
        add_unit(str_to_unit(s + i, b, inner_digits))  // 将inner_digits个字符转为一个单元
    }
    for (; i != n; i++)
    {
        mul_unit(b)
        add_unit(char_to_int(s[i]))
    }
}
```

对于表示16进制数的字符串，因为每2个字符可以确定一个字节，所以32位环境中每4个字符可以确定一个计算单元，64位环境中每8个字符可以确定一个计算单元，所以不必通过乘法和加法就可以构造大整数对象。
```C++
number_t::construct_from_hex_string(const char* s)
{
    int n = strlen(s)
    int k = sizeof(unit_t) * 2   // k个字节为一个单元
    const char* p0 = s + n - k
    const char* p1 = s + n % k

    allocate_units((n + k - 1) / k)    // 共需要(n + k - 1) / k个单元
    for (; p0 >= p1; p0 -= k)          // 每次将k个字符转为一个单元存入单元序列中
    {
        dat[len++] = strhex_to_unit(p0, k)  
    }
    if (n % k)                                    //最后将n%k个字符转为一个单元存入单元序列中 
    {
        dat[len++] = strhex_to_unit(s, n % k)
    }
}
```
故通过表示16进制数的字符串构造大整数对象时的效率最高。
同理对于表示2进制数的字符串，也不必通过乘法和加法构造大整数对象。


###Construct from basic types


