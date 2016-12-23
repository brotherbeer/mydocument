Addition
-------------

##Functions

Set res to a + b
```C++
void add(const number_t& a, const number_t& b, number_t& res);
```

Set res to a + x (x is a basic type variable)
```C++
void add(const number_t& a, int x, number_t& res);
void add(const number_t& a, unsigned int x, number_t& res);
void add(const number_t& a, long x, number_t& res);
void add(const number_t& a, unsigned long x, number_t& res);
void add(const number_t& a, long long x, number_t& res);
void add(const number_t& a, unsigned long long x, number_t& res);
```

Set res to x + b (x is a basic type variable)
```C++
void add(int x, const number_t& b, number_t& res);
void add(unsigned int x, const number_t& b, number_t& res);
void add(long x, const number_t& b, number_t& res);
void add(unsigned long x, const number_t& b, number_t& res);
void add(long long x, const number_t& b, number_t& res);
void add(unsigned long long x, const number_t& b, number_t& res);
```

Return a + b
```C++
number_t add(const number_t& a, const number_t& b);
```

##Member functions

Add *this with o
```C++
number_t& number_t::add(const number_t& o);
```

Add *this with a basic type variable
```C++
number_t& number_t::add(int x);
number_t& number_t::add(unsigned int x);
number_t& number_t::add(long x);
number_t& number_t::add(unsigned long x);
number_t& number_t::add(long long x);
number_t& number_t::add(unsigned long long x);
```

Add *this with a word type variable
```C++
number_t& number_t::add_ui(word_t);
number_t& number_t::add_si(sword_t);
```

Add *this with a unit
```C++
number_t& number_t::add_unit(unit_t);
```

##Operators overloaded
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
