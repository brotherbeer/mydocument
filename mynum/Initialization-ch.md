大整数对象的初始化
-------------

 * [函数](#函数)
 * [注意事项](#注意事项)
 * [示例](#示例)
 * [算法](#算法)

##函数

默认构造函数, \*this的值为0
```C++
number_t::number_t();
```

用基本整数类型的变量构造大整数对象
```C++
number_t::number_t(int x);
number_t::number_t(long x);
number_t::number_t(long long x);
number_t::number_t(unsigned int x);
number_t::number_t(unsigned long x);
number_t::number_t(unsigned long long x);
```

用表示base进制数的字符串（以'\0'结尾）构造大整数对象，base ∈ [2, 36]
可以用'-'表示负数
不接受任何空白符或标点符号
```C++
number_t::number_t(const char* s, int base);
```

如果省略base，则认为字符串表示的是10进制数
```C++
number_t::number_t(const char* s);
```

也可以指定字符串的长度
```C++
number_t::number_t(const char* s, size_t length, int base);
```

用string_t对象构造大整数对象
```C++
number_t::number_t(const string_t&);
number_t::number_t(const string_t&, int base);
number_t::number_t(const string_t&, size_t length, int base);
```

拷贝构造函数
```C++
number_t::number_t(const number_t&);
```

用另一个大整数对象赋值
```C++
number_t& assign(const number_t&);
```

用基本整数类型的变量赋值
```C++
number_t& assign(int x);
number_t& assign(long x);
number_t& assign(long long x);
number_t& assign(unsigned int x);
number_t& assign(unsigned long x);
number_t& assign(unsigned long long x);
```

用字符串赋值，各参数意义与构造函数相同
```C++
number_t& assign(const char* s);
number_t& assign(const char* s, int base);
number_t& assign(const char* s, size_t length, int base);
number_t& assign(const string_t& s);
number_t& assign(const string_t& s, int base);
number_t& assign(const string_t& s, size_t length, int base);
```

复制大整数对象
```C++
void copy(const number_t&);
```

##注意事项
为了更高的效率，由字符串构造大整数对象时，mynum不考虑任何前缀，如"0x"、"0b"等，也不考虑字符串的格式是否正确。
如果字符串中有错误，那么构造的对象的值也是错误的，但不至于让程序崩溃。
有效字符只有[0-9a-zA-Z]，'a' 和'A'表示10，'b'和'B'表示11，…， 'z'和'Z'表示35
如果一个字符表示的数值大于指定的进制，大整数对象的值也将是错误的。

用表示16进制数的字符串构造对象时，效率是最高的。

copy(const number_t&) 和 assign(const number_t&) 是不同的, assign 只是将另一个对象的值赋给*this，copy不但赋值而且还会分配与指定的对象相同内存空间。


##示例
```C++
#include "mynum.h"
using namespace mynum;        // the namespace of mynum

number_t a = 123, b(789L);    // 用基本类型构造
number_t c("271828182845");   // 用表示10进制数的字符串构造
number_t d("abcdef", 16);     // 用表示16进制数的字符串构造
number_t e("1234567", 8);     // 用表示8进制数的字符串构造
number_t f("1111100", 2);     // 用表示2进制数的字符串构造
number_t g("abcdefg", 17);    // 用表示17进制数的字符串构造

number_t x("123456789", 8);   // 8进制数中没有8和9，所以x的值将是错误的
number_t y("1,234,567", 8);   // ',' 和其它标点符串是不允许的
number_t z("1 234 567", 8);   // 空白符也是不允许的
```

可以用check函数来检查字符串是否正确，例如：
如果字符串是正确的，check函数返回字符串长度，否则返回0
```C++
const char* s = "1234567890";
assert(check(s, 10) > 0);     // 如果s表示10进制数，s是正确的
assert(check(s, 8) == 0);     // 如果s表示8进制数，s是错误的
```

##算法

对于下列论述中的BASE、MASK等常量，可参见上一章《[mynum的数据存储方式](https://github.com/brotherbeer/mydocument/blob/master/mynum/Storage-ch.md)》。

###用字符串构造对象

设某个字符串s有n个字符，表示b进制的数，可用s构造一个number_t对象o，o与s表示的值相同。

首先要确定o需要多少内存才能装下s表示的数。

显然，n位b进制数的最大值为b<sup>n</sup>-1，设o需要m个单元才能装下这个数，则m需要满足如下等式(设ln表示自然对数，ceil表示向上取整)：

BASE<sup>m</sup>-1 = b<sup>n</sup>-1

ln(BASE<sup>m</sup>) = ln(b<sup>n</sup>)

m = ceil(n \* ln(b) / ln(BASE))

由此可求出需要分配的内存空间为m \* sizeof(unit_t)个字节。

设S为s的字符序列对应的数值序列，s表示的整数可由下式表式：

S[0]\*b<sup>n-1</sup> + S[1]\*b<sup>n-2</sup> + ... + S[n-1]\*b<sup>0</sup>

该式的计算可由一个迭代过程完成，伪代码如下：
```C++
number_t::construct_from_string(const char* s, int b)
{
    int n = strlen(s);
    allocate_units(ceil(n * ln(b) / ln(BASE)));  // allocate m units
    for (i = 0; i < n; i++)
    {
        mul_unit(b);
        add_unit(char_to_int(s[i])); // char_to_int converts a char to int
                                     // S[i] is char_to_int(s[i])
    }
}
```
在for循环中，i为0时将o的值设为S[0]，以后每次用mul_unit方法将o的值乘以b再用add_unit方法将其加S[i]，循环n次后即完成了对象的初始化，关于mul_unit和add_unit方法请参见上一章《[mynum的数据存储方式](https://github.com/brotherbeer/mydocument/blob/master/mynum/Storage-ch.md)》。

至此，将字符串转为number_t对象的原理已经说明，但在效率上可以改进。

设inner_digits是可以使b<sup>inner_digits</sup> <= MASK成立的最大值（MASK为计算单元的最大值），inner_base = b<sup>inner_digits</sup>。
在for循环中，每次将inner_digits个字符转成一个单元进行处理，有效减少了乘法和加法的次数，从而提高了效率：
```C++
number_t::construct_from_string(const char* s, int b)
{
    int n = strlen(s), i = 0;
    allocate_units(ceil(n * ln(b) / ln(BASE)));
    int inner_base = get_inner_base(b);
    int inner_digits = get_inner_digits(b);
    for (; i < n - n % inner_digits; i += inner_digits)
    {
        mul_unit(inner_base);
        add_unit(str_to_unit(s + i, b, inner_digits)); // 每次将inner_digits个字符转为一个单元 
    }
    for (; i != n; i++)
    {
        mul_unit(b);
        add_unit(char_to_int(s[i]));
    }
}
```

对于表示16进制数的字符串，因为每2个字符可以确定一个字节，32位环境中每4个字符可以确定一个计算单元，64位环境中每8个字符可以确定一个计算单元，所以不必进行乘法和加法就可以构造大整数对象。
```C++
number_t::construct_from_hex_string(const char* s)
{
    int n = strlen(s);
    int k = sizeof(unit_t) * 2;         // k个字节为一个单元
    const char* p0 = s + n - k;
    const char* p1 = s + n % k;

    allocate_units((n + k - 1) / k);    // 共需要(n + k - 1) / k个单元
    for (; p0 >= p1; p0 -= k)           // 每次将k个字符转为一个单元存入单元序列中
    {
        dat[len++] = strhex_to_unit(p0, k); 
    }
    if (n % k)                          //最后将n % k个字符转为一个单元存入单元序列中 
    {
        dat[len++] = strhex_to_unit(s, n % k);
    }
}
```
故在相同数值的情况下，用16进制表示的字符串构造大整数对象时的效率最高，同理对于表示2进制数的字符串，也不必通过乘法和加法构造大整数对象。

###用基本类型的变量构造对象

可以通过某个基本整数类型的变量v（如int、long等），构造一个number_t对象o，o与v的值相同。

因为o以二进制方式存储数据，所以在初始化时可以直接分配大于或等于sizeof(v)的内存，然后再将v的值复制过来。

举个例子，unsigned long long v = 1，如果用其在32位系统中构造o，首先需要分配sizeof(v)即8个字节的空间4个单元的空间，这4个单元由低地址到高地址依次为0x0001，0x0000，0x0000，0x0000。

高址的3个单元为0，是无效的，number_t成员变量len只表示有效单元的个数，所以o中的len应为1，而不是4。

这种高址上的0单元在mynum中被称为『前导零』，前导零的数量不应计入len中。

