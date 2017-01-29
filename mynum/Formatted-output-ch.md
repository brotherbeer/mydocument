大整数对象转为格式化字符串
-------------

大整数(number_t)对象可以按指定的格式转化为字符串(string_t)对象。可由format_t类的对象指定格式，例如：
```C++
string_t s;
number_t a("1234567890");
format_t fmt;
cout << fmt.dump(a, 16, s) << endl;  // 将a转为表示16进制数的字符串

fmt.set(UPPER_CASE | SHOW_LEADING);
cout << fmt.dump(a, 16, s) << endl;
```
输出：
```
499602d2
0x499602D2
```
其中，UPPER_CASE和SHOW_LEADING是用以指定格式化信息的标志位，分别表示用大写字母记录各位数值和显示前导字符，默认情况下用小写字母并不显示前导字符。dump函数将大整数对象转为指定进制的字符串，示例中为16进制。
关于format_t类的详细信息如下：

 * [标志位](#标志位)
 * [format_t构造函数](#构造函数)
 * [format_t成员函数](#成员函数)
 * [前导字符](#前导字符)
 * [分组与换行](#分组与换行)
 * [注意事项](#注意事项)

##标志位
格式化标志位为format_flags_t型的常量，各标志位定义如下：  

|标志位|意义|
|------|----|
|UPPER_CASE| 用大写字母输出字符串，无此标志位则用小写字母|
|UPPER_LEADING| 用大写字母输出前导字符，如默认情况下十六进制对应0X、二进制对应0B等|
|SHOW_POS| 如果指定的大整数对象为正数，则输出+号|
|SHOW_LEADING| 输出前导字符，如默认情况下十六进制对应0x、二进制对应0b等，前导字符可以设定|
|SIGN_RIGHT_LEADING| 符号在前导字符右侧，如0x-ab，无此标志位则符号在前导字符左侧，如-0xab|
|GROUP_COMPLETE| 如果最后一个分组中的字符个数小于group，则由filler指定的字符填充|
|GROUP_FROM_MSB| 从高位开始按指定字符数对字符分组|
|ZERO_NO_LEADING| 如果指定的大整数为0，不输出前导字符，无此标志位则输出|
|ZERO_POS| 如果存在SHOW_POS标志位且指定的大整数对象为0，则输出+号|
|ZERO_NEG| 如果指定的大整数对象为0，输出-号|
|EMPTY_AS_ERROR| 存在此标志位时将空字符串视为错误字符串，否则视为0|
|MULTISIGN_AS_ERROR| 将多负号或多正号视为错误|

如：
```C++
format_t fmt;
fmt.set(UPPER_CASE | SHOW_POS | SHOW_LEADING);
fmt.clear(SHOW_POS); // 清除SHOW_POS标志位
assert(fmt.get() == UPPER_CASE | SHOW_LEADING)
fmt.set(NO_FLAGS);   // 清除所有标志位
assert(fmt.get() == 0);
```

##构造函数
可在构造时指定标志位，默认值为0，即不设定任何标志位
```C++
format_t(format_flags_t ff = 0):
```
##成员函数
设定某（些）标志位
```C++
void set(format_flags_t ff);
```
清除某（些）标志位
```C++
void clear(format_flags_t ff);
```
清除所有标志位
```C++
void clear_all() { _flags = 0; }
```
判断是否设定了某（些）标志位
```C++
bool has(format_flags_t ff) const;
```
返回所有标志位
```C++
format_flags_t flags() const;
```
返回分组大小，详见[分组与换行](#分组与换行)
```C++
size_t group_size() const;
```
返回行内分组个数，详见[分组与换行](#分组与换行)
```C++
size_t line_group_count() const;
```
返回组分隔符
```C++
const string_t& group_separator() const;
```
返回行分隔符
```C++
const string_t& line_separator() const;
```
返回组填充符符
```C++
char group_filler() const;
```
设置组分隔符
```C++
void set_group_separator(const char* p);
```
设置组填充符
```C++
void set_group_filler(char c);
```
设置组字符个数
```C++
void set_group_size(size_t size);
```
设置行内组个数
```C++
void set_line_group_count(size_t cnt);
```
设置行分隔符，默认为'\n'
```C++
void set_line_separator(const char* p);
```
将大整数对象a转为进制为base的字符串str
```C++
string_t& dump(const number_t& a, int _base, string_t& str) const;
```

##分组与换行
可将输出字符串按指定的字符个数进行分组，组间由组分隔符分隔，组字符个数由set_group_size函数设定，当指定字符个数为0时不分组，默认不分组。如：
```C++
string_t s;
number_t a("3141592653589");
format_t fmt;
fmt.set_group_size(3);
fmt.set_group_separator(", ");
assert(fmt.dump(a, 10, s) == "3, 141, 592, 653, 589");
```
如果不设定GROUP_FROM_MSB，将从低位开始每隔指定的字符数输出组分隔符，如果设定GROUP_FROM_MSB，则从高位开始。当一个分组不足指定的字符个数时，可以通过设置GROUP_COMPLETE标志位对分组进行补全，默认补全字符为'0'，补全字符可以由set_group_filler函数设定。当设置了GROUP_FROM_MSB时，GROUP_COMPLETE标志位无效。如：
```C++
fmt.set(GROUP_COMPLETE);
fmt.set_group_size(4);
fmt.set_group_separator(" ");
assert(fmt.dump(a, 16, s) == "02db 7583 9f15");

fmt.set(GROUP_FROM_MSB);
assert(fmt.dump(a, 16, s) == "2db7 5839 f15");
```
也可以将大整数对象分行输出，由set_line_group_count指定每行的组数，如：
```C++
string_t s;
format_t fmt(UPPER_CASE | GROUP_FROM_MSB);
number_t a("2718281828459045235360287471352662497757247093699959574966");
fmt.set_group_size(8);
fmt.set_group_separator(" ");
fmt.set_line_group_count(4);
cout << fmt.dump(a, 16, s) << endl;
```
输出：
```
6EDC2FBE 41B6E8CA 1A10B710 5509E711
40F58F3B 79A7D1B6
```
可由set_line_separator设定行分隔符，默认为'\n'。

##前导字符
可以按照惯例，在输出的字符串前加上“前导字符”以表示进制，如8进制为“0”，16进制为“0x”，可以用set_leading函数设定某进制的前导字符，也可以用get_leading函数获取某进制的前导字符：

获取指定进制base的前导字符串，该字符串以'\0'结尾，如果无前导字符串则返回NULL  
16进制的前导字符串默认为"0x"，2进制为"0b"，8进制为"0"
```C++
const char* get_leading(int base);
```

将leading指定为进制base的前导字符串，一经设定，全局生效。  
如果想删除某个进制的前导字符串，将leading置为NULL即可。
注意！leading中不应存在任何空白符
```C++
void set_leading(int base, const char* leading);
```

如果设定SHOW_LEADING标志位，则输出前导字符，否则不输出，如：
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
注意，前导字符在mynum中是不区分大小写的，如果需要用大写字母显示前导字符，可以设置UPPER_LEADING标志位。

对于有符号大整数对象，还存在一个问题，即符号应该显示在前导字符的左侧还是右侧，默认情况下mynum将符号显示在前导字符的左侧，可以通过设置SIGN_RIGHT_LEADING标志位，使符号显示在前导字符的右边，如：
```C++
number_t a("-1234567890");
string_t s;
set_leading(36, "b36:");

format_t fmt(SHOW_LEADING);
assert(fmt.dump(a, 36, s) == "-b36:kf12oi");

fmt.set(SIGN_RIGHT_LEADING);
assert(fmt.dump(a, 36, s) == "b36:-kf12oi");
```

##注意事项
前导字符为全局数据，设置后load、dump函数以及标准输入输出流均生效，但没有任何线程安全措施，故尽量不要某个线程中调用set_leading函数而在另一个线程中调用load、dump等函数。
