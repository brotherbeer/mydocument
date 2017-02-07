Big integer to ordinary integer
-------------

 * [Number_t members](#number_t-members)
 * [Attentions](#attentions)
 * [Examples](#examples)

##Number_t members

Determine whether the value of _*this_ is within the range of the ordinary integer type
```C++
bool in_range_char() const;
bool in_range_short() const;
bool in_range_int() const;
bool in_range_long() const;
bool in_range_longlong() const;
bool in_range_uchar() const;
bool in_range_ushort() const;
bool in_range_uint() const;
bool in_range_ulong() const;
bool in_range_ulonglong() const;
bool in_range_word() const;
bool in_range_sword() const;
```

Convert to the ordinary integer
```C++
char to_char() const;
short to_short() const;
int to_int() const;
long to_long() const;
long long to_longlong() const;
unsigned char to_uchar() const;
unsigned short to_ushort() const;
unsigned int to_uint() const;
unsigned long to_ulong() const;
unsigned long long to_ulonglong() const;
```

operators:
```C++
operator bool () const;
bool operator ! () const;
operator char () const;
operator short () const;
operator int () const;
operator long () const;
operator long long () const;
operator unsigned char () const;
operator unsigned short () const;
operator unsigned int () const;
operator unsigned long () const;
operator unsigned long long () const;
```

##Attentions
Before the conversion, you should determine whether the value of the number_t object is within the range of the specified ordinary integer type, otherwise, the value of the ordinary integer converted may be wrong.

The ranges of the ordinary integer types:

|type|range|
|----|-----|
|char| \[-128, 127\]|
|short| \[-32768, 32767\]|
|int| \[-2147483648, 2147483647\]|
|long| decided by the compilers |
|long long| \[-9223372036854775808, 9223372036854775807\] |
|unsigned char| \[0, 255\]|
|unsigned short|\[0, 65535\]|
|unsigned int| \[0, 4294967295\] |
|unsigned long| decided by the compilers |
|unsigned long long| \[0, 18446744073709551615\] |

The range of long/unsigned long are decided by the compilers, in gcc, are the same as long long/unsigned long long, in MSVC, are the same as int/unsigned int.

##Examples
```C++
number_t a(0xffffffff), b(-1);
if (a.in_range_int()) cout << a.to_int() << endl;
if (a.in_range_uint()) cout << a.to_uint() << endl;
if (b.in_range_int()) cout << a.to_int() << endl;
if (b.in_range_uint()) cout << a.to_uint() << endl;
```
Output:
```
4294967295
-1
```