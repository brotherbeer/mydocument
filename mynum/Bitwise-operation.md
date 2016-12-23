Bitwise operation
-------------

##Functions

Right shift, _res_ is equivalent to multiply _a_ by _2<sup>b</sup>_
```C++
void shr(const number_t& a, size_t b, number_t& res);
```

Left shift, _res_ is equivalent to divide _a_ by _2<sup>b</sup>_
```C++
void shl(const number_t& a, size_t b, number_t& res);
```

Return the value on the _n_-th bit
```C++
bool number_t::bit_at(size_t n) const;
bool number_t::operator [] (size_t n) const;
```

Set the value on the _n_-th bit
```C++
void number_t::bit_set(size_t n, bool v = 1);
void number_t::bit_set_one(size_t n);
void number_t::bit_set_zero(size_t n);
bitref_t number_t::operator [] (size_t n);
```

Return the bits count
```C++
size_t number_t::bits_count() const;
```

Allocate at least n bits memory
```C++
void number_t::bits_reserve(size_t n);
```

Bitwise AND, OR, XOR, NOT

The sign of the big integers here is of little significance. mynum stipulates that if the operands have the same sign, the result is positive, otherwise the result is negative. 

```C++
void bit_and(const number_t& a, const number_t& b, number_t& res);
void bit_or(const number_t& a, const number_t& b, number_t& res);
void bit_xor(const number_t& a, const number_t& b, number_t& res);
void bit_not(const number_t& a, number_t& res);

void bit_and(const number_t& a, int x, number_t& res);
void bit_and(const number_t& a, unsigned int x, number_t& res);
void bit_and(const number_t& a, long x, number_t& res);
void bit_and(const number_t& a, unsigned long x, number_t& res);
void bit_and(const number_t& a, long long x, number_t& res);
void bit_and(const number_t& a, unsigned long long x, number_t& res);
void bit_and(int x, const number_t& b, number_t& res);
void bit_and(unsigned int x, const number_t& b, number_t& res);
void bit_and(long x, const number_t& b, number_t& res);
void bit_and(unsigned long x, const number_t& b, number_t& res);
void bit_and(long long x, const number_t& b, number_t& res);
void bit_and(unsigned long long x, const number_t& b, number_t& res);

void bit_or(const number_t& a, int x, number_t& res);
void bit_or(const number_t& a, unsigned int x, number_t& res);
void bit_or(const number_t& a, long x, number_t& res);
void bit_or(const number_t& a, unsigned long x, number_t& res);
void bit_or(const number_t& a, long long x, number_t& res);
void bit_or(const number_t& a, unsigned long long x, number_t& res);
void bit_or(int x, const number_t& b, number_t& res);
void bit_or(unsigned int x, const number_t& b, number_t& res);
void bit_or(long x, const number_t& b, number_t& res);
void bit_or(unsigned long x, const number_t& b, number_t& res);
void bit_or(long long x, const number_t& b, number_t& res);
void bit_or(unsigned long long x, const number_t& b, number_t& res);

void bit_xor(const number_t& a, int x, number_t& res);
void bit_xor(const number_t& a, unsigned int x, number_t& res);
void bit_xor(const number_t& a, long x, number_t& res);
void bit_xor(const number_t& a, unsigned long x, number_t& res);
void bit_xor(const number_t& a, long long x, number_t& res);
void bit_xor(const number_t& a, unsigned long long x, number_t& res);
void bit_xor(int x, const number_t& b, number_t& res);
void bit_xor(unsigned int x, const number_t& b, number_t& res);
void bit_xor(long x, const number_t& b, number_t& res);
void bit_xor(unsigned long x, const number_t& b, number_t& res);
void bit_xor(long long x, const number_t& b, number_t& res);
void bit_xor(unsigned long long x, const number_t& b, number_t& res);
```

Result as return value
```C++
number_t shr(const number_t& a, size_t b);
number_t shl(const number_t& a, size_t b);
number_t bit_and(const number_t& a, const number_t& b);
number_t bit_or(const number_t& a, const number_t& b);
number_t bit_xor(const number_t& a, const number_t& b);
number_t bit_not(const number_t& a);
```

##Member functions
```C++
number_t& number_t::shr(size_t);
number_t& number_t::shl(size_t);

number_t& number_t::bit_or(const number_t&);
number_t& number_t::bit_and(const number_t&);
number_t& number_t::bit_xor(const number_t&);
number_t& number_t::bit_not();
number_t& number_t::bit_and_ui(word_t);
number_t& number_t::bit_or_ui(word_t);
number_t& number_t::bit_xor_ui(word_t);
number_t& number_t::bit_and_si(sword_t);
number_t& number_t::bit_or_si(sword_t);
number_t& number_t::bit_xor_si(sword_t);

number_t& number_t::bit_and(int x);
number_t& number_t::bit_and(unsigned int x);
number_t& number_t::bit_and(long x);
number_t& number_t::bit_and(unsigned long x);
number_t& number_t::bit_and(long long x);
number_t& number_t::bit_and(unsigned long long x);
number_t& number_t::bit_or(int x);
number_t& number_t::bit_or(unsigned int x);
number_t& number_t::bit_or(long x);
number_t& number_t::bit_or(unsigned long x);
number_t& number_t::bit_or(long long x);
number_t& number_t::bit_or(unsigned long long x);
number_t& number_t::bit_xor(int x);
number_t& number_t::bit_xor(unsigned int x);
number_t& number_t::bit_xor(long x);
number_t& number_t::bit_xor(unsigned long x);
number_t& number_t::bit_xor(long long x);
number_t& number_t::bit_xor(unsigned long long x);

number_t& number_t::bit_and_unit(unit_t);
number_t& number_t::bit_or_unit(unit_t);
number_t& number_t::bit_xor_unit(unit_t);
```

Operators overloaded
```C++
number_t  number_t::operator ~ () const;
number_t& number_t::operator &= (const number_t& x);
number_t& number_t::operator |= (const number_t& x);
number_t& number_t::operator ^= (const number_t& x);
number_t& number_t::operator &= (int x);
number_t& number_t::operator |= (int x);
number_t& number_t::operator ^= (int x);
number_t& number_t::operator &= (unsigned int x);
number_t& number_t::operator |= (unsigned int x);
number_t& number_t::operator ^= (unsigned int x);
number_t& number_t::operator &= (long x);
number_t& number_t::operator |= (long x);
number_t& number_t::operator ^= (long x);
number_t& number_t::operator &= (unsigned long x);
number_t& number_t::operator |= (unsigned long x);
number_t& number_t::operator ^= (unsigned long x);
number_t& number_t::operator &= (long long x);
number_t& number_t::operator |= (long long x);
number_t& number_t::operator ^= (long long x);
number_t& number_t::operator &= (unsigned long long x);
number_t& number_t::operator |= (unsigned long long x);
number_t& number_t::operator ^= (unsigned long long x);
number_t& number_t::operator <<= (size_t x);
number_t& number_t::operator >>= (size_t x);

number_t operator & (const number_t& a, const number_t& b);
number_t operator & (const number_t& a, bool b);
number_t operator & (bool a, const number_t& b);
number_t operator & (const number_t& a, char b);
number_t operator & (char a, const number_t& b);
number_t operator & (const number_t& a, short b);
number_t operator & (short a, const number_t& b);
number_t operator & (const number_t& a, int b);
number_t operator & (int a, const number_t& b);
number_t operator & (const number_t& a, long b);
number_t operator & (long a, const number_t& b);
number_t operator & (const number_t& a, long long b);
number_t operator & (long long a, const number_t& b);
number_t operator & (const number_t& a, unsigned char b);
number_t operator & (unsigned char a, const number_t& b);
number_t operator & (const number_t& a, unsigned short b);
number_t operator & (unsigned short a, const number_t& b);
number_t operator & (const number_t& a, unsigned int b);
number_t operator & (unsigned int a, const number_t& b);
number_t operator & (const number_t& a, unsigned long b);
number_t operator & (unsigned long a, const number_t& b);
number_t operator & (const number_t& a, unsigned long long b);
number_t operator & (unsigned long long a, const number_t& b);

number_t operator | (const number_t& a, const number_t& b);
number_t operator | (const number_t& a, bool b);
number_t operator | (bool a, const number_t& b);
number_t operator | (const number_t& a, char b);
number_t operator | (char a, const number_t& b);
number_t operator | (const number_t& a, short b);
number_t operator | (short a, const number_t& b);
number_t operator | (const number_t& a, int b);
number_t operator | (int a, const number_t& b);
number_t operator | (const number_t& a, long b);
number_t operator | (long a, const number_t& b);
number_t operator | (const number_t& a, long long b);
number_t operator | (long long a, const number_t& b);
number_t operator | (const number_t& a, unsigned char b);
number_t operator | (unsigned char a, const number_t& b);
number_t operator | (const number_t& a, unsigned short b);
number_t operator | (unsigned short a, const number_t& b);
number_t operator | (const number_t& a, unsigned int b);
number_t operator | (unsigned int a, const number_t& b);
number_t operator | (const number_t& a, unsigned long b); 
number_t operator | (unsigned long a, const number_t& b);
number_t operator | (const number_t& a, unsigned long long b);
number_t operator | (unsigned long long a, const number_t& b);

number_t operator ^ (const number_t& a, const number_t& b);
number_t operator ^ (const number_t& a, bool b);
number_t operator ^ (bool a, const number_t& b);
number_t operator ^ (const number_t& a, char b);
number_t operator ^ (char a, const number_t& b);
number_t operator ^ (const number_t& a, short b);
number_t operator ^ (short a, const number_t& b);
number_t operator ^ (const number_t& a, int b);
number_t operator ^ (int a, const number_t& b);
number_t operator ^ (const number_t& a, long b);
number_t operator ^ (long a, const number_t& b);
number_t operator ^ (const number_t& a, long long b);
number_t operator ^ (long long a, const number_t& b);
number_t operator ^ (const number_t& a, unsigned char b);
number_t operator ^ (unsigned char a, const number_t& b);
number_t operator ^ (const number_t& a, unsigned short b);
number_t operator ^ (unsigned short a, const number_t& b);
number_t operator ^ (const number_t& a, unsigned int b);
number_t operator ^ (unsigned int a, const number_t& b);
number_t operator ^ (const number_t& a, unsigned long b); 
number_t operator ^ (unsigned long a, const number_t& b);
number_t operator ^ (const number_t& a, unsigned long long b);
number_t operator ^ (unsigned long long a, const number_t& b);

number_t operator << (const number_t& a, int b);
number_t operator >> (const number_t& a, int b);
number_t operator << (const number_t& a, long b);
number_t operator >> (const number_t& a, long b);
number_t operator << (const number_t& a, unsigned int b);
number_t operator >> (const number_t& a, unsigned int b);
number_t operator << (const number_t& a, unsigned long b);
number_t operator >> (const number_t& a, unsigned long b);
number_t operator << (const number_t& a, const number_t& b);
number_t operator >> (const number_t& a, const number_t& b);
#if UNITBITS == 32
number_t operator << (const number_t& a, long long b);
number_t operator >> (const number_t& a, long long b);
number_t operator << (const number_t& a, unsigned long long b);
number_t operator >> (const number_t& a, unsigned long long b);
#endif
```

UNITBITS is a macro that indicates the bits count in an unit, if UNITBITS is 32, that means current environment is 64-bit, see [The data storage model of mynum](https://github.com/brotherbeer/mydocument/blob/master/mynum/Storage.md)
