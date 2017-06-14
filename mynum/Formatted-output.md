<h1>Big integer to formatted string</h1>

A `number_t` object can be converted into a [string_t](https://github.com/brotherbeer/mydocument/blob/master/mynum/string.md) object in the specified format, The format can be specified by `format_t`  class, for example:

```C++
string_t s;
number_t a("1234567890");
format_t fmt;
cout << fmt.dump(a, 16, s) << endl;  // to hex string

fmt.set(UPPER_CASE | SHOW_LEADING);  // use upper case chars
cout << fmt.dump(a, 16, s) << endl;
```
Output：
```
499602d2
0x499602D2
```
`UPPER_CASE` and `SHOW_LEADING` are format flags, for the details:

 * [Format flags](#t1)
 * [Format_t constructors](#t2)
 * [Format_t members](#t3)
 * [Group and line feed](#t4)
 * [Leading charactors](#t5)
 * [Attentions](#t6)

<h2 id="t1">Format flags</h2>

The format flags are `format_flags_t` constants:

|flag|meaning|
|----|-------|
|UPPER_CASE| Use upper case letters|
|UPPER_LEADING| Use upper case letters to show the leading charactors|
|SHOW_POS| If number_t object > 0，output '+'|
|SHOW_LEADING| Show the leading charactors|
|SIGN_RIGHT_LEADING| Show the sign rightside the leading charactors|
|GROUP_COMPLETE| If the chars in last group are less than the group size, fill the group by _filler_|
|GROUP_FROM_MSB| Divide the chars into groups from the most significant bit|
|ZERO_NO_LEADING| If the value is 0, donot show the leading charactors|
|ZERO_POS| If the value is 0, show '+'|
|ZERO_NEG| If the value is 0, show '-'|
|EMPTY_AS_ERROR| See the empty string as error, only for `load` functions|
|MULTISIGN_AS_ERROR| See multi-sign as error, only for `load` functions|

The flags can be concatenate by '\|':
```C++
format_t fmt;
fmt.set(UPPER_CASE | SHOW_POS | SHOW_LEADING);
fmt.clear(SHOW_POS); // drop SHOW_POS
assert(fmt.get() == UPPER_CASE | SHOW_LEADING);
fmt.set(NO_FLAGS);   // drop all flags
assert(fmt.get() == 0);
```

<h2 id="t2">format_t constructors</h2>

```C++
format_t(format_flags_t ff = 0);
```

<h2 id="t3">format_t members</h2>

Set _ff_ as the flags
```C++
void set(format_flags_t ff);
```
Clear flags specified by _ff_
```C++
void clear(format_flags_t ff);
```
Return true if _ff_ is set
```C++
bool has(format_flags_t ff) const;
```
Return all flags
```C++
format_flags_t flags() const;
```
Return the group size, see [Group and line feed](#t4)
```C++
size_t group_size() const;
```
Return group counts in a line, see [Group and line feed](#t4)
```C++
size_t line_group_count() const;
```
Return the group separator
```C++
const string_t& group_separator() const;
```
Return the line separator
```C++
const string_t& line_separator() const;
```
Return the group filler
```C++
char group_filler() const;
```
Set the group separator as a string which is _p_ pointed
```C++
void set_group_separator(const char* p);
```
Set the group separator as _c_
```C++
void set_group_filler(char c);
```
Set the charactor count _size_ in a group
```C++
void set_group_size(size_t size);
```
Set the group count _cnt_ in a line
```C++
void set_line_group_count(size_t cnt);
```
Set the line separator, '\n' is default
```C++
void set_line_separator(const char* p);
```
Convert _a_ to _str_ in base _base_
```C++
string_t& dump(const number_t& a, int _base, string_t& str) const;
```

<h2 id="t4">Group and line feed</h2>

You can divide the chars into groups, separate by the group separator, the count of chars in a group is specified by `set_group_size` function:
```C++
string_t s;
number_t a("3141592653589");
format_t fmt;
fmt.set_group_size(3);
fmt.set_group_separator(", ");
assert(fmt.dump(a, 10, s) == "3, 141, 592, 653, 589");
```
If `GROUP_FROM_MSB` is not set, the group starts from LSB, if `GROUP_FROM_MSB` is set, the group starts from MSB.
```C++
fmt.set(GROUP_COMPLETE);
fmt.set_group_size(4);
fmt.set_group_separator(" ");
assert(fmt.dump(a, 16, s) == "02db 7583 9f15");

fmt.set(GROUP_FROM_MSB);
assert(fmt.dump(a, 16, s) == "2db7 5839 f15");
```
line feed:
```C++
string_t s;
format_t fmt(UPPER_CASE | GROUP_FROM_MSB);
number_t a("2718281828459045235360287471352662497757247093699959574966");
fmt.set_group_size(8);
fmt.set_group_separator(" ");
fmt.set_line_group_count(4);
cout << fmt.dump(a, 16, s) << endl;
```
Output：
```
6EDC2FBE 41B6E8CA 1A10B710 5509E711
40F58F3B 79A7D1B6
```
Use `set_line_separator` to set the line separator, '\n' is the default.

<h2 id="t5">Leading charactors</h2>

Get the leading charactors of _base_.  
If No leading charactors, NULL is returned
```C++
const char* get_leading(int base);
```
Set the leading charactors of _base_.  
If you want to delete the leading charactors, set _leading_ to NULL.  
Notice! There should be no whitespace in _leading_
```C++
void set_leading(int base, const char* leading);
```
If `SHOW_LEADING` is set, then the leading charactors can be output, otherwise no leading charactors:
```C++
number_t a("1234567890");
string_t s;
set_leading(36, "b36:");

format_t fmt(SHOW_LEADING);
assert(fmt.dump(a, 36, s) == "b36:kf12oi");

fmt.set(UPPER_CASE);
assert(fmt.dump(a, 36, s) == "b36:KF12OI");

fmt.set(UPPER_LEADING);
assert(fmt.dump(a, 36, s) == "B36:KF12OI");
```
The leading charactors are case insensitive, If you want to show them in upper case, set `UPPER_LEADING`.

Specify the sign position:
```C++
number_t a("-1234567890");
string_t s;
set_leading(36, "b36:");

format_t fmt(SHOW_LEADING);
assert(fmt.dump(a, 36, s) == "-b36:kf12oi");

fmt.set(SIGN_RIGHT_LEADING);
assert(fmt.dump(a, 36, s) == "b36:-kf12oi");
```

<h2 id="t6">Attentions</h2>

The leading charactors are global data, you'd better call `set_leading` in main thread.

The leading characters should be able to be separated from the body of the string, there should be no whitespace, and the group separator should be able to be separated from the string too, otherwise ambiguity will be caused.