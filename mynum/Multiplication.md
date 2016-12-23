Multiplication
-------------

##Functions

Set res to a * b
kmul uses Karatsuba algorithm
```C++
void mul(const number_t& a, const number_t& b, number_t& res);
void kmul(const number_t& a, const number_t& b, number_t& res);
```

Set res to a * x (x is a basic type variable)
```C++
void mul(const number_t& a, int x, number_t& res);
void mul(const number_t& a, unsigned int x, number_t& res);
void mul(const number_t& a, long x, number_t& res);
void mul(const number_t& a, unsigned long x, number_t& res);
void mul(const number_t& a, long long x, number_t& res);
void mul(const number_t& a, unsigned long long x, number_t& res);
```

Set res to x * b (x is a basic type variable)
```C++
void mul(int x, const number_t& b, number_t& res);
void mul(unsigned int x, const number_t& b, number_t& res);
void mul(long x, const number_t& b, number_t& res);
void mul(unsigned long x, const number_t& b, number_t& res);
void mul(long long x, const number_t& b, number_t& res);
void mul(unsigned long long x, const number_t& b, number_t& res);
```

Return a * b
```C++
number_t mul(const number_t& a, const number_t& b);
number_t kmul(const number_t& a, const number_t& b);
```

##Member functions

Multiply *this by o
```C++
number_t& number_t::mul(const number_t& o);
number_t& number_t::kmul(const number_t& o);
```

Multiply *this by x (a basic type variable)
```C++
number_t& number_t::mul(int x);
number_t& number_t::mul(unsigned int x);
number_t& number_t::mul(long x);
number_t& number_t::mul(unsigned long x);
number_t& number_t::mul(long long x);
number_t& number_t::mul(unsigned long long x);
number_t& number_t::mul_ui(word_t x);
number_t& number_t::mul_si(sword_t x);
number_t& number_t::mul_unit(unit_t x);
```

Operators overloaded
```C++
number_t& number_t::operator *= (const number_t& x);
number_t& number_t::operator *= (int x);
number_t& number_t::operator *= (unsigned int x);
number_t& number_t::operator *= (long x);
number_t& number_t::operator *= (unsigned long x);
number_t& number_t::operator *= (long long x);
number_t& number_t::operator *= (unsigned long long x);

number_t operator * (const number_t& a, const number_t& b);
number_t operator * (const number_t& a, bool b);
number_t operator * (bool a, const number_t& b);
number_t operator * (const number_t& a, char b);
number_t operator * (char a, const number_t& b);
number_t operator * (const number_t& a, short b);
number_t operator * (short a, const number_t& b);
number_t operator * (const number_t& a, int b);
number_t operator * (int a, const number_t& b);
number_t operator * (const number_t& a, long b);
number_t operator * (long a, const number_t& b);
number_t operator * (const number_t& a, long long b);
number_t operator * (long long a, const number_t& b);
number_t operator * (const number_t& a, unsigned char b);
number_t operator * (unsigned char a, const number_t& b);
number_t operator * (const number_t& a, unsigned short b);
number_t operator * (unsigned short a, const number_t& b);
number_t operator * (const number_t& a, unsigned int b);
number_t operator * (unsigned int a, const number_t& b);
number_t operator * (const number_t& a, unsigned long b);
number_t operator * (unsigned long a, const number_t& b);
number_t operator * (const number_t& a, unsigned long long b);
number_t operator * (unsigned long long a, const number_t& b);
```
