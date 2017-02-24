The data storage model of mynum
-------------

_Mynum is currently only available on the LITTLE-ENDIAN machines, which store the least significant byte (LSB) of a word at the lowest memory address, and store the other bytes following in increasing order of significance._

Mynum stores the big integer in binary form, in principle, it is the same as C integer types, but is not limited by the fixed memory size.

For example, the integer 0xabcdef, if it is stored in an int variable and the variable has 4 bytes, the bytes from low address to high address are 0xef, 0xcd, 0xab, 0x00, If construct a number_t object with a value of 0xabcdef, there is an array in the object, the first byte of the array is 0xef, the second is 0xcd, the third is 0xab, the LSB of the integer is stored at the lowest memory address.

There are 3 important member variables in number_t:
```C++
    unit_t* dat;
    slen_t len;
    slen_t cap;
```
and some useful constants:
```C++
const dunit_t BASE = (dunit_t)1 << UNITBITS;
const unit_t  UNITMAX = ~unit_t(0);
```
The **unit_t** is the most basic computing unit type, it is an unsigned integer type, UNITBITS-bit, and the max value is UNITMAX. Hereafter the **unit_t** variable will be abbreviated as unit. The **slen_t** is a signed integer type that represents the length.

Because the number_t object stores the big integer in binary form, so it can be understood as a sequence of units, the member variable _dat_ points to the sequence, the absolute value of _len_ is the count of the valid units in the sequence, _cap_ is the count of all units in the sequence.
When _len_ < 0, the object is negative, when _len_ > 0, the object is positive, and when _len_ = 0, the object is 0.

Obviously, the number_t object can be understood as a number which has _len_ digits and has BASE as its base, the value of the _i_-th digit is the value of the _i_-th unit (_len > i >= 0_).

The **unit_t** is a system related type, on 64-bit systems, it is unsigned int, on 32-bit systems, it is unsigned short. Another example:
Construct a number_t object, and its value is 0xaaaabbbbccccddddeeeeffff,
on 32-bit systems, the unit sequence is 0xffff，0xeeee, 0xdddd, 0xcccc, 0xbbbb, 0xaaaa
on 64-bit systems, the unit sequence is 0xeeeeffff, 0xccccdddd, 0xaaaabbbb

Constructing a number_t object from the string "aaaabbbbccccddddeeeeffff" denoting a hexadecimal number is relatively simple, we will discuss how to construct objects from the strings denoting arbitrary-based numbers in the following chapters.

The size of an unit is a half of a word, if dunit_t is the word type, we can use standard C/C++ to derive the carry or borrow in computing process easily.
```C++
// res = a + b, and return the carry
unit_t add(unit_t a, unit_t b, unit_t& res)
{
    dunit_t sum = (dunit_t)a + b;
    *res = sum & UNITMAX;
    return sum >> UNITBITS;
}

// res = a * b + c, and return the carry
unit_t muladd(unit_t a, unit_t b, unit_t c, unit_t& res)
{
    dunit_t sum = (dunit_t)a * b + c;
    *res = sum & UNITMAX;
    return sum >> UNITBITS;
}
```
0xffff * 0xffff + 0xffff = 0xffff0000, so the data in the functions will not overflow, Similarly in the 64-bit environment it will not overflow too.

Now we can multiplicate or add the number_t object with a unit(ignore the case len < 0, and some details)
```C++
number_t::mul_unit(unit_t x)
{
    unit_t carry = 0;
    for (slen_t i = 0; i < len; i++)
    {
        carry = muladd(dat[i], x, carry, &dat[i]);
    }
    if (carry)
    {
        dat[len++] = carry; // Assume that the memory space is sufficient
    }
}

number_t::add_unit(unit_t x)
{
    unit_t carry = add(dat[0], x, &dat[0])
    for (slen_t i = 1; i < len && carry != 0; i++)
    {
        carry = add(dat[i], carry, &dat[i]);
    }
    if (carry)
    {
        dat[len++] = carry;
    }
}
```

The **slen_t** is also a system related type, on 64-bit system, it is long long, on 32-bit system, it is int. The **slen_t** variables always indicate the count of units, the max value of a slent_t variable is 2147483647(2Gb) on 32-bit systems, or 9223372036854775807(8191Pb) on 64-bit system, as it were, under available memory conditions, the size of a number_t object is arbitrary.

next chapter: [The Initialization of the big integer object](https://github.com/brotherbeer/mydocument/blob/master/mynum/Initialization.md)
