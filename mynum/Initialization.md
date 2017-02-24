The initialization of the big integer object
-------------

 * [Functions](#functions)
 * [Attentions](#attentions)
 * [Examples](#examples)
 * [Algorithms](#algorithms)

##Functions

Default constructor, the value of \*this is 0
```C++
number_t::number_t();
```

Construct a new big integer from _x_
```C++
number_t::number_t(int x);
number_t::number_t(long x);
number_t::number_t(long long x);
number_t::number_t(unsigned int x);
number_t::number_t(unsigned long x);
number_t::number_t(unsigned long long x);
```

Construct a new big integer from _s_, a null-terminated C string in base _base_ (_base_ ∈ [2, 36]).
The string may contain an optional minus sign to indicate its value is minus, and the chars are case insensitive.
'+' and any spaces or punctuations are not allowed.
```C++
number_t::number_t(const char* s, int base);
```

If the _base_ is omitted, see _s_ as in base 10
```C++
number_t::number_t(const char* s);
```

You can also specify the _length_ of the _s_
```C++
number_t::number_t(const char* s, size_t length, int base);
```

Construct a new big integer from a string_t object
```C++
number_t::number_t(const string_t&);
number_t::number_t(const string_t&, int base);
number_t::number_t(const string_t&, size_t length, int base);
```

The copy constructor
```C++
number_t::number_t(const number_t&);
```

Assigns the value of another number_t object to *this.
```C++
number_t& assign(const number_t&);
```

Assigns the value of _x_ to *this.
```C++
number_t& assign(int x);
number_t& assign(long x);
number_t& assign(long long x);
number_t& assign(unsigned int x);
number_t& assign(unsigned long x);
number_t& assign(unsigned long long x);
```

Assigns the value of _s_ to *this, the usage is similar to the constructors
```C++
number_t& assign(const char* s);
number_t& assign(const char* s, int base);
number_t& assign(const char* s, size_t length, int base);
number_t& assign(const string_t& s);
number_t& assign(const string_t& s, int base);
number_t& assign(const string_t& s, size_t length, int base);
```

Copy from another object
```C++
void copy(const number_t&);
```

check whether _str_ is right for _base_  
If right, return the length of _str_, otherwise return 0
```C++
int check(const char* str, int base);
int check(const char* strbegin, const char* strend, int base);
```

##Attentions
To achieve a higher efficiency, when constructing or assigning from a string, the constructors and the assignment functions do not consider '+' and any prefixes, such as "0x", "0b", and do not detect any wrong char in the string argument.
If the string argument is wrong, the value of the object is wrong too, but the program will not crash.
The legal chars in the string argument are only [0-9a-zA-Z], 'a' and 'A' mean 10, 'b' and 'B' mean 11, and so on, 'z' and 'Z' mean 35.
If a digit denoted by a char is equal to or bigger than the specified base, the value of the big integer object is wrong. 

Of course, this is just a feature of the constructors and the assignment functions, mynum can handle strings with complex formats, see [\[Formatted string to big integer\]](https://github.com/brotherbeer/mydocument/blob/master/mynum/Formatted-input.md)
 and [\[Big integer to formatted string\]](https://github.com/brotherbeer/mydocument/blob/master/mynum/Formatted-output.md)

When using a string that denotes a hexadecimal intger, the time complexity is the lowest.

`copy(const number_t` and `assign(const number_t&)` are not the same, `assign` only sets the value of another object to *this, `copy` not only copies the value but also allocate the same memory as the object specified.

##Examples
```C++
#include "mynum.h"
using namespace mynum;        // the namespace of mynum

number_t a = 123, b(789L);    // use C integer type to initialize number_t objects
number_t c("271828182845");   // use a decimal string to initialize the object
number_t d("abcdef", 16);     // use a hexadecimal number to initialize the object
number_t e("1234567", 8);     // use an octal string to initialize the object
number_t f("1111100", 2);     // use a binary string to initialize the object
number_t g("abcdefg", 17);    // use a string denotes 17 based integer

number_t x("123456789", 8);   // in octal number, '8' and '9' are wrong, so the value of x is wrong
number_t y("1,234,567", 8);   // ',' and other punctuations are not acceptable
number_t z("1 234 567", 8);   // the blank spaces are not acceptable
```

If you want to test the correctness of the string, you can use the `check` function, for example:
The `check` function returns the string length if the string is right, or 0 if the string is wrong.
```C++
const char* s = "1234567890";
assert(check(s, 10) > 0);     // if s denotes a decimal number, then s is correct
assert(check(s, 8) == 0);     // if s denotes an octal number, then s is wrong
```

##Algorithms

For the `BASE`, `UNITMAX` and other constants, see the previous chapter [Data storage model](https://github.com/brotherbeer/mydocument/blob/master/mynum/Storage.md).

###Construct a big integer object form a string

If a string _s_ has _n_ chars, and it denotes an integer in base _b_, we can construct a number_t object _o_ whose value is the same as the integer denoted by _s_.

First determine how much memory the _o_ needs to hold the number of the _s_ represented.

Obviously, the max value of n-digit integer in base _b_ is b<sup>n</sup>-1, assume that _o_ need _m_ units to hold this number, the _m_ must satisfy the following equations (let ln denote the natural logarithm, and ceil denotes rounding up):

BASE<sup>m</sup>-1 = b<sup>n</sup>-1

ln(BASE<sup>m</sup>) = ln(b<sup>n</sup>)

m = ceil(n * ln(b) / ln(BASE))

So the memory needed is m * sizeof(unit_t) bytes.

Let _S_ be the digits sequence corresponding to the chars in _s_, the value of the integer denoted by _s_ is:

_S[0]\*b<sup>n-1</sup> + S[1]\*b<sup>n-2</sup> + ... + S[n-1]\*b<sup>0</sup>_

The calculation of this formula can be done by an iterative procedure, the pseudo code:
```C++
number_t::construct_from_string(const char* s, int b)
{
    int n = strlen(s);
    allocate_units(ceil(n * ln(b) / ln(BASE)));  // allocate m units
    for (i = 0; i < n; i++)
    {
        mul_unit(b);
        add_unit(char_to_int(s[i])); // char_to_int converts a char to int
                                     // S[i] is char_to_int(s[i])
    }
}
```
In the for loop, when _i_ is 0, set the value of _o_ to _S[0]_, when _i_ > 0, use the mul_unit to multiply _o_by _b_, and use add_unit to add _o_ with _S[i]_
About mul_unit and add_unit see previous chapter [Data storage model](https://github.com/brotherbeer/mydocument/blob/master/mynum/Storage.md).

So far, the principle of converting strings to number_t objects has been described, but the efficiency can be improved.

Let _inner\_digits_ be the max value which makes _b<sup>inner\_digits</sup>_ <= UNITMAX, _inner\_base_ = _b<sup>inner\_digits</sup>_. 
Each times conver _inner\_digits_ chars to an unit, reduce multiplication and addition times effectively, the efficiency is improved.
```C++
number_t::construct_from_string(const char* s, int b)
{
    int n = strlen(s), i = 0;
    allocate_units(ceil(n * ln(b) / ln(BASE)));
    int inner_base = get_inner_base(b);
    int inner_digits = get_inner_digits(b);
    for (; i < n - n % inner_digits; i += inner_digits) // convert inner_digits chars to one unit each time
    {
        mul_unit(inner_base);
        add_unit(str_to_unit(s + i, b, inner_digits)); 
    }
    for (; i != n; i++)
    {
        mul_unit(b);
        add_unit(char_to_int(s[i]));
    }
}
```

For strings representing hexadecimal integers, because each of the 2 characters can determine a byte, 
on the 32-bit system, 4 chars can determine an unit, on the 32-bit system, 8 chars can determine an unit, so the construction doesnot need multiplication and addition at all, this is similarly for the strings representing binary number.
```C++
number_t::construct_from_hex_string(const char* s)
{
    int n = strlen(s);
    int k = sizeof(unit_t) * 2;         // k chars are one unit
    const char* p0 = s + n - k;
    const char* p1 = s + n % k;

    allocate_units((n + k - 1) / k);    // need (n + k - 1) / k units
    for (; p0 >= p1; p0 -= k)           // convert k chars to one unit
    {
        dat[len++] = strhex_to_unit(p0, k); 
    }
    if (n % k)
    {
        dat[len++] = strhex_to_unit(s, n % k);
    }
}
```
So, when using a string that denotes a hexadecimal intger, the efficiency is the highest.

###Construct a big integer object form a basic type variable

If _v_ is variable of basic integer type (int, long, etc.), we can construct a number_t object _o_ whose value is the same as _v_.

Because the data in _o_ is in the same form of basic types, so we can allocate sizeof(_v_), and copy the value immediately.

For example, unsigned long long _v_ = 1, if we construct _o_ from it on 32-bit system, first we allocate sizeof(_v_) bytes, that is 4 units, and then we copy the value, the 4 units from low address to high address will be: 0x0001, 0x0000, 0x0000, 0x0000.

The units at high adderss are zero, they are invalid, the member _len_ in number_t should only describ the conut of valid units, so the member _len_ in _o_ should be 1, not 4.

The zero unit at high adderss in mynum is called "leading zero", the count of leading zeros should not be included in _len_.


