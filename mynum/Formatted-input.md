Formatted string to big integer
-------------

 * [Functions](#Functions)
 * [Examples](#examples)

##Functions

You can use `load` functions to assign the value expressed by _str_ to the number_t object _a_.  
The blank chars like blank space, tab, '\r', '\n' will be ignored, and the chars in the group separator specified by _format_ will be ignored too.   
If _str_ is right, the functions return 1, otherwise return 0.
```C++
int load(number_t& a, const char* str, int base = 0, const format_t* format = NULL);
int load(number_t& a, const char* str, size_t length, int base = 0, const format_t* format = NULL);
int load(number_t& a, const string_t& str, int base = 0, const format_t* format = NULL);
```
_base_∈[0, 36],  when _base_ < 1, the base is determined from the "leading charactors" , like "0x" means hexadecimal, the "leading charactors" are case-insensitive。  
Use '-' to denote negtive integer，'-' may be rightside the "leading charactors", or leftside. '+' is acceptable, means positive.

|flag|meaning|
|----|-------|
|EMPTY_AS_ERROR| see empty string or NULL pointer as error|
|MULTISIGN_AS_ERROR| see multi-sign as error|

About format_t, format flags, and the setting of the "leading charactors", see [Big integer to formatted string](https://github.com/brotherbeer/mydocument/blob/master/mynum/Formatted-output.md)

##Examples
```C++
number_t a;
load(a, " 0x1234567890\r\n");
assert(a == 0x1234567890ULL);

assert(!load(a, "1, 234, 567, 890"));  // ',' is wrong
format_t fmt;
fmt.set_group_separator(",");
assert(load(a, "1, 234, 567, 890", 0, &fmt));  // use fmt to ignore ','
assert(a == 1234567890);

assert(load(a, ""));
assert(a == 0); // the empty string means 0
fmt.set(EMPTY_AS_ERROR); // see the empty string as error
assert(!load(a, "", 0, &fmt));

assert(load(a, "--1"));
assert(a == 1); // multi-sign
fmt.set(MULTISIGN_AS_ERROR); // see multi-sign as error
assert(!load(a, "--1", 0, &fmt));
```