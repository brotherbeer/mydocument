Division
-------------

##Functions

Set a / b to q, and a % b to r. If b is 0, the functions return 0, otherwise return 1
```C++
int div(const number_t& a, const number_t& b, number_t& q, number_t& r);
int div(const number_t& a, const number_t& b, number_t& q);
```

Set a / x to res
```C++
void div(const number_t& a, int x, number_t& res);
void div(const number_t& a, unsigned int x, number_t& res);
void div(const number_t& a, long x, number_t& res);
void div(const number_t& a, unsigned long x, number_t& res);
void div(const number_t& a, long long x, number_t& res);
void div(const number_t& a, unsigned long long x, number_t& res);
```

Set x / b to res
```C++
void div(int x, const number_t& b, number_t& res);
void div(unsigned int x, const number_t& b, number_t& res);
void div(long x, const number_t& b, number_t& res);
void div(unsigned long x, const number_t& b, number_t& res);
void div(long long x, const number_t& b, number_t& res);
void div(unsigned long long x, const number_t& b, number_t& res);
```

Return a / b
```C++
number_t div(const number_t& a, const number_t& b);
```

##Member functions

Divide *this by o, r is the remainder
```C++
number_t& number_t::div(const number_t& o);
number_t& number_t::div(const number_t& o, number_t& r);
```

Divide *this by x (a basic type variable)
```C++
number_t& number_t::div_ui(word_t x);
number_t& number_t::div_si(sword_t x);
number_t& number_t::div(int x);
number_t& number_t::div(unsigned int x);
number_t& number_t::div(long x);
number_t& number_t::div(unsigned long x);
number_t& number_t::div(long long x);
number_t& number_t::div(unsigned long long x);
number_t& number_t::div_unit(unit_t x);
```

Operators overloaded
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

##Attentions

If the divisor is zero, mynum will not do the calculation, so you would better check the divisor before call the division functions.

