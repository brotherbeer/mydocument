Division
-------------

 * [Global functions](#global-functions)
 * [Number_t members](#number_t-members)
 * [Operators overloaded](#operators-overloaded)
 * [Do the division via multiplication](#do-the-division-via-multiplication)
 * [Attentions](#attentions)

##Global functions

Set _a_ / _b_ to _q_, and _a_ % _b_ to _r_. If _b_ is 0, the functions return 0, otherwise return 1
```C++
int div(const number_t& a, const number_t& b, number_t& q, number_t& r);
int div(const number_t& a, const number_t& b, number_t& q);
```

Set _a_ / _x_ to _res_, the divisor _x_ is an unit, return the absolute value of the remainder
```C++
unit_t div_unit(const number_t& a, unit_t x, number_t& res);
```

_udm_ is the reciprocal of the divisor, use multiplication to do the division, return the absolute value of the remainder
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

##Number_t members

Divide _*this_ by another number_t object _x_, _r_ is the remainder
```C++
number_t& div(const number_t& x);
number_t& div(const number_t& x, number_t& r);
```
Divide _*this_ by an unit  
Return the absolute value of the remainder
```
unit_t div_unit(unit_t x);
unit_t div_unit(const UDM& x);
```
Divide _*this_ by a word or a signed word   
Return the absolute value of the remainder
```C++
word_t div_word(word_t x);
word_t div_sword(sword_t x);
```
Divide _*this_ by _x_ (_x_ is an ordinary integer)
```C++
number_t& div(int x);
number_t& div(unsigned int x);
number_t& div(long x);
number_t& div(unsigned long x);
number_t& div(long long x);
number_t& div(unsigned long long x);
number_t& div_unit(unit_t x);
```

##Operators overloaded
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

##Do the division via multiplication

As well known, the cost of an integer division is several times that of an integer multiplication.  
But fortunately, according to "[Division by Invariant Integers using Multiplication](https://github.com/brotherbeer/mydocument/blob/master/mynum/resource/divcnst-pldi94.pdf)" Torbjorn Granlund and Peter L. Montgomery, we can convert the division to the multiplication by the reciprocal of the divisor.

If the divisor is a unit, we can use `UDM` class to derive the reciprocal of the divisor.
```C++
number_t a("1234567890");
unit_t d = 123;
UDM udm(d);  // UDM: Unit Divisor to Multiplier
a.div_unit(udm); // faster than calling a.div_unit(d) directly
```
When the value of a number_t object is large, the division using UDM is much faster. If the divisors are predictable, the corresponding UDM objects can be reused. 

##Attentions

If the divisor is zero, mynum will not do the calculation, so you would better check the divisor before call the division functions.

