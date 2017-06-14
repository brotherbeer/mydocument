<h1>大整数对象转为字符串</h1>

 * [成员函数](#memberfunctions)
 * [输出流运算符](#ostreamoperator)
 * [注意事项](#attentions)
 * [示例](#examples)
 * [算法](#algorithms)

<h2 id="memberfunctions">成员函数</h2>

按2进制转为字符串str
```C++
string_t& to_bin_string(string_t& str) const;
```
按8进制转为字符串str
```C++
string_t& to_oct_string(string_t& str) const;
```
按10进制转为字符串str
```C++
string_t& to_dec_string(string_t& str) const;
```
按16进制转为字符串str
```C++
string_t& to_hex_string(string_t& str) const;
```
按base进制转为字符串str
```C++
string_t& to_string(string_t& str, int base = 10) const;
```
返回对象
```C++
string_t to_bin_string() const;
string_t to_oct_string() const;
string_t to_dec_string() const;
string_t to_hex_string() const;
string_t to_string(int base = 10) const;
```
重载()，按base进制返回字符串对象
```C++
string_t operator () (int base) const;
```

<h2 id="ostreamoperator">输出流运算符</h2>

```C++
std::ostream& operator << (std::ostream& os, const number_t& a)
```

<h2 id="attentions">注意事项</h2>

为了更高的效率，所有与字符串转换相关的成员函数不会成生前导字符串或空白符，并只用小写字母。 
当然，mynum可以将大整数对象转为具有复杂格式的字符串，如用format_t类的dump函数，具体请参见《[大整数对象转为格式化字符串](https://github.com/brotherbeer/mydocument/blob/master/mynum/Formatted-output-ch.md)》

将大整数对象按16进制转为字符串的时间复杂度最低。

<h2 id="examples">示例</h2>

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

<h2 id="algorithms">算法</h2>

根据前文，大整数对象的值相当于一个BASE进制的数，各数据单元的值即是其各位的值，将一个有n个单元(n>=0)的大整数对象转为任意进制数，即是将
〈u<sub>n-1</sub>, ..., u<sub>1</sub>, u<sub>0</sub>〉<sub>BASE</sub>转为〈r<sub>m-1</sub>, ..., r<sub>1</sub>, r<sub>0</sub>〉<sub>base</sub>的过程，base为任意进制，转换后的base进制数有m位，r<sub>i</sub>为其各位数值(0 <= i < m)。将r<sub>i</sub>依次转为字符串，大整数对象便转成了字符串。

**当n为1时：**

设u为一个数据单元，即0 <= u < BASE，将u转为base进制数可由以下循环完成，其中d为一个数组，记录u转为base进制数后各位数值，i为数组元素下标：
```C++
for (i = 0; u != 0; i++)
{
	d[i] = u % base;
	u /= base;
}
```

**当n为2时：**

设u<sub>1</sub>、u<sub>2</sub>为两个数据单元，它们组成整数〈u<sub>1</sub>, u<sub>2</sub>〉<sub>BASE</sub>，
根据上一步的结论，可先将u<sub>1</sub>转为base进制数，设其有k位，即〈d<sub>k</sub>, ..., d<sub>1</sub>, d<sub>0</sub>〉<sub>base</sub>

〈u<sub>1</sub>, u<sub>2</sub>〉<sub>BASE</sub> =〈d<sub>k</sub>, ..., d<sub>1</sub>, d<sub>0</sub>〉<sub>base</sub> * BASE + u<sub>2</sub> =〈d<sub>k</sub> \* BASE, ..., d<sub>1</sub> \* BASE, d<sub>0</sub> \* BASE + u<sub>2</sub>〉<sub>base</sub>


设d<sub>0</sub> \* BASE + u<sub>2</sub> = q<sub>0</sub> \* base + r<sub>0</sub>，r<sub>0</sub> < base:

〈u<sub>1</sub>, u<sub>2</sub>〉<sub>BASE</sub> = 〈d<sub>k</sub> \* BASE, ..., d<sub>1</sub> \* BASE, q<sub>0</sub> \* base + r<sub>0</sub>〉<sub>base</sub> =〈d<sub>k</sub> \* BASE, ..., d<sub>2</sub> \* BASE, d<sub>1</sub> \* BASE + q<sub>0</sub>, r<sub>0</sub>〉<sub>base</sub>

设d<sub>1</sub> \* BASE + q<sub>0</sub> = q<sub>1</sub> \* base + r<sub>1</sub>，r<sub>1</sub> < base:

〈u<sub>1</sub>, u<sub>2</sub>〉<sub>BASE</sub> =〈d<sub>k</sub> \* BASE, ..., d<sub>2</sub> \* BASE + q<sub>1</sub>, r<sub>1</sub>, r<sub>0</sub>〉<sub>base</sub>

显然，利用相同的方法令d<sub>i</sub> \* BASE + q<sub>i-1</sub> = q<sub>i</sub> \* base + r<sub>i</sub>，即q<sub>i</sub> = (d<sub>i</sub> \* BASE + q<sub>i-1</sub>) / base, r<sub>i</sub> = (d<sub>i</sub> \* BASE + q<sub>i-1</sub>) % base，i >= 1，可得：

〈u<sub>1</sub>, u<sub>2</sub>〉<sub>BASE</sub> =〈q<sub>n</sub>, r<sub>n-1</sub>, ..., r<sub>1</sub>, r<sub>0</sub>〉<sub>base</sub>

其中d<sub>i</sub> \* BASE + q<sub>i-1</sub>的结果为一个dunit_t型变量，其高位设为d<sub>i</sub>，低位设为q<sub>i-1</sub>即可，无需乘法和加法计算。

如果q<sub>n</sub> >= base，与n为1时相似，将q<sub>n</sub>转为base进制的序列〈r<sub>m-1</sub>, ..., r<sub>n</sub>〉<sub>base</sub>

即完成了将〈u<sub>1</sub>, u<sub>2</sub>〉<sub>BASE</sub>转成〈r<sub>m-1</sub>, ..., r<sub>1</sub>, r<sub>0</sub>〉<sub>base</sub>的过程。

**当n > 2时：**

设大整数对象的值为〈u<sub>n-1</sub>, ...u<sub>1</sub>, u<sub>0</sub>〉，结合前面的讨论，可以先将u<sub>n-1</sub>转成base进制数，再将〈u<sub>n-1</sub>, ...u<sub>n-2</sub>〉转成base进制数，最终将〈u<sub>n-1</sub>, ...u<sub>1</sub>, u<sub>0</sub>〉转为base进制数。显然该算法的时间复杂度为O(n<sup>2</sup>)，n与数据单元的数量有关。

大整数对象转任意进制数的讨论至此完毕。

**将大整数对象转为16进制数**
由于16进制的特殊性，每一个字节的数值可由两个字符表示，所以如果将大整数对象按16进制转为字符串不需要前面提到的迭代过程和除法运算，在O(n)时间复杂度内可完成转换。

注：mynum参考了Donald Knuth的有关论述，完成了上述算法。
