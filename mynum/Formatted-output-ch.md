大整数对象的格式化输出
-------------

 * [格式化参数](#格式化参数)
 * [函数](#函数)
 * [注意事项](#注意事项)
 * [示例](#示例)
 * [算法](#算法)

##格式化参数

格式化参数类format_t，由成员变量指定各种格式化信息，由成员函数dump将指定的大整数对象格式化为字符串：
```C++
struct format_t
{
    format_flags_t flags;  // 格式化标志位
    int base;              // 进制
    size_t group;          // 每个分组中的字符个数
    string_t separator;    // 组分隔符
    char filler;           // 组填充符
 
    /** 默认构造函数*/
    format_t();
    /** 构造函数，由ff初始化成员flags*/
    format_t(format_flags_t ff);
    /** 构造函数，由ff初始化成员flags，b初始化成员base*/
    format_t(format_flags_t ff, int b);

    /** 将ff指定的标志位加入flags */
    void set(format_flags_t ff);
    /** 将ff指定的标志位从flags中清除 */
    void clear(format_flags_t ff);
    /** 清除所有标志位 */
    void clear_all();

    /** 判断是否存在ff指定的标志位 */
    bool has(format_flags_t ff) const;
	/** 返回所有标志位*/
    format_flags_t get() const;

	/** 将大整数对象a按指定的格式化信息转成进制为b的字符串str */
    string_t& dump(const number_t& a, int b, string_t& str) const;

	/** 如果不指定b，则进制由成员变量base决定 */
    string_t  dump(const number_t& a) const;
    string_t& dump(const number_t& a, string_t& str) const;
}; 
```
###分组


###格式化标志位
|标志位|意义|
|------|----|
|UPPER_CASE| 用大写字母输出字符串，如无此标志位则用小写字母|
|SHOW_POS| 如果指定大整数对象为正数，则输出+号|
|SHOW_LEADING| 输出前导字符，十六进制对应0x、二进制对应0b等，前导字符可以设定|
|SIGN_RIGHT_LEADING| 符号在前导字符右侧，如0x-ab，如无此标志位符号在前导字符左侧，如-0xab|
|GROUP_COMPELTE| 如果最后一个分组中的字符个数小于group，则由filler指定的字符填充|
|ZERO_NO_LEADING| 0无前导字符|
|ZERO_POS| 如果存在SHOW_POS标志位且指定大整数对象为0，则输出+号|
|ZERO_NEG| 指定大整数对象为0，输出-号|
|EMPTY_AS_ERROR| 空字符串为错误字符串，否则为0|

###设定前导字符


##函数

将大整数对象转为二进制字符串
```C++
string_t& number_t::to_bin_string(string_t& str) const;
```

将大整数对象转为八进制字符串
```C++
string_t& number_t::to_oct_string(string_t& str) const;
```

将大整数对象转为十进制字符串
```C++
string_t& number_t::to_dec_string(string_t& str) const;
```

将大整数对象转为十六进制字符串
```C++
string_t& number_t::to_hex_string(string_t& str) const;
```

将大整数对象转为base进制字符串
```C++
string_t& number_t::to_string(string_t& str, int base = 10) const;
```

返回string_t对象
```C++
string_t to_bin_string() const;
string_t to_oct_string() const;
string_t to_dec_string() const;
string_t to_hex_string() const;
string_t to_string(int base = 10) const;
```

