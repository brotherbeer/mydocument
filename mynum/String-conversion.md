<h1>String conversion</h1>

 * [Member functions](#nemberfunctions)
 * [Ostream operator](#ostreamoperator)
 * [Attentions](#attentions)
 * [Examples](#examples)

<h2 id="memberfunctions">Member functions</h2>

Conver the value of _*this_ to _str_
```C++
string_t& to_bin_string(string_t& str) const;
string_t& to_oct_string(string_t& str) const;
string_t& to_dec_string(string_t& str) const;
string_t& to_hex_string(string_t& str) const;
```

Conver the value of _*this_ to _str_, which is in specified base _base_
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

<h2 id="ostreamoperator">Ostream operator</h2>

```C++
std::ostream& operator << (std::ostream& os, const number_t& a)
```

<h2 id="attentions">Attentions</h2>

To achieve a higher efficiency, all the string conversion functions do not generate leading charactors or blank charactors, and only lower case letters are used.  
If you want to generate formatted string, you can use the format_t class, see [\[Big integer to formatted string\]](https://github.com/brotherbeer/mydocument/blob/master/mynum/Formatted-output.md)

The run time complexity of `to_hex_string` function is the lowest.

<h2 id="examples">Examples</h2>

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
