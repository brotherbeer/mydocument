Multiplication
-------------

 * [Functions](#Functions)
 * [Member functions](#Member-functions)
 * [Operators overloaded](#Operators-overloaded)
 * [NTT class](#NTT-class)

##Functions

Set _res_ to _a_ \* _b_, using basic algorithm
```C++
void mul(const number_t& a, const number_t& b, number_t& res);
```

Set _res_ to _a_ \* _b_, using Karatsuba algorithm  
```C++
void kmul(const number_t& a, const number_t& b, number_t& res);
```

Set _res_ to _a_ \* _b_, using NTT(Number Theoretic Transform) algorithm
```C++
void fmul(const number_t& a, const number_t& b, number_t& res);
```

Set _res_ to _a_ \* _x_, _x_ is an unit
```C++
void mul_unit(const number_t& a, unit_t x, number_t& res);
```

Set _res_ to _a_ \* _x_ (_x_ is an ordinary integer)
```C++
void mul(const number_t& a, int x, number_t& res);
void mul(const number_t& a, unsigned int x, number_t& res);
void mul(const number_t& a, long x, number_t& res);
void mul(const number_t& a, unsigned long x, number_t& res);
void mul(const number_t& a, long long x, number_t& res);
void mul(const number_t& a, unsigned long long x, number_t& res);
```

Set _res_ to _x_ \* _a_ (_x_ is an ordinary integer)
```C++
void mul(int x, const number_t& a, number_t& res);
void mul(unsigned int x, const number_t& a, number_t& res);
void mul(long x, const number_t& a, number_t& res);
void mul(unsigned long x, const number_t& a, number_t& res);
void mul(long long x, const number_t& a, number_t& res);
void mul(unsigned long long x, const number_t& a, number_t& res);
```

Set _res_ to _a<sup>2</sup>_, using basic algorithm  
```C++
void sqr(const number_t& a, number_t& res);
```

Set _res_ to _a<sup>2</sup>_, using Karatsuba algorithm  
```C++
void ksqr(const number_t& a, number_t& res);
```

Set _res_ to _a<sup>2</sup>_, using NTT(Number Theoretic Transform) algorithm
```C++
void fsqr(const number_t& a, number_t& res);
```

##Member functions

Multiply _*this_ by another number_t object _x_
```C++
number_t& number_t::mul(const number_t& x);
number_t& number_t::kmul(const number_t& x);
```
Multiply _*this_ by an unit
```C++
void number_t::mul_unit(unit_t x);
```
Multiply _*this_ with a word type variable
```C++
void number_t::mul_word(word_t x);
void number_t::mul_sword(sword_t x);
```
Multiply _*this_ by an ordinary integer
```C++
number_t& number_t::mul(int x);
number_t& number_t::mul(unsigned int x);
number_t& number_t::mul(long x);
number_t& number_t::mul(unsigned long x);
number_t& number_t::mul(long long x);
number_t& number_t::mul(unsigned long long x);
```

##Operators overloaded
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

##NTT class
