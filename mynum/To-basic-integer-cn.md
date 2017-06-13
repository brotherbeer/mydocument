<h1>大整数对象转为基本整型变量</h1>

 * [成员函数](#memberfunctions)
 * [注意事项](#attentions)
 * [示例](#examples)

<h2 id="memberfunctions">相关成员函数</h2>

判断对象的值是否在指定的基本整型范围内
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

将对象的值转为相应基本整型变量
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

<h2 id="attentions">注意事项</h2>

将大整数对象转为基本整型变量之前应先判断其值是否在相应基本整型的范围内，如果不在该范围内，转化后的值为不正确的值。  
另外，值为负时，不算入相应无符号类型的范围内，如-1不在unsigned int范围内，-2不在unsigned long范围内。  
各类型范围：

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

其中，long/unsigned long型的范围由编译器决定，gcc编译环境中与long long/unsigned long long相同，MSVC环境中与int/unsigned int相同。

<h2 id="examples">示例</h2>

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