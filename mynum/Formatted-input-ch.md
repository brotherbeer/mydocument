格式化字符串转为大整数对象
-------------

 * [函数](#函数)
 * [示例](#示例)

##函数

load函数可以将字符串str表示的值赋与number_t对象a。  
str中的所有空白符会被忽略，空白符指空格、tab、换行、回车等，format参数中组分隔符中的字符也会被忽略。
如果str可以正确表示base进制的数则load函数对a赋值并返回1，否则返回0。  
```C++
int load(number_t& a, const char* str, int base = 0, const format_t* format = NULL);
int load(number_t& a, const char* str, size_t length, int base = 0, const format_t* format = NULL);
int load(number_t& a, const string_t& str, int base = 0, const format_t* format = NULL);
```
其中，base∈[0, 36]，当base为0或1时，根据字符串的“前导字符”判断进制，如0x或0X表示16进制，0b或0B表示2进制，0表示8进制，前导字符不区分大小写。  
可用'-'表示负数，'-'可以在“前导字符”的左边也可以在其右边。  
与load函数相关的两个格式化标志位：

|标志位|意义|
|------|----|
|EMPTY_AS_ERROR| 存在此标志位时将空字符串视为错误字符串，否则视为0|
|MULTISIGN_AS_ERROR| 将多负号或多正号视为错误|

关于format_t、格式化标志位以及如何设置某进制的前导字符，详见《[大整数对象转为格式化字符串](https://github.com/brotherbeer/mydocument/blob/master/mynum/Formatted-output-ch.md)》

##示例
```C++
number_t a;
load(a, " 0x1234567890\r\n");
assert(a == 0x1234567890ULL);

assert(!load(a, "1, 234, 567, 890"));  // 错误的标点','
format_t fmt;
fmt.set_group_separator(",");
assert(load(a, "1, 234, 567, 890", 0, &fmt));  // 指定fmt对象忽略标点','
assert(a == 1234567890);

assert(load(a, ""));
assert(a == 0); // 默认情况下空串被视为0
fmt.set(EMPTY_AS_ERROR); // 将空串视为错误
assert(!load(a, "", 0, &fmt));

assert(load(a, "--1"));
assert(a == 1); // 默认情况下可有多重符号
fmt.set(MULTISIGN_AS_ERROR); // 将多重符号视为错误
assert(!load(a, "--1", 0, &fmt));
```