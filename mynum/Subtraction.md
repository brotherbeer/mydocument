<h1>Subtraction</h1>

 * [Functions](#functions)
 * [Member functions](#memberfunctions)
 * [Operators overloaded](#operatorsoverloaded)

<h2 id="functions">Functions</h2>

Set _res_ to _a_ - _b_
```C++
void sub(const number_t& a, const number_t& b, number_t& res);
```

Set _res_ to _a_ - _x_, _x_ is an unit.
```C++
void sub_unit(const number_t& a, unit_t x, number_t& res);
```

Set _res_ to _a_ - _x_ (_x_ is an ordinary integer)
```C++
void sub(const number_t& a, int x, number_t& res);
void sub(const number_t& a, unsigned int x, number_t& res);
void sub(const number_t& a, long x, number_t& res);
void sub(const number_t& a, unsigned long x, number_t& res);
void sub(const number_t& a, long long x, number_t& res);
void sub(const number_t& a, unsigned long long x, number_t& res);
```

Set _res_ to _x_ - _a_ (_x_ is an ordinary integer)
```C++
void sub(int x, const number_t& a, number_t& res);
void sub(unsigned int x, const number_t& a, number_t& res);
void sub(long x, const number_t& a, number_t& res);
void sub(unsigned long x, const number_t& a, number_t& res);
void sub(long long x, const number_t& a, number_t& res);
void sub(unsigned long long x, const number_t& a, number_t& res);
```
Return _a_ - _b_
```C++
number_t sub(const number_t& a, const number_t& b);
```

<h2 id="memberfunctions">Member functions</h2>

Sub _*this_ with another number_t object _x_
```C++
number_t& sub(const number_t& x);
```
Sub _*this_ with a unit
```C++
void number_t::sub_unit(unit_t x);
```
Sub _*this_ with a word type variable
```C++
void number_t::sub_word(word_t x);
void number_t::sub_sword(sword_t x);
```
Sub _*this_ with an ordinary integer
```C++
number_t& number_t::sub(int x);
number_t& number_t::sub(unsigned int x);
number_t& number_t::sub(long x);
number_t& number_t::sub(unsigned long x);
number_t& number_t::sub(long long x);
number_t& number_t::sub(unsigned long long x);
```

<h2 id="operatorsoverloaded">Operators overloaded</h2>

Member operators

```C++
number_t& number_t::operator -- ();
number_t& number_t::operator -- (int);
number_t& number_t::operator -= (const number_t& x);
number_t& number_t::operator -= (int x);
number_t& number_t::operator -= (unsigned int x);
number_t& number_t::operator -= (long x);
number_t& number_t::operator -= (unsigned long x);
number_t& number_t::operator -= (long long x);
number_t& number_t::operator -= (unsigned long long x);
```

Global operators  
Defined in [myoperators.h](https://github.com/brotherbeer/mynum/blob/master/myoperators.h)

```C++
number_t operator - (const number_t& a, const number_t& b);
number_t operator - (const number_t& a, bool b);
number_t operator - (bool a, const number_t& b);
number_t operator - (const number_t& a, char b);
number_t operator - (char a, const number_t& b);
number_t operator - (const number_t& a, short b);
number_t operator - (short a, const number_t& b);
number_t operator - (const number_t& a, int b);
number_t operator - (int a, const number_t& b);
number_t operator - (const number_t& a, long b);
number_t operator - (long a, const number_t& b);
number_t operator - (const number_t& a, long long b);
number_t operator - (long long a, const number_t& b);
number_t operator - (const number_t& a, unsigned char b);
number_t operator - (unsigned char a, const number_t& b);
number_t operator - (const number_t& a, unsigned short b);
number_t operator - (unsigned short a, const number_t& b);
number_t operator - (const number_t& a, unsigned int b);
number_t operator - (unsigned int a, const number_t& b);
number_t operator - (const number_t& a, unsigned long b);
number_t operator - (unsigned long a, const number_t& b);
number_t operator - (const number_t& a, unsigned long long b);
number_t operator - (unsigned long long a, const number_t& b);
```
