模运算
-------------

##Functions
Set _r_ to _a_ % _b_,
if b is zero, return 0, otherwise return 1
```C++
int mod(const number_t& a, const number_t& b, number_t& r);
```

Set _res_ to _a_ % _x_ (_x_ is a basic type variable)
```C++
void mod(const number_t& a, int x, number_t& res);
void mod(const number_t& a, unsigned int x, number_t& res);
void mod(const number_t& a, long x, number_t& res);
void mod(const number_t& a, unsigned long x, number_t& res);
void mod(const number_t& a, long long x, number_t& res);
void mod(const number_t& a, unsigned long long x, number_t& res);
```

Set _res_ to _x_ % _a_ (_x_ is a basic type variable)
```C++
void mod(int x, const number_t& b, number_t& res);
void mod(unsigned int x, const number_t& b, number_t& res);
void mod(long x, const number_t& b, number_t& res);
void mod(unsigned long x, const number_t& b, number_t& res);
void mod(long long x, const number_t& b, number_t& res);
void mod(unsigned long long x, const number_t& b, number_t& res);
```

Return the result
```C++
number_t mod(const number_t& a, const number_t& b);
```

##Member Functions
```C++
number_t& number_t::mod(const number_t&);
number_t& number_t::mod_ui(word_t);
number_t& number_t::mod_si(sword_t);
number_t& number_t::mod(int x);
number_t& number_t::mod(unsigned int x);
number_t& number_t::mod(long x);
number_t& number_t::mod(unsigned long x);
number_t& number_t::mod(long long x);
number_t& number_t::mod(unsigned long long x);
number_t& number_t::mod_unit(unit_t);
```

##Operators overloaded
```C++
number_t& number_t::operator %= (const number_t& x);
number_t& number_t::operator %= (int x);
number_t& number_t::operator %= (unsigned int x);
number_t& number_t::operator %= (long x);
number_t& number_t::operator %= (unsigned long x);
number_t& number_t::operator %= (long long x);
number_t& number_t::operator %= (unsigned long long x);

number_t operator % (const number_t& a, const number_t& b);
number_t operator % (const number_t& a, bool b);
number_t operator % (bool a, const number_t& b);
number_t operator % (const number_t& a, char b);
number_t operator % (char a, const number_t& b);
number_t operator % (const number_t& a, short b);
number_t operator % (short a, const number_t& b);
number_t operator % (const number_t& a, int b);
number_t operator % (int a, const number_t& b);
number_t operator % (const number_t& a, long b);
number_t operator % (long a, const number_t& b);
number_t operator % (const number_t& a, long long b);
number_t operator % (long long a, const number_t& b);
number_t operator % (const number_t& a, unsigned char b);
number_t operator % (unsigned char a, const number_t& b);
number_t operator % (const number_t& a, unsigned short b);
number_t operator % (unsigned short a, const number_t& b);
number_t operator % (const number_t& a, unsigned int b);
number_t operator % (unsigned int a, const number_t& b);
number_t operator % (const number_t& a, unsigned long b);
number_t operator % (unsigned long a, const number_t& b);
number_t operator % (const number_t& a, unsigned long long b);
number_t operator % (unsigned long long a, const number_t& b);
```