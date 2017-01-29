大整数对象转为基本整型变量
-------------

 * [相关成员函数](#相关成员函数)
 * [注意事项](#注意事项)
 * [示例](#示例)

##相关成员函数

判断对象的值是否在指定的基本整型范围内
```C++
bool number_t::in_range_char() const;
bool number_t::in_range_short() const;
bool number_t::in_range_int() const;
bool number_t::in_range_long() const;
bool number_t::in_range_longlong() const;
bool number_t::in_range_uchar() const;
bool number_t::in_range_ushort() const;
bool number_t::in_range_uint() const;
bool number_t::in_range_ulong() const;
bool number_t::in_range_ulonglong() const;
bool number_t::in_range_word() const;
bool number_t::in_range_sword() const;
```

将对象的值转为相应基本整型变量
```C++
char number_t::to_char() const;
short number_t::to_short() const;
int number_t::to_int() const;
long number_t::to_long() const;
long long number_t::to_longlong() const;
unsigned char number_t::to_uchar() const;
unsigned short number_t::to_ushort() const;
unsigned int number_t::to_uint() const;
unsigned long number_t::to_ulong() const;
unsigned long long number_t::to_ulonglong() const;
```

类型转换运算符重载
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

##注意事项
将大整数对象转为基本整型变量之前应先判断其值是否在相应基本整型的范围内，如果不在该范围内，转化后的值为不正确的值。  
另外，值为负时，不算入相应无符号类型的范围内，如-1不在unsigned int范围内，-2不在unsigned long范围内。  
各类型范围：
|char| [-128, 127]|
|short| [-32768, 32767]|
|int| [-2147483648, 2147483647]|
|long| 随编译器而定|
|long long| [-9223372036854775808, 9223372036854775807] |
|unsigned char| [0, 255]|
|unsigned short|[0, 65535]|
|unsigned int| [0, 4294967295] |
|unsigned long| 随编译器而定|
|unsigned long long| [0, 18446744073709551615] |
其中，long/unsigned long型的范围随编译器而定，gcc编译环境中与long long/unsigned long long相同，MSVC环境中与int/unsigned int相同。

##示例
```C++
number_t a(0xffffffff), b(-1);
if (a.in_range_int()) cout << a.to_int() << endl;
if (a.in_range_uint()) cout << a.to_uint() << endl;
if (b.in_range_int()) cout << a.to_int() << endl;
if (b.in_range_uint()) cout << a.to_uint() << endl;
```
输出：
```
4294967295
-1
```