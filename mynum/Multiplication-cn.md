乘法
-------------

 * [全局函数](#全局函数)
 * [Number_t成员函数](#number_t成员函数)
 * [运算符](#运算符)
 * [算法](#算法)

##全局函数

用基本算法求a与b的乘积res
```C++
void mul(const number_t& a, const number_t& b, number_t& res);
```

用Karatsuba算法求a与b的乘积res
```C++
void kmul(const number_t& a, const number_t& b, number_t& res);
```

用NTT(Number Theoretic Transform)算法求a与b的乘积res
```C++
void fmul(const number_t& a, const number_t& b, number_t& res);
```

求a与x的乘积res，x为一个数据单元
```C++
void mul_unit(const number_t& a, unit_t x, number_t& res);
```

求a与x的乘积res，x为基本整型
```C++
void mul(const number_t& a, int x, number_t& res);
void mul(const number_t& a, unsigned int x, number_t& res);
void mul(const number_t& a, long x, number_t& res);
void mul(const number_t& a, unsigned long x, number_t& res);
void mul(const number_t& a, long long x, number_t& res);
void mul(const number_t& a, unsigned long long x, number_t& res);
```

求x与a的乘积res，x为基本整型
```C++
void mul(int x, const number_t& a, number_t& res);
void mul(unsigned int x, const number_t& a, number_t& res);
void mul(long x, const number_t& a, number_t& res);
void mul(unsigned long x, const number_t& a, number_t& res);
void mul(long long x, const number_t& a, number_t& res);
void mul(unsigned long long x, const number_t& a, number_t& res);
```

用基本算法求a的平方res
```C++
void sqr(const number_t& a, number_t& res);
```

用Karatsuba算法求a的平方res
```C++
void ksqr(const number_t& a, number_t& res);
```

用NTT(Number Theoretic Transform)算法求a的平方res
```C++
void fsqr(const number_t& a, number_t& res);
```

##Number_t成员函数

与另一个number_t对象相乘
```C++
number_t& number_t::mul(const number_t& x);
number_t& number_t::kmul(const number_t& x);
```
与一个数据单元相乘
```C++
void number_t::mul_unit(unit_t x);
```
与一个字相乘
```C++
void number_t::mul_word(word_t x);
void number_t::mul_sword(sword_t x);
```
与基本整型变量相乘
```C++
number_t& number_t::mul(int x);
number_t& number_t::mul(unsigned int x);
number_t& number_t::mul(long x);
number_t& number_t::mul(unsigned long x);
number_t& number_t::mul(long long x);
number_t& number_t::mul(unsigned long long x);
```

##运算符
```C++
number_t& number_t::operator *= (const number_t& x);
number_t& number_t::operator *= (int x);
number_t& number_t::operator *= (unsigned int x);
number_t& number_t::operator *= (long x);
number_t& number_t::operator *= (unsigned long x);
number_t& number_t::operator *= (long long x);
number_t& number_t::operator *= (unsigned long long x);

number_t operator * (const number_t& a, const number_t& b);
number_t operator * (const number_t& a, bool b);
number_t operator * (bool a, const number_t& b);
number_t operator * (const number_t& a, char b);
number_t operator * (char a, const number_t& b);
number_t operator * (const number_t& a, short b);
number_t operator * (short a, const number_t& b);
number_t operator * (const number_t& a, int b);
number_t operator * (int a, const number_t& b);
number_t operator * (const number_t& a, long b);
number_t operator * (long a, const number_t& b);
number_t operator * (const number_t& a, long long b);
number_t operator * (long long a, const number_t& b);
number_t operator * (const number_t& a, unsigned char b);
number_t operator * (unsigned char a, const number_t& b);
number_t operator * (const number_t& a, unsigned short b);
number_t operator * (unsigned short a, const number_t& b);
number_t operator * (const number_t& a, unsigned int b);
number_t operator * (unsigned int a, const number_t& b);
number_t operator * (const number_t& a, unsigned long b);
number_t operator * (unsigned long a, const number_t& b);
number_t operator * (const number_t& a, unsigned long long b);
number_t operator * (unsigned long long a, const number_t& b);
```

##算法

本节讨论任意大整数之间乘法的算法。

《[数据存储方式](https://github.com/brotherbeer/mydocument/blob/master/mynum/Storage-ch.md)》一章指出，一个大整数对象可以理解成一个n位进制为BASE的数（n >= 0），下文为简明起见，将一个具有n个数据单元的大整数对象简称为“n位数”，如无特殊声明，以下讨论中的各符号均为整数，运算符“*”、“+”表示整数乘法和加法，“=”表示相等。

 * [M.0 1位数乘1位数再与1位数相加](#M0)
 * [M.1 n位数乘以1位数（n > 1）](#M1)
 * [M.2 任意位数之间的基本乘法](#M2)
 * [M.3 任意位数的基本平方算法](#M3)
 * [M.4 n+1位数减去n位数乘以1位数的积（n >= 2）](#M4)
 * [M.5 Karatsuba算法](#M5)
 * [M.6 NTT算法](#M6)

<h3 id="M0">M.0 1位数乘1位数再与1位数相加</h3>

设a、b、c为1位数，即1个数据单元，a * b + c的结果需要用2个数据单元记录，低位单元为计算结果，高位单元为进位，代码如下：
```C++
// M.0.0
unit_t mul_add(unit_t a, unit_t b, unit_t c, unit_t* res)
{
    dunit_t sum = (dunit_t)a * b + c;
    *res = sum & UNITMAX;
    return sum >> UNITBITS;
}
```
该算法将res指向的单元设为结果，并返回进位。

1个计算单元的最大值为BASE-1，1个字(word)的最大值为BASE<sup>2</sup> - 1，2个具有最大值的计算单元相乘后再与1个最大值的单元相加：  

(BASE - 1)<sup>2</sup> + BASE - 1 = BASE<sup>2</sup> - BASE < BASE<sup>2</sup> - 1

即结果不会超出字长范围，所以这段代码的是可靠的，不难发现，2个具有最大值的计算单元相乘后再与2个最大值的单元相加，结果刚好为BASE<sup>2</sup> - 1，也不会溢出，可给出mul_add函数的一个重载，计算a * b + c + d，d亦为一个数据单元：
```C++
// M.0.1
unit_t mul_add(unit_t a, unit_t b, unit_t c, unit_t d, unit_t* res)
{
    dunit_t sum = (dunit_t)a * b + c + d;
    *res = sum & UNITMAX;
    return sum >> UNITBITS;
}
```

<h3 id="M1">M.0 n位数乘以1位数（n > 1）</h3>

设X =〈x<sub>n-1</sub>, ..., x<sub>1</sub>, x<sub>0</sub>〉为n位数，y为1位数，X与y的乘积为〈z<sub>n</sub>, ..., z<sub>1</sub>, z<sub>0</sub>〉，0 <= z<sub>i</sub> < BASE，i∈[0, n]，X与y的积可能有n + 1位：  
```C++
slen_t __mul_unit_core(const unit_t* x, slen_t n, unit_t y, unit_t* z)
{
    unit_t carry = 0;
    const unit_t* e = x + n;

    for (; x != e; x++, z++)
    {
        carry = mul_add(*x, *y, carry, z);  // M.0.0
    }
	if (carry)
	{
		n++;
		*z = carry;
	}
	return n;
}
```
其中指针x指向X的数据单元序列，z指向结果数据单元序列，结果单元序列至少包函n + 1个单元。该函数返回结果的位数，即单元个数。  
请注意，具体实现中，存储在低地址的数据单元记录大整数数值的低位，存储在高地址的单元记录数值的高位。表达式〈x<sub>n-1</sub>, ..., x<sub>1</sub>, x<sub>0</sub>〉中左侧的单元表示高位，右侧的单元表示低位，单元的下标仅作单元区分之用，与高低位无关。

<h3 id="M2">M.2 任意位数之间的基本乘法</h3>

设m位数X =〈x<sub>m-1</sub>, ..., x<sub>1</sub>, x<sub>0</sub>〉，n位数Y =〈y<sub>n-1</sub>, ..., y<sub>1</sub>, y<sub>0</sub>〉(m >= 0, n >= 0)，显然如果m与n有一者为0，结果即为0，下面讨论m、n均不为0的情况。任意位数之间的基本乘法我们在小学的时候已经学过了，这里复习一下，用一个求和公式表达较为清晰：

X * Y = Σ(x<sub>i</sub> * Y * BASE<sup>i</sup>) i=0 → m-1

i从0到m-1的每一步中，计算x<sub>i</sub> * Y * BASE<sup>i</sup>并与上一步的结果相加，利用算法M.0.1可以作到即乘即加，与BASE<sup>i</sup>不必做实际的乘法，只需从上一步结果的第i个单元开始相加即可。结果单元序列至少包含m + n个单元，并且在计算之前应被清零。

```C++
slen_t __mul_core(const unit_t* x, slen_t m, const unit_t* y, slen_t n, unit_t* res)
{
    unit_t carry = 0, xi;
    unit_t *pr, *rb = res;
    const unit_t *ex = x + m;
    const unit_t *ey = y + n, *py;

    for (; x != ex; x++, rb++)
    {
        for (xi = *x, py = y, pr = rb; py < ey; py++, pr++)
        {
			carry = mul_add(xi, *py, *pr, carry, pr);  // M.0.1
        }
        if (carry)
        {
            *pr = carry;
            carry = 0;
        }
    }
    m += n;
    __trim_leading_zeros(res, m);
    return m;
}
```
其中指针x指向X的单元序列，y指向Y的单元序列，res指向结果的单元序列。ex、ey分别指向X和Y的单元序列末尾，rb指向上一步计算结果的单元序列，在外层循环中每次增1，即实现了x<sub>i</sub> * Y与BASE<sup>i</sup>相乘。__trim_leading_zeros是一个宏，处理高位的零单元，请参见减法算法描述。

显然，算法的时间复杂度为O(m * n)。注意，考虑到代码的优化，本节讨论的算法代码与mynum的具体实现并不完全相同，但在原理上是一致的。

<h3 id="M3">M.3 任意位数的基本平方算法</h3>

整数求平方也可由算法M.2计算，但由于两个乘数完全相同，故可以进行一定的特殊处理。

以4位数〈x<sub>0</sub>, x<sub>1</sub>, x<sub>2</sub>, x<sub>3</sub>〉的平方为例，在用M.2算法求结果时，有相当一部分计算是重复的：


图中(i * j)表示x<sub>i</sub> * x<sub>j</sub> (i, j∈[0, 4])，下划线表示重复的计算。

不难发现规律，对于任意n位大整数X =〈x<sub>n-1</sub>, ..., x<sub>1</sub>, x<sub>0</sub>〉

X<sup>2</sup> = Σ((x<sub>i</sub> * x<sub>i</sub> + 2 * x<sub>i</sub> *〈x<sub>n-1</sub>, ..., x<sub>i+1</sub>〉) * BASE<sup>2i</sup>) i=0 → n-1

要注意的是2 * x<sub>i</sub>可能超出了一个单元的范围，这时需要分两种情况处理，具体代码请参见__sqr_core函数，此算法比用M.2求平方快一倍，但其时间复杂度仍为O(n<sup>2</sup>)。

<h3 id="M4">M.4 n+1位数减去n位数乘以1位数的积（n >= 2）</h3>
此算法融合了加法减法以及除法，在大整数除法中此算法起到了关键作用。
设大整数X为n+1位，Y为n位，z为1位，求X - Y * z的代码如下： 
```C++
unit_t __sub_mul(unit_t* x, const unit_t* y, slen_t n, unit_t z)
{
    const unit_t *ey = y + n;
    unit_t borrow = 0, carry = 0, s;

    for (; y != ey; x++, y++)
    {
		carry = mul_add(z, *y, carry, &s);
		borrow = sub_with_borrow(*x, s, borrow, x);
    }
	return sub_with_borrow(*x, carry, borrow, x);
}
```
其中，指针x指向X的单元序列，y指向Y的单元序列，如果存在借位则返回1，否则返回0, sub_with_borrow参见减法算法。在mynum的实际代码中，考虑到函数调用的成本，mul_add、sub_with_borrow等函数均被展开，但原理是一致的。

<h3 id="M5">Karatsuba算法</h3>

<h3 id="M6">NTT算法</h3>

	



