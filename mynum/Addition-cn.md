<h1>加法</h1>

 * [函数](#functions)
 * [成员函数](#memberfunctions)
 * [运算符](#operatorsoverloaded)

<h2 id="functions">函数</h2>

Set _res_ to _a_ + _b_
```C++
void add(const number_t& a, const number_t& b, number_t& res);
```

Set _res_ to _a_ + _x_, _x_ is an unit.
```C++
void add_unit(const number_t& a, unit_t x, number_t& res);
```

Set _res_ to _a_ + _x_ (_x_ is an ordinary integer)
```C++
void add(const number_t& a, int x, number_t& res);
void add(const number_t& a, unsigned int x, number_t& res);
void add(const number_t& a, long x, number_t& res);
void add(const number_t& a, unsigned long x, number_t& res);
void add(const number_t& a, long long x, number_t& res);
void add(const number_t& a, unsigned long long x, number_t& res);
```

Set _res_ to _x_ + _a_ (_x_ is an ordinary integer)
```C++
void add(int x, const number_t& a, number_t& res);
void add(unsigned int x, const number_t& a, number_t& res);
void add(long x, const number_t& a, number_t& res);
void add(unsigned long x, const number_t& a, number_t& res);
void add(long long x, const number_t& a, number_t& res);
void add(unsigned long long x, const number_t& a, number_t& res);
```

Return _a_ + _b_
```C++
number_t add(const number_t& a, const number_t& b);
```

<h2 id="memberfunctions">成员函数</h2>

Add _*this_ with another number_t object _x_
```C++
number_t& number_t::add(const number_t& x);
```
Add _*this_ with a unit
```C++
void number_t::add_unit(unit_t x);
```
Add _*this_ with a word type variable
```C++
void number_t::add_word(word_t x);
void number_t::add_sword(sword_t x);
```
Add _*this_ with an ordinary integer
```C++
number_t& number_t::add(int x);
number_t& number_t::add(unsigned int x);
number_t& number_t::add(long x);
number_t& number_t::add(unsigned long x);
number_t& number_t::add(long long x);
number_t& number_t::add(unsigned long long x);
```

<h2 id="operatorsoverloaded">运算符</h2>

```C++
number_t& number_t::operator ++ ();
number_t& number_t::operator ++ (int);
number_t& number_t::operator += (const number_t& x);
number_t& number_t::operator += (int x);
number_t& number_t::operator += (unsigned int x);
number_t& number_t::operator += (long x);
number_t& number_t::operator += (unsigned long x);
number_t& number_t::operator += (long long x);
number_t& number_t::operator += (unsigned long long x);

number_t operator + (const number_t& a, const number_t& b);
number_t operator + (const number_t& a, bool b);
number_t operator + (bool a, const number_t& b);
number_t operator + (const number_t& a, char b);
number_t operator + (char a, const number_t& b);
number_t operator + (const number_t& a, short b);
number_t operator + (short a, const number_t& b);
number_t operator + (const number_t& a, int b);
number_t operator + (int a, const number_t& b);
number_t operator + (const number_t& a, long b);
number_t operator + (long a, const number_t& b);
number_t operator + (const number_t& a, long long b);
number_t operator + (long long a, const number_t& b);
number_t operator + (const number_t& a, unsigned char b);
number_t operator + (unsigned char a, const number_t& b);
number_t operator + (const number_t& a, unsigned short b);
number_t operator + (unsigned short a, const number_t& b);
number_t operator + (const number_t& a, unsigned int b);
number_t operator + (unsigned int a, const number_t& b);
number_t operator + (const number_t& a, unsigned long b);
number_t operator + (unsigned long a, const number_t& b);
number_t operator + (const number_t& a, unsigned long long b);
number_t operator + (unsigned long long a, const number_t& b);
```
