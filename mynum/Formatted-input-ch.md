格式化字符串转为大整数对象

用字符串str初始化number_t对象a（str表示一个base进制的数，以'\0'结尾）。str中的所有空白符会被忽略，空白符指空格、tab、换行、回车等。如果字符串的格式正确则初始化a并返回1，否则返回0。  
base∈[2, 36]，当base为0或1，根据字符串的“前导字符”判断进制，如0x或0X表示16进制，0b或0B表示2进制，0表示8进制，前导字符不区分大小写。  
可用'-'表示负数，'-'可以在“前导字符”的左边也可以在其右边，load函数可以处理相对复杂的情况，关于format参数，以及如何设置某进制的前导字符，请参见《[大整数对象的格式化输出](https://github.com/brotherbeer/mydocument/blob/master/mynum/Formatted-output-ch.md)》

```C++
int load(number_t& a, const char* str, int base, const format_t* format = NULL);
int load(number_t& a, const char* str, size_t length, int base, const format_t* format = NULL);
int load(number_t& a, const string_t& str, int base, const format_t* format = NULL);
```