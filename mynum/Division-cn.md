除法
-------------

 * [全局函数](#全局函数)
 * [Number_t成员函数](#number_t成员函数)
 * [运算符](#运算符)
 * [用乘法作除法](#用乘法作除法)
 * [注意事项](#注意事项)

##全局函数

Set _a_ / _b_ to _q_, and _a_ % _b_ to _r_. If _b_ is 0, the functions return 0, otherwise return 1
```C++
int div(const number_t& a, const number_t& b, number_t& q, number_t& r);
int div(const number_t& a, const number_t& b, number_t& q);
```

Set _a_ / _x_ to _res_, if the divisor _x_ is small and can be hold by `unit_t`, return the remainder
```C++
unit_t div_unit(const number_t& a, unit_t x, number_t& res);
```

_udm_ is the reciprocal of the divisor, use multiplication to do the division, return the remainder
```C++
unit_t div_unit(const number_t& a, const UDM& udm, number_t& res);
```

Set _a_ / _x_ to _res_ (_x_ is an ordinary integer)
```C++
void div(const number_t& a, int x, number_t& res);
void div(const number_t& a, unsigned int x, number_t& res);
void div(const number_t& a, long x, number_t& res);
void div(const number_t& a, unsigned long x, number_t& res);
void div(const number_t& a, long long x, number_t& res);
void div(const number_t& a, unsigned long long x, number_t& res);
```

Set _x_ / _b_ to _res_ (_x_ is an ordinary integer)
```C++
void div(int x, const number_t& b, number_t& res);
void div(unsigned int x, const number_t& b, number_t& res);
void div(long x, const number_t& b, number_t& res);
void div(unsigned long x, const number_t& b, number_t& res);
void div(long long x, const number_t& b, number_t& res);
void div(unsigned long long x, const number_t& b, number_t& res);
```

Return _a_ / _b_
```C++
number_t div(const number_t& a, const number_t& b);
```

##Number_t成员函数

Divide _*this_ by another number_t object _x_, _r_ is the remainder
```C++
number_t& div(const number_t& x);
number_t& div(const number_t& x, number_t& r);
```
Divide _*this_ by _x_ (_x_ is an unit)
```
unit_t div_unit(unit_t x);
unit_t div_unit(const UDM& x);
```
Divide _*this_ by _x_ (_x_ is an ordinary integer)
```C++
number_t& div_ui(word_t x);
number_t& div_si(sword_t x);
number_t& div(int x);
number_t& div(unsigned int x);
number_t& div(long x);
number_t& div(unsigned long x);
number_t& div(long long x);
number_t& div(unsigned long long x);
number_t& div_unit(unit_t x);
```

##运算符
```C++
number_t& number_t::operator /= (const number_t& x);
number_t& number_t::operator /= (int x);
number_t& number_t::operator /= (unsigned int x);
number_t& number_t::operator /= (long x);
number_t& number_t::operator /= (unsigned long x);
number_t& number_t::operator /= (long long x);
number_t& number_t::operator /= (unsigned long long x);

number_t operator / (const number_t& a, const number_t& b);
number_t operator / (const number_t& a, bool b);
number_t operator / (bool a, const number_t& b);
number_t operator / (const number_t& a, char b);
number_t operator / (char a, const number_t& b);
number_t operator / (const number_t& a, short b);
number_t operator / (short a, const number_t& b);
number_t operator / (const number_t& a, int b);
number_t operator / (int a, const number_t& b);
number_t operator / (const number_t& a, long b);
number_t operator / (long a, const number_t& b);
number_t operator / (const number_t& a, long long b);
number_t operator / (long long a, const number_t& b);
number_t operator / (const number_t& a, unsigned char b);
number_t operator / (unsigned char a, const number_t& b);
number_t operator / (const number_t& a, unsigned short b);
number_t operator / (unsigned short a, const number_t& b);
number_t operator / (const number_t& a, unsigned int b);
number_t operator / (unsigned int a, const number_t& b);
number_t operator / (const number_t& a, unsigned long b);
number_t operator / (unsigned long a, const number_t& b);
number_t operator / (const number_t& a, unsigned long long b);
number_t operator / (unsigned long long a, const number_t& b);
```

##用乘法作除法

众所周知, 整数除法指令的执行效率相比于乘法指令是相当低的，往往是乘法指令的数倍，幸运地是，根据Torbjorn Granlund和Peter L. Montgomery的论文"[Division by Invariant Integers using Multiplication](https://github.com/brotherbeer/mydocument/blob/master/mynum/resource/divcnst-pldi94.pdf)", 可以将除法转为除数倒数相关的乘法。

如果除数是一个计算单元，可用UDM类获取除数的倒数，再进行除法，如：
```C++
number_t a("1234567890");
unit_t d = 123;
UDM udm(d);  // UDM: Unit Divisor to Multiplier
a.div_unit(udm); // 比直接调用a.div_unit(d)快
```
当大整数对象的值比较大时，利用UDM的除法明显比直接除法快。如果除数是可预见的，则其对应的UDM对象是可重用的。

##注意事项

如果除数为0，将不做任何计算，所以最好在做除法之前检查除数是否为0
