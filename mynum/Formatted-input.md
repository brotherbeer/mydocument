<h1>Formatted string to big integer</h1>

 * [Functions](#functions)
 * [Examples](#examples)

<h2 id="functions">Functions</h2>

You can use `load` functions to assign the value expressed by _str_ to the number_t object _a_.  
The white spaces, tabs, '\r', '\n', '\v', '\f' are ignored, and the chars in the group separator specified by _format_ are ignored too.   
If _str_ is right for base _base_, the functions return 1, otherwise return 0.
```C++
int load(number_t& a, const char* str, int base = 0, const format_t* format = NULL);
int load(number_t& a, const char* str, size_t length, int base = 0, const format_t* format = NULL);
int load(number_t& a, const string_t& str, int base = 0, const format_t* format = NULL);
```
_base_∈[0, 36], when _base_ < 1, the base is determined from the "leading charactors" , like "0x" means hexadecimal, the leading charactors are case-insensitive.  
'-' denotes the integer is negtive, '-' may be on the left side of the leading charactors, or be right side. '+' is acceptable, means positive.

Default leading charactors:

|leading|base|
|-------|----|
|0b| 2|
|0| 8|
|0x| 16|

2 format flags:

|flag|meaning|
|----|-------|
|EMPTY_AS_ERROR| see the empty string or NULL pointer as error|
|MULTISIGN_AS_ERROR| see multi-sign as error|

About format_t, format flags, and the setting of the leading charactors, see [Big integer to formatted string](https://github.com/brotherbeer/mydocument/blob/master/mynum/Formatted-output.md)

<h2 id="examples">Examples</h2>

```C++
number_t a;
load(a, " 0x1234567890\r\n");
assert(a == 0x1234567890ULL);

assert(!load(a, "1, 234, 567, 890"));  // by default, ',' is wrong
format_t fmt;
fmt.set_group_separator(",");
assert(load(a, "1, 234, 567, 890", 0, &fmt));  // use fmt to ignore ','
assert(a == 1234567890);

assert(load(a, ""));
assert(a == 0); // by default, the empty string means 0
fmt.set(EMPTY_AS_ERROR); // see the empty string as error
assert(!load(a, "", 0, &fmt));

assert(load(a, "--1"));  // multi-sign
assert(a == 1); 
fmt.set(MULTISIGN_AS_ERROR); // see multi-sign as error
assert(!load(a, "--1", 0, &fmt));
```