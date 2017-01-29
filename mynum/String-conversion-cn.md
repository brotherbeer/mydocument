大整数对象转为字符串
-------------

 * [相关成员函数](#相关成员函数)
 * [注意事项](#注意事项)
 * [示例](#示例)
 * [算法](#算法)

##相关成员函数

按2进制转为字符串str
```C++
string_t& number_t::to_bin_string(string_t& str) const;
```
按8进制转为字符串str
```C++
string_t& number_t::to_oct_string(string_t& str) const;
```
按10进制转为字符串str
```C++
string_t& number_t::to_dec_string(string_t& str) const;
```
按16进制转为字符串str
```C++
string_t& number_t::to_hex_string(string_t& str) const;
```
按base进制转为字符串str
```C++
string_t& number_t::to_string(string_t& str, int base = 10) const;
```
按对象返回
```C++
string_t number_t::to_bin_string() const;
string_t number_t::to_oct_string() const;
string_t number_t::to_dec_string() const;
string_t number_t::to_hex_string() const;
string_t number_t::to_string(int base = 10) const;
```
重载()，按base进制返回字符串对象
```C++
string_t number_t::operator () (int base) const;
```

##注意事项
为了更高的效率，所有与字符串转换相关的成员函数不会成生前导字符串或空白符，并只用小写字母。 
当然，mynum可以将大整数对象转为具有复杂格式的字符串，如用format_t类的dump函数，具体请参见《[大整数对象转为格式化字符串](https://github.com/brotherbeer/mydocument/blob/master/mynum/Formatted-output-ch.md)》

##示例
```C++
number_t a, b(123), c("abcdef", 16);
number_t d("gogogo", 32), e("iloveyou", 36);
cout << a.to_bin_string() << endl;
cout << b.to_dec_string() << endl;
cout << c.to_hex_string() << endl;
cout << d.to_string(32) << endl;
cout << e(36) << endl;
```
输出：
```
0
123
abcdef
gogogo
iloveyou
```

##算法


