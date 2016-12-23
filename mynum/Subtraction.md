Subtraction
-------------

##Functions

Set res to a - b
```C++
void sub(const number_t& a, const number_t& b, number_t& res);
```

Set res to a - x (x is a basic type variable)
```C++
void sub(const number_t& a, int x, number_t& res);
void sub(const number_t& a, unsigned int x, number_t& res);
void sub(const number_t& a, long x, number_t& res);
void sub(const number_t& a, unsigned long x, number_t& res);
void sub(const number_t& a, long long x, number_t& res);
void sub(const number_t& a, unsigned long long x, number_t& res);
```

Set res to x - b (x is a basic type variable)
```C++
void sub(int x, const number_t& b, number_t& res);
void sub(unsigned int x, const number_t& b, number_t& res);
void sub(long x, const number_t& b, number_t& res);
void sub(unsigned long x, const number_t& b, number_t& res);
void sub(long long x, const number_t& b, number_t& res);
void sub(unsigned long long x, const number_t& b, number_t& res);
```
Return a - b
```C++
number_t sub(const number_t& a, const number_t& b);
```

##Member functions

Sub *this with o
```C++
number_t& sub(const number_t& o);
```

Sub *this with a basic type variable
```C++
number_t& number_t::sub(int x);
number_t& number_t::sub(unsigned int x);
number_t& number_t::sub(long x);
number_t& number_t::sub(unsigned long x);
number_t& number_t::sub(long long x);
number_t& number_t::sub(unsigned long long x);

number_t& number_t::sub_ui(word_t);
number_t& number_t::sub_si(sword_t);
number_t& number_t::sub_unit(unit_t);
```

##Operators overloaded
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
