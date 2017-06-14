<h1>大整数对象的初始化</h1>

本文介绍如何初始化number_t对象（大整数对象），可以用字符串或基本整型变量初始化或赋值number_t对象，赋值相当于重新初始化。也可以将number_t对象转化为字符串或基本整型变量，详见后文《[大整数对象转为字符串](https://github.com/brotherbeer/mydocument/blob/master/mynum/String-conversion-cn.md)》、《[大整数对象转为基本整型变量](https://github.com/brotherbeer/mydocument/blob/master/mynum/To-basic-integer-cn.md)》。

 * [number_t构造函数](#t1)
 * [number_t赋值函数](#t2)
 * [number_t内存相关函数](#t3)
 * [字符串格式检查](#t4)
 * [注意事项](#t5)
 * [示例](#t6)
 * [算法](#t7)

<h2 id="t1">number_t构造函数</h2>

默认构造函数, 对象的值为0
```C++
number_t::number_t();
```

用基本整数类型的变量构造大整数对象，对象的值与其参数的值相同
```C++
number_t::number_t(int x);
number_t::number_t(long x);
number_t::number_t(long long x);
number_t::number_t(unsigned int x);
number_t::number_t(unsigned long x);
number_t::number_t(unsigned long long x);
```

用表示base进制数的字符串s（以'\0'结尾）构造大整数对象，base∈[2, 36]  
可以用'-'表示负数，不接受'+'、前导字符以及任何空白符或标点符号，当s指向空串或为空指针时，对象的值为0
```C++
number_t::number_t(const char* s, int base);
```

如果省略base，则认为字符串表示的是10进制数
```C++
number_t::number_t(const char* s);
```

也可以用length参数指定字符串的长度
```C++
number_t::number_t(const char* s, size_t length, int base);
```

用[string_t](https://github.com/brotherbeer/mydocument/blob/master/mynum/string-cn.md)对象构造大整数对象
```C++
number_t::number_t(const string_t& str, int base);
```

如果省略base，则认为[string_t](https://github.com/brotherbeer/mydocument/blob/master/mynum/string-cn.md)对象表示的是10进制数
```C++
number_t::number_t(const string_t& str);
```

可以用bpos和epos参数指定字符串的起止位置，即用str中位置属于[bpos, epos)的字符序列构造大整数对象，  
bpos从0开始计数，当epos大于str.length()时，则将epos设为str.length()，当bpos >= epos时，大整数对象的值为0
```C++
number_t::number_t(const string_t& str, size_t bpos, size_t epos, int base);
```

拷贝构造函数
```C++
number_t::number_t(const number_t& obj);
```

<h2 id="t2">number_t赋值函数</h2>

用另一个大整数对象赋值
```C++
number_t& number_t::assign(const number_t& obj);
```

用基本整数类型的变量赋值
```C++
number_t& number_t::assign(int x);
number_t& number_t::assign(long x);
number_t& number_t::assign(long long x);
number_t& number_t::assign(unsigned int x);
number_t& number_t::assign(unsigned long x);
number_t& number_t::assign(unsigned long long x);
```

用字符串赋值，各参数意义与相应构造函数相同
```C++
number_t& number_t::assign(const char* s);
number_t& number_t::assign(const char* s, int base);
number_t& number_t::assign(const char* s, size_t length, int base);
number_t& number_t::assign(const string_t& s);
number_t& number_t::assign(const string_t& s, int base);
number_t& number_t::assign(const string_t&, size_t bpos, size_t epos, int base);
```
重载 >>
```C++
std::istream& operator >> (std::istream& is, number_t& a)
```
复制大整数对象
```C++
void copy(const number_t&);
```

将对象的值设为1
```C++
void number_t::set_one();
```

将对象的值设为0
```C++
void number_t::set_zero();
```

<h2 id="t3">number_t内存相关函数</h2>

将对象的值清零，但其占有的内存空间不变
```C++
void number_t::clear();
```
彻底清除对象占有的全部内存，清除后对象的值为0
```C++
void number_t::release();
```
设定对象占有units个数据单元，当units小于当前单元个数时不生效
```
void number_t::reserve(size_t units);
```
将对象的值清零，再设定对象占有的单元个数，当units小于当前单元个数时只清零
```
void number_t::clear_and_reserve(size_t units);
```

<h2 id="t4">字符串格式检查</h2>

检查字符串格式是否正确，可以与构造函数或assign函数配合使用
```C++
int check(const char* str, int base);
int check(const char* strbegin, const char* strend, int base);
```

<h2 id="t5">注意事项</h2>

为了更高的效率，以字符串为参数的构造函数和赋值函数不接受'+'、任何空白符以及任何“前导字符”（如"0x"、"0b"），也不考虑字符串中的字符是否正确。
如果字符串中有错误，那么对象的值也是错误的，但不至于让程序崩溃。可用check函数检查相关字符串是否正确，如果正确再进行初始化，如果可以保证用以初始化的字符串是正确的，则可省去检查的开销。
对于构造函数和赋值函数而言，有效字符为[0-9a-zA-Z]，'a' 和'A'表示的值为10，'b'和'B'表示的值为11，…， 'z'和'Z'表示的值为35，如果一个字符表示的数值大于或等于指定的进制，大整数对象的值也将是错误的。

当然，这只是构造函数和赋值函数的特性，mynum可以处理具有复杂格式的字符串，详见《[格式化字符串转为大整数对象](https://github.com/brotherbeer/mydocument/blob/master/mynum/Formatted-input-ch.md)》以及《[大整数对象转为格式化字符串](https://github.com/brotherbeer/mydocument/blob/master/mynum/Formatted-output-ch.md)》。

用表示16进制数的字符串构造大整数对象时，时间复杂度最低。

copy(const number_t&) 和 assign(const number_t&) 是不同的, assign 只是根据另一个对象进行赋值，copy不但赋值而且还会分配与指定的对象相同内存空间。

<h2 id="t6">示例</h2>

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

<h2 id="t7">算法</h2>

对于下列论述中的BASE、UNITMAX等常量，可参见上一章《[数据存储方式](https://github.com/brotherbeer/mydocument/blob/master/mynum/Storage-ch.md)》。

<h3>用字符串构造对象</h3>

设某个字符串s有n个字符，表示b进制的数，可用s构造一个number_t对象o，o的值与s表示的值相同。

首先要确定o需要多少内存才能装下s表示的数。

显然，n位b进制数的最大值为b<sup>n</sup>-1，设o需要m个单元才能装下这个数，则m需要满足如下等式(设ln表示对数，ceil表示向上取整)：

BASE<sup>m</sup>-1 = b<sup>n</sup>-1

ln(BASE<sup>m</sup>) = ln(b<sup>n</sup>)

m = ceil(n \* ln(b) / ln(BASE)) 

由此可求出需要分配的内存空间为m \* sizeof(unit_t)个字节。

设S<sub>i</sub>为s的第i个字符对应的数值，i∈[0,n)，s表示的整数即：

〈S<sub>0</sub>, S<sub>1</sub>, ..., S<sub>n-1</sub>〉<sub>b</sub> =〈S<sub>0</sub>, S<sub>1</sub>, ..., S<sub>n-2</sub>〉<sub>b</sub> * b + S<sub>n-1</sub>

故该式的计算可由一个迭代过程完成，伪代码如下：
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
在for循环中，i为0时将o的值设为S[0]，以后每次用mul_unit方法将o的值乘以b再用add_unit方法将其加S[i]，循环n次后即完成了对象的初始化，关于mul_unit和add_unit方法请参见上一章《[数据存储方式](https://github.com/brotherbeer/mydocument/blob/master/mynum/Storage-ch.md)》。

显然，该算法的时间复杂度为O(1 + 2 + ... + n) = O(n<sup>2</sup>)，至此，将字符串转为number_t对象的原理已经说明，但在效率上可以改进。

设power_digits是可以使b<sup>power_digits</sup> <= UNITMAX成立的最大值（UNITMAX为数据单元的最大值），power_base = b<sup>power_digits</sup>。
在for循环中，每次将power_digits个字符转成一个单元进行处理，有效减少了乘法和加法的次数，从而提高了效率：
```C++
number_t::construct_from_string(const char* s, int b)
{
    int n = strlen(s), i = 0;
    allocate_units(ceil(n * ln(b) / ln(BASE)));
    int power_base = get_power_base(b);
    int power_digits = get_power_digits(b);
    for (; i < n - n % power_digits; i += power_digits)
    {
        mul_unit(power_base);
        add_unit(str_to_unit(s + i, b, power_digits)); // 每次将power_digits个字符转为一个单元 
    }
    for (; i != n; i++)     // 此for循环是为清晰起见，其实此处仍可优化
    {
        mul_unit(b);
        add_unit(char_to_int(s[i]));
    }
}
```
虽然改进后的算法在效率上有明显提升，但其时间复杂度仍为O(n<sup>2</sup>)。

对于表示16进制数的字符串，因为每2个字符可以确定一个字节，32位环境中每4个字符可以确定一个数据单元，64位环境中每8个字符可以确定一个数据单元，所以不必进行乘法和加法就可以构造大整数对象，时间复杂度为O(n)。
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

<h3>用基本类型的变量构造对象</h3>

可以通过某个基本整数类型的变量v（如int、long等），构造一个number_t对象o，o的值与v的值相等。

因为o以二进制方式存储数据，所以在初始化时可以直接分配大于或等于sizeof(v)的内存，然后再将v的值复制过来。

举个例子，unsigned long long v = 1，如果用其在32位系统中构造o，首先需要分配sizeof(v)即8个字节的空间4个单元的空间，这4个单元由低地址到高地址依次为0x0001，0x0000，0x0000，0x0000。

高址的3个单元为0，是无效的，number_t成员变量len只表示有效单元的个数，所以o中的len应为1，而不是4。

这种高地址上的0单元在mynum中被称为『前导零』，前导零的数量不应计入len中。

