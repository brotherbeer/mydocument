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
重载<<
```C++
std::ostream& operator << (std::ostream& os, const number_t& a)
```

##注意事项
为了更高的效率，所有与字符串转换相关的成员函数不会成生前导字符串或空白符，并只用小写字母。 
当然，mynum可以将大整数对象转为具有复杂格式的字符串，如用format_t类的dump函数，具体请参见《[大整数对象转为格式化字符串](https://github.com/brotherbeer/mydocument/blob/master/mynum/Formatted-output-ch.md)》

将大整数对象按16进制转为字符串的时间复杂度最低。

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

###将一个计算单元转为base进制数（base∈[2, 36]）

设u为一个计算单元，即0 <= u < BASE，相关定义请参见《[mynum的数据存储方式](https://github.com/brotherbeer/mydocument/blob/master/mynum/Storage-ch.md)》，将u转为base进制的数可由以下循环得出，其中d为一个数组，记录u转为base进制数后各位数值，i为数组下标：
```C++
for (i = 0; u != 0; i++)
{
	d[i] = u % base;
	u /= base;
}
```
设u转为base进制数后共n位，即u = d<sub>n-1</sub> \* base<sup>n-1</sup> + ... + d<sub>1</sub>\* base + d<sub>0</sub>，简记为：u =〈d<sub>n-1</sub>, ..., d<sub>1</sub>, d<sub>0</sub>〉<sub>base</sub>  

###将两个计算单元转为base进制数

设u<sub>1</sub>、u<sub>2</sub>为两个计算单元，它们组成整数〈u<sub>1</sub>, u<sub>2</sub>〉<sub>BASE</sub>，此处讨论如何将该整数转为base进制数。
根据前面的结论，可将u<sub>1</sub>转为〈d<sub>n-1</sub>, ..., d<sub>1</sub>, d<sub>0</sub>〉<sub>base</sub>

〈u<sub>1</sub>, u<sub>2</sub>〉<sub>BASE</sub> =〈d<sub>n-1</sub>, ..., d<sub>1</sub>, d<sub>0</sub>〉<sub>base</sub> * BASE + u<sub>2</sub>

设d<sub>0</sub> \* BASE + u<sub>2</sub> = q<sub>0</sub> \* base + r<sub>0</sub>，r<sub>0</sub> < base:

〈u<sub>1</sub>, u<sub>2</sub>〉<sub>BASE</sub> =〈d<sub>n-1</sub> \* BASE, ..., d<sub>2</sub> \* BASE, d<sub>1</sub> \* BASE + q<sub>0</sub>, r<sub>0</sub>〉<sub>base</sub>

设d<sub>1</sub> \* BASE + q<sub>0</sub> = q<sub>1</sub> \* base + r<sub>1</sub>，r<sub>1</sub> < base:

〈u<sub>1</sub>, u<sub>2</sub>〉<sub>BASE</sub> =〈d<sub>n-1</sub> \* BASE, ..., d<sub>2</sub> \* BASE + q<sub>1</sub>, r<sub>1</sub>, r<sub>0</sub>〉<sub>base</sub>

显然，利用相同的方法令d<sub>i</sub> \* BASE + q<sub>i-1</sub> = q<sub>i</sub> \* base + r<sub>i</sub>，即q<sub>i</sub> = (d<sub>i</sub> \* BASE + q<sub>i-1</sub>)/base, r<sub>i</sub> = (d<sub>i</sub> \* BASE + q<sub>i-1</sub>)%base，i >= 1，可得：

〈u<sub>1</sub>, u<sub>2</sub>〉<sub>BASE</sub> =〈q<sub>n</sub>, r<sub>n-1</sub>, ..., r<sub>1</sub>, r<sub>0</sub>〉<sub>base</sub>

令q<sub>n</sub> =〈r<sub>m</sub>, ..., r<sub>n</sub>〉<sub>base</sub> (m >= n)

即完成了将〈u<sub>1</sub>, u<sub>2</sub>〉<sub>BASE</sub>转成〈r<sub>m</sub>, ..., r<sub>1</sub>, r<sub>0</sub>〉<sub>base</sub>的过程。

###将大整数对象转为base进制数

设大整数对象的值为〈u<sub>n-1</sub>, ...u<sub>1</sub>, u<sub>0</sub>〉，结合前面的讨论，可以先将u<sub>n-1</sub>转成base进制数，再将〈u<sub>n-1</sub>, ...u<sub>n-2</sub>〉转成base进制数，最终将〈u<sub>n-1</sub>, ...u<sub>1</sub>, u<sub>0</sub>〉转为base进制数。显然该算法的时间复杂度为O(n<sup>2</sup>)，n与计算单元的数量有关。

###将大整数对象转为16进制数
由于16进制的特殊性，每一个字节的数值可由两个字符表示，所以如果将大整数对象按16进制转为字符串不需要前面提到的迭代过程和除法运算，在O(n)时间复杂度内可完成转换。

注：mynum参考了Donald Knuth的有关论述，完成了上述算法。





