除法
-------------

 * [全局函数](#全局函数)
 * [Number_t成员函数](#number_t成员函数)
 * [运算符](#运算符)
 * [用乘法作除法](#用乘法作除法)
 * [注意事项](#注意事项)
 * [算法](#算法)

##全局函数

Set _a_ / _b_ to _q_, and _a_ % _b_ to _r_. If _b_ is 0, the functions return 0, otherwise return 1
```C++
int div(const number_t& a, const number_t& b, number_t& q, number_t& r);
int div(const number_t& a, const number_t& b, number_t& q);
```

Set _a_ / _b_ to _q_. If _b_ is 0, the functions return 0, otherwise return 1  
```C++
int div(const number_t& a, const number_t& b, number_t& q);
```
Set _a_ / _b_ to _q_, and _a_ % _b_ to _r_  
If _q_ and _r_ refer to the same object, the behavior of this function is unexpected
```C++
int div(const number_t& a, const number_t& b, number_t& q, number_t& r);
```

_udm_ is the reciprocal of the divisor, use multiplication to do the division, return the absolute value of the remainder
```C++
unit_t div_unit(const number_t& a, const UDM& udm, number_t& res);
```

Set _a_ / _x_ to _res_ (_x_ is an ordinary integer)
```C++
void div(const number_t& a, int x, number_t& res);
void div(const number_t& a, unsigned int x, number_t& res);
void div(const number_t& a, long x, number_t& res);
void div(const number_t& a, unsigned long x, number_t& res);
void div(const number_t& a, long long x, number_t& res);
void div(const number_t& a, unsigned long long x, number_t& res);
```

Set _x_ / _b_ to _res_ (_x_ is an ordinary integer)
```C++
void div(int x, const number_t& b, number_t& res);
void div(unsigned int x, const number_t& b, number_t& res);
void div(long x, const number_t& b, number_t& res);
void div(unsigned long x, const number_t& b, number_t& res);
void div(long long x, const number_t& b, number_t& res);
void div(unsigned long long x, const number_t& b, number_t& res);
```

Return _a_ / _b_
```C++
number_t div(const number_t& a, const number_t& b);
```

##Number_t成员函数

Divide _*this_ by another number_t object _x_, _r_ is the remainder  
_r_ and _*this_ should not be the same
```C++
number_t& div(const number_t& x);
number_t& div(const number_t& x, number_t& r);
```
Divide _*this_ by an unit  
Return the absolute value of the remainder
```
unit_t div_unit(unit_t x);
unit_t div_unit(const UDM& x);
```
Divide _*this_ by a word or a signed word  
Return the absolute value of the remainder
```C++
word_t div_word(word_t x);
word_t div_sword(sword_t x);
```
Divide _*this_ by _x_ (_x_ is an ordinary integer)
```C++
number_t& div(int x);
number_t& div(unsigned int x);
number_t& div(long x);
number_t& div(unsigned long x);
number_t& div(long long x);
number_t& div(unsigned long long x);
number_t& div_unit(unit_t x);
```

##运算符
```C++
number_t& number_t::operator /= (const number_t& x);
number_t& number_t::operator /= (int x);
number_t& number_t::operator /= (unsigned int x);
number_t& number_t::operator /= (long x);
number_t& number_t::operator /= (unsigned long x);
number_t& number_t::operator /= (long long x);
number_t& number_t::operator /= (unsigned long long x);

number_t operator / (const number_t& a, const number_t& b);
number_t operator / (const number_t& a, bool b);
number_t operator / (bool a, const number_t& b);
number_t operator / (const number_t& a, char b);
number_t operator / (char a, const number_t& b);
number_t operator / (const number_t& a, short b);
number_t operator / (short a, const number_t& b);
number_t operator / (const number_t& a, int b);
number_t operator / (int a, const number_t& b);
number_t operator / (const number_t& a, long b);
number_t operator / (long a, const number_t& b);
number_t operator / (const number_t& a, long long b);
number_t operator / (long long a, const number_t& b);
number_t operator / (const number_t& a, unsigned char b);
number_t operator / (unsigned char a, const number_t& b);
number_t operator / (const number_t& a, unsigned short b);
number_t operator / (unsigned short a, const number_t& b);
number_t operator / (const number_t& a, unsigned int b);
number_t operator / (unsigned int a, const number_t& b);
number_t operator / (const number_t& a, unsigned long b);
number_t operator / (unsigned long a, const number_t& b);
number_t operator / (const number_t& a, unsigned long long b);
number_t operator / (unsigned long long a, const number_t& b);
```

##用乘法作除法

众所周知, 整数除法指令的执行效率相比于乘法指令是相当低的，往往是乘法指令的数倍，幸运地是，根据Torbjorn Granlund和Peter L. Montgomery的论文"[Division by Invariant Integers using Multiplication](https://github.com/brotherbeer/mydocument/blob/master/mynum/resource/divcnst-pldi94.pdf)", 可以将除法转为除数倒数相关的乘法。

如果除数是一个计算单元，可用UDM类获取除数的倒数，再进行除法，如：
```C++
number_t a("1234567890");
unit_t d = 123;
UDM udm(d);  // UDM: Unit Divisor to Multiplier
a.div_unit(udm); // 比直接调用a.div_unit(d)快
```
当大整数对象的值比较大时，利用UDM的除法明显比直接除法快。如果除数是可预见的，则其对应的UDM对象是可重用的。

##注意事项

如果除数为0，将不做任何计算，所以最好在做除法之前检查除数是否为0。

对于函数：
```C++
int div(const number_t& a, const number_t& b, number_t& q, number_t& r);
```
q与r不应引用同一对象，否则结果是不可预期的。

对于number_t的成员函数：
```C++
int div(const number_t& b, number_t& r);
```
r与*this不应为同一对象，否则结果是不可预期的。

##算法

《[数据存储方式](https://github.com/brotherbeer/mydocument/blob/master/mynum/Storage-ch.md)》一节指出，一个大整数对象可以理解成一个n位进制为BASE的数（n>=0），下文为简明起见，将一个具有n个数据单元的大整数对象简称为“n位数”，如无特殊声明，以下讨论中的各符号均为整数，运算符“/”、“%”表示整数除法和取余。

 * [D.0 2位数除以1位数](#D_0)
 * [D.1 3位数除以2位数](#D_1)
 * [D.2 n位数除以1位数（n > 2）](#D_2)
 * [D.3 n+1位数除以n位数（n > 3）](#D_3)
 * [D.4 任意位数之间的除法](#D_4)

###<span id="D_0">D.0 2位数除以1位数</span>

设2位被除数为〈x<sub>0</sub>, x<sub>1</sub>〉，除数为d，x<sub>0</sub>、x<sub>1</sub>、d均小于BASE，那么〈x<sub>0</sub>, x<sub>1</sub>〉在字长范围内，故可直接利用计算机的除法指令获取商和余数。
```C++
q = ((dunit_t)x0 << SHIFT | x1) / d;
r = ((dunit_t)x0 << SHIFT | x1) % d;
```
q和r分别为商和余数，BASE、SHIFT等常量可参见《[数据存储方式](https://github.com/brotherbeer/mydocument/blob/master/mynum/Storage-ch.md)》。

在实际代码中往往用__make_dunit函数将两个数据单元组成一个字：
```C++
q = __make_dunit(x0, x1) / d;
r = __make_dunit(x0, x1) % d;
```
`__make_dunit(x0, x1)`也就是〈x<sub>0</sub>, x<sub>1</sub>〉，即`(dunit_t)x0 << SHIFT | x1`。

###<span id="D_1">D.1 3位数除以2位数</span>

设3位被除数为X =〈x<sub>0</sub>, x<sub>1</sub>, x<sub>2</sub>〉，2位除数为Y =〈y<sub>0</sub>, y<sub>1</sub>〉，被除数已经超过了字长范围，故无法直接求解。

先讨论〈x<sub>0</sub>, x<sub>1</sub>〉<〈y<sub>0</sub>, y<sub>1</sub>〉时的情况：

可先用t =〈x<sub>0</sub>, x<sub>1</sub>〉/ y<sub>0</sub> 来估商，设商的实际值为Q，t一定大于或等于Q，证明参见#9。因为〈x<sub>0</sub>, x<sub>1</sub>〉< Y，故t必然小于BASE，即t可由一个数据单元记录。

然后再检验并修正t的值，当t * Y <= X时，说明t的值即为Q的值，而当t * Y > X，则说明t值偏大，t应该适当减小。
t * Y和X的值都超过了字长范围，故不能直接计算，但  

t * Y = t * y0 * BASE + t * y1 =〈x<sub>0</sub>, x<sub>1</sub>〉* BASE - r * BASE + t * y<sub>1</sub>

其中，r =〈x<sub>0</sub>, x<sub>1</sub>〉% y<sub>0</sub> 

而〈x<sub>0</sub>, x<sub>1</sub>, x<sub>2</sub>〉=〈x<sub>0</sub>, x<sub>1</sub>〉* BASE + x<sub>3</sub>

所以t * Y 与X的比较就转化成了 -r * BASE + t * y<sub>1</sub>与x<sub>3</sub>的比较，即t * y<sub>1</sub>与〈r, x<sub>2</sub>〉的比较，这时可以直接计算。

如果t * y<sub>1</sub> >〈r, x<sub>2</sub>〉，将t减1，r增加y<sub>0</sub>，再代入该不等式中，如果不等式成立，则此时t与实际值相等，如果不成立则重复将t减1、r增加y<sub>0</sub>的过程直至不等式成立，这个过程我们称为试商过程。

可以再引入一次除法来加速试商过程，设d是t与实际值的差值，即〈r + d * y<sub>0</sub>, x<sub>2</sub>〉>= (t - d) * y<sub>1</sub>，可得

r * BASE + d * y<sub>0</sub> * BASE + x<sub>2</sub> >= t * y<sub>1</sub> - d * y<sub>1</sub>

d * y<sub>0</sub> * BASE + d * y<sub>1</sub> >= t * y<sub>1</sub> - (r * BASE + x<sub>2</sub>)

d * Y >= t * y<sub>1</sub> -〈r, x<sub>2</sub>〉

故d = &#8968;(t * y<sub>1</sub> -〈r, x<sub>2</sub>〉) / Y&#8969; = (t * y<sub>1</sub> -〈r, x<sub>2</sub>〉) / Y + ((t * y<sub>1</sub> -〈r, x<sub>2</sub>〉) % Y != 0)

t - d 即为商的实际值，r + d * y<sub>0</sub>即是余数的实际值，代码如下：

```C++
dunit_t __original_div_3by2(dunit_t x0x1, unit_t x2, dunit_t y0y1, dunit_t* pr)
{
    dunit_t t, r, u, v, d;
    unit_t y0 = y0y1 >> SHIFT, y1 = y0y1 & MASK;

	assert(x0x1 <= y0y1 && y0 != 0);

    t = x0x1 / y0;
    r = x0x1 % y0;
    if (t >= BASE)
    {
        t = MASK;
        r = x0x1 - t * y0;
    }
    u = t * y1;
    v = __make_dunit(r, x2);
    if (r < BASE && u > v)
    {
        u -= v;
        d = u / y0y1 + (u % y0y1 != 0);
        t -= d;
        u = t * y1;
        v = __make_dunit(r + d * y0, x2);
    }
    *pr = v - u;  // the remainder
    return t;  // the quotient, in unit_t range
}
```
需要注意的是有时r的值会超出一个数据单元的范围，即r >= BASE，如果r >= BASE，那么t * y<sub>1</sub>的值必然小于〈r, x<sub>2</sub>〉，最后〈r + d * y<sub>0</sub>, x<sub>2</sub>〉的值也可能超出字长范围，但对余数的计算并无影响，因为余数必然在字长范围内，所以在代码中，即使忽略v溢出的高位，v - u的结果也总是正确的。

可见〈x<sub>0</sub>, x<sub>1</sub>〉<〈y<sub>0</sub>, y<sub>1</sub>〉时，本算法输出商的实际值，而当〈x<sub>0</sub>, x<sub>1</sub>〉=〈y<sub>0</sub>, y<sub>1</sub>〉时，如果仍然套用上面的算法，则t会被置为MASK即BASE - 1，这时t * y<sub>1</sub>一定小于〈r, x<sub>2</sub>〉，所以当〈x<sub>0</sub>, x<sub>1</sub>〉= Y时，会输出MASK，而实际值应为BASE，但在用到本算法的地方并不算错误，在算法D.4中会继续讨论这个问题。

对于〈x<sub>0</sub>, x<sub>1</sub>〉>〈y<sub>0</sub>, y<sub>1</sub>〉这种情况不予讨论，因为在本算法被使用的过程中，这种情况根本不会发生。

###<span id="D_2">D.2 n位数除以1位数（n > 2）</span>

设n位被除数为〈x<sub>0</sub>, x<sub>1</sub>, ..., x<sub>n-1</sub>〉，1位除数为d，结果为〈q<sub>0</sub>, q<sub>1</sub>, ..., q<sub>n-1</sub>〉，q<sub>i</sub> >= 0，i∈[0, n-1]。

可以利用一个循环得出结果：

q<sub>0</sub>, r<sub>0</sub> =〈0, x<sub>0</sub>〉/ d,〈0, x<sub>0</sub>〉% d

q<sub>1</sub>, r<sub>1</sub> =〈r<sub>0</sub>, x<sub>1</sub>〉/ d,〈r<sub>0</sub>, x<sub>1</sub>〉% d

...

q<sub>n-1</sub>, r<sub>n-1</sub> =〈r<sub>n-2</sub>, x<sub>n-1</sub>〉/ d,〈r<sub>n-2</sub>, x<sub>n-1</sub>〉% d

证明：

q<sub>n-1</sub> * d + r<sub>n-1</sub> =〈r<sub>n-2</sub>, x<sub>n-1</sub>〉

q<sub>n-2</sub> * d + r<sub>n-2</sub> =〈r<sub>n-3</sub>, x<sub>n-2</sub>〉

...

q<sub>0</sub> * d + r<sub>0</sub> = 〈0, x<sub>0</sub>〉

故〈q<sub>0</sub>, q<sub>1</sub>, ..., q<sub>n-1</sub>〉* d + r<sub>n-1</sub> =〈x<sub>0</sub>, x<sub>1</sub>, ..., x<sub>n-1</sub>〉，算法得证，r<sub>n-1</sub>即为余数。

###<span id="D_3">D.3 n+1位数除以n位数（n > 3）</span>

设n+1位除数X =〈x<sub>0</sub>, x<sub>1</sub>, ..., x<sub>n</sub>〉，n位除数Y =〈y<sub>0</sub>, y<sub>1</sub>, ..., y<sub>n-1</sub>〉，x<sub>0</sub> != 0，y<sub>0</sub> !=0，n > 3。

设  
LX =〈x<sub>3</sub>, ..., x<sub>n</sub>〉 
LY =〈y<sub>2</sub>, ..., 2<sub>n-1</sub>〉  
A = BASE<sup>n-3</sup>  
则  
X =〈x<sub>0</sub>, x<sub>1</sub>, x<sub>2</sub>〉* A + LX  
Y =〈y<sub>0</sub>, y<sub>1</sub>〉* A + LY

设
Q为X与Y进行实数除法的商，t为〈x<sub>0</sub>, x<sub>1</sub>, x<sub>2</sub>〉与〈y<sub>0</sub>, y<sub>1</sub>〉进行实数除法的商。
将t * Y与X进行比较：

t * Y = t * (〈y<sub>0</sub>, y<sub>1</sub>〉* A + LY) =〈x<sub>0</sub>, x<sub>1</sub>, x<sub>2</sub>〉* A + t * LY
X =〈x<sub>0</sub>, x<sub>1</sub>, x<sub>2</sub>〉* A + LX

所以t * Y与X进行比较，即是将t * LY与LX进行比较。

1. 如果t * LY <= LX  
显然，0 < X - &#8970;t&#8971; * Y < Y，&#8970;t&#8971;即是整数除法的商

2. 如果t * LY > LX  
说明t大于实际值Q，此时t比Q大了多少呢，可以考察t - 1与Q的关系。

Q * Y = X =〈x<sub>0</sub>, x<sub>1</sub>, x<sub>2</sub>〉* A + LX

(t - 1) * Y = (t - 1) * (〈y<sub>0</sub>, y<sub>1</sub>〉* A + LY) =〈x<sub>0</sub>, x<sub>1</sub>, x<sub>2</sub>〉* A - 〈y<sub>0</sub>, y<sub>1</sub>〉* A + (t - 1) * LY

因为y<sub>0</sub> != 0，所以〈y<sub>0</sub>, y<sub>1</sub>〉* A是一个n位数，LY最大为n - 2位数，

如果t <= BASE，则t - 1 < BASE，(t - 1) * LY最大是n - 1位数，-〈y<sub>0</sub>, y<sub>1</sub>〉* A + (t - 1) * LY必为负数，故(t - 1) * Y 必然会小于X，说明t - 1 < Q，所以t与实际值Q的差值不会超过1。

如果t > BASE，t与Q的差值将难以估计，所以我们规定本算法的前提条件为〈x<sub>0</sub>, x<sub>1</sub>〉<=〈y<sub>0</sub>, y<sub>1</sub>〉，从而保证t <= BASE。

结合1、2两种情况，考虑X与Y的整数除法，可以利用算法D.1求出t =〈x<sub>0</sub>, x<sub>1</sub>, x<sub>2</sub>〉/〈y<sub>0</sub>, y<sub>1</sub>〉的值，t这里为整数，则X / Y的值可能是t也可能是t - 1，不会有第三种可能。

在本算法的实际使用中，X的高n位总是小于Y，所以t的值小于BASE，可由一个数据单元记录。

利用算法M.4，求出R = X - t * Y的值，R即为余数，如果没有借位，t和R即为整数除法的结果，如果出现借位，t减1，R加上Y，即为最终结果。

###<span id="D_4">D.4 任意位数之间的除法</span>

设被除数X为m位，除数Y为n位(n > 0, m > 0)。

显然，当n > m时，商为0，余数为X。

当n <= m时，如果Y为1位数，由可由算法D.2求得结果，下以讨论Y的位数大于等于2的情况。

如果X的最高单元大于或等于Y的最高单元，则将X的最高单元更高的单元置0，m增1，从而保证了X的高n位一定小于Y，则商必为m - n位数，也保证了算法D.3的前提条件。

任意位数之间的除法，其原理与算法D.2是相同的，可以将n位除数Y视作一个整体，利用算法D.3，每次用X的高n + 1位除以Y，得到一个商值，并将余数写回X的高n + 1位，写回余数后X的最高单元为0，即X的位数会减1，所以重复这样的除法直到X的位数与Y相同，每次求得的商从高位到低位排列，即是原X除以Y的商，最后X的值即为余数。

每次用X的高n + 1位除以Y时，算法D.3的前提条件都是满足的，而且X的高n位都小于Y，每次用算法D.1估商的值都应该小于BASE，即可用一个数据单元记录。

有一个特殊情况，设〈x<sub>0</sub>, x<sub>1</sub>〉为X最高位的两个单元，〈y<sub>0</sub>, y<sub>1</sub>〉是Y最高位的两个单元，〈x<sub>0</sub>, x<sub>1</sub>〉与〈y<sub>0</sub>, y<sub>1</sub>〉有可能相等，这时用算法D.1来估商得到MASK，可以证明本次除法商的实际值就是MASK。

证明：  
设X =〈x<sub>0</sub>, x<sub>1</sub>, ..., x<sub>n</sub>〉  
Y =〈y<sub>0</sub>, y<sub>1</sub>, ..., y<sub>n-1</sub>〉  
LX =〈x<sub>2</sub>, ..., x<sub>n-1</sub>〉 
LY =〈y<sub>2</sub>, ..., y<sub>n-1</sub>〉 

x<sub>0</sub> = y<sub>0</sub>，x<sub>1</sub> = y<sub>1</sub>

X - Y * MASK = X - Y * BASE + Y = (LX - LY) * BASE + x<sub>n</sub> + Y

-LY <= LX - LY <= -1，x<sub>n</sub> < BASE

LY 最大为n-2位数，所以0 < X - Y * MASK < Y，故X / Y的值为MASK。

至此关于除法的算法暂告一段落。
