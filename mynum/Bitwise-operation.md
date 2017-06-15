<h1>Bitwise operation</h1>

 * [Functions](#functions)
 * [Member functions](#memberfunctions)
 * [Operators overloaded](#operatorsoverloaded)

<h2 id="functions">Functions</h2>

<h3>Shift operation</h3>

Right shift, _res_ is equivalent to multiply _a_ by _2<sup>b</sup>_
```C++
void shr(const number_t& a, size_t b, number_t& res);
```

Left shift, _res_ is equivalent to divide _a_ by _2<sup>b</sup>_
```C++
void shl(const number_t& a, size_t b, number_t& res);
```

<h3>Bitwise AND, OR, XOR, NOT</h3>

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

Bitwise operation with unit
```C++
void bit_and_unit(const number_t& a, unit_t x, number_t& res);
void bit_or_unit(const number_t& a, unit_t x, number_t& res);
void bit_xor_unit(const number_t& a, unit_t x, number_t& res);
```

Set _res_ to _a_ ^ (_b_ << _shift_),  
But this function is faster than use the expression
```C++
void bit_shift_xor(const number_t& a, const number_t& b, size_t shift, number_t& res);
```

Set _res_ to _a_ | (_b_ << _shift_),  
But this function is faster than use the expression
```C++
void bit_shift_or(const number_t& a, const number_t& b, size_t shift, number_t& res);
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

<h2 id="memberfunctions">Member functions</h2>

Return the value of the bit at position _pos_, the position of the least significant bit is 0, and the positions of other bits are successively increasing
```C++
bool number_t::bit_at(size_t pos) const;
bool number_t::operator [] (size_t pos) const;
```

Set the bit at position _pos_ or the bits within the rang [_bpos_, _epos_) to 1
```C++
number_t& number_t::bit_set_one(size_t pos);
number_t& number_t::bit_set_one(size_t bpos, size_t epos);
```

Set the bit at position _pos_ or the bits within the rang [_bpos_, _epos_) to 0
```C++
number_t& number_t::bit_set_zero(size_t pos);
number_t& number_t::bit_set_zero(size_t bpos, size_t epos);
```

Flip the bit at position _pos_ or the bits within the rang [_bpos_, _epos_), i.e., 1 to 0 or 0 to 1
```C++
number_t& number_t::bit_set_flip(size_t pos);
number_t& number_t::bit_set_flip(size_t bpos, size_t epos);
```

Set the bit at position _pos_ or the bits within the rang [_bpos_, _epos_) to _v_,  
_v_ may be 0, 1 or -1, if v is -1, then flip the bits
```C++
number_t& number_t::bit_set(size_t pos, int v);
number_t& number_t::bit_set(size_t bpos, size_t epos, int v);
```

Remove the bits within the range [bpos, epos)
```C++
number_t& number_t::bit_remove(size_t bpos, size_t epos);
```

Insert bits at position _pos_, _v_ is the value
```C++
number_t& number_t::bit_insert(size_t pos, size_t size, bool v);
```

Return the number of the significant bits, if _*this_ < 0
```C++
size_t number_t::bits_count() const;
```

Return the trailing 0 bits count, starting at the least significant bit position
```C++
size_t number_t::tz_count() const;
```

Return the population count, i.e., the number of 1 bits
```C++
size_t number_t::pop_count() const;
```

Allocate at least n bits memory
```C++
void number_t::bits_reserve(size_t n);
```

Shift
```C++
number_t& number_t::shr(size_t);
number_t& number_t::shl(size_t);
```

Bitwise or, and, xor, not
```C++
number_t& number_t::bit_or(const number_t&);
number_t& number_t::bit_and(const number_t&);
number_t& number_t::bit_xor(const number_t&);
number_t& number_t::bit_not();
```

Bitwise operation with ordinary integer
```C++
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
```

Bitwise operation with unit
```C++
void number_t::bit_and_unit(unit_t);
void number_t::bit_or_unit(unit_t);
void number_t::bit_xor_unit(unit_t);
```

Bitwise operation with word
```C++
void number_t::bit_and_word(word_t);
void number_t::bit_or_word(word_t);
void number_t::bit_xor_word(word_t);
void number_t::bit_and_sword(sword_t);
void number_t::bit_or_sword(sword_t);
void number_t::bit_xor_sword(sword_t);
```

<h2 id="operatorsoverloaded">Operators overloaded</h2>

Defined in [myoperators.h](https://github.com/brotherbeer/mynum/blob/master/myoperators.h)

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
