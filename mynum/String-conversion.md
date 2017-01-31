String conversion
-------------

 * [Number_t members](#Number_t members)
 * [Ostream operator](#ostream-operator)
 * [Attentions](#attentions)
 * [Examples](#examples)

##Number_t members

Conver the value of *this to _str_
```C++
string_t& to_bin_string(string_t& str) const;
string_t& to_oct_string(string_t& str) const;
string_t& to_dec_string(string_t& str) const;
string_t& to_hex_string(string_t& str) const;
```

Conver the value of *this to _str_, which is in specified base _base_
```C++
string_t& to_string(string_t& str, int base = 10) const;
```

Return the string_t object
```C++
string_t to_bin_string() const;
string_t to_oct_string() const;
string_t to_dec_string() const;
string_t to_hex_string() const;
string_t to_string(int base = 10) const;
```

Return the string_t object, which is in base _base_
```C++
string_t operator () (int base) const;
```

##Ostream operator

```C++
std::ostream& operator << (std::ostream& os, const number_t& a)
```

##Attentions
To achieve a higher efficiency, all the string conversion functions do not generate leading charactors or blank charactors, and only lower case letters are used.  
If you want to generate formatted string, you can use the format_t class, see [\[Big integer to formatted string\]](https://github.com/brotherbeer/mydocument/blob/master/mynum/Formatted-output.md)

The time complexity of `to_hex_string` function is the lowest.

##Examples
```C++
number_t a, b(123), c("abcdef", 16);
number_t d("gogogo", 32), e("iloveyou", 36);
cout << a.to_bin_string() << endl;
cout << b.to_dec_string() << endl;
cout << c.to_hex_string() << endl;
cout << d.to_string(32) << endl;
cout << e(36) << endl;
```
Output:
```
0
123
abcdef
gogogo
iloveyou
```
