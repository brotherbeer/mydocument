<h1>数据存储方式</h1>

`注意：目前mynum只适用于小尾序机型（即整数的低位存储在低地址，高位存储在高地址）。`

Mynum的大整数类名为number_t，在内存中以二进制方式存储数据，一个内存比特位记录大整数的一个二进制位，且所有比特位都是连续的。其原理上与C语言整数类型的存储方式相似，但不受固定内存空间的限制。例如，用4个字节的int型变量存储整数0xabcdef，那么这个int变量的4个字节从低地址址到高地址依次为0xef、0xcd、0xab、0x00，如果构造一个值为0xabcdef的number_t对象，会在堆上分配一个数组，数组的第一个字节是0xef，第二个字节是0xcd，第三个字节是0xab。当一个整数需要n个字节的空间时，相应的number_t对象会至少分配n个字节来存放数据，当有其它数据与之相加或相乘时，其内存空间还会动态增大。

为了便于管理数据以及提高运算速度，将相临的2个或4个字节分为一组，视作一个整型变量，这样的整型变量称为“数据单元”。据有连续地址的数据单元序列组成了大整数的数据。

number_t有三个重要的成员变量：
```C++
struct number_t {
    unit_t* dat;
    slen_t len;
    slen_t cap;

    // other members omitted...
};
```
相关常量：
```C++
const unit_t UNITMAX = ~unit_t(0);
const dunit_t BASE = (dunit_t)1 << UNITBITS;
```
unit_t即数据单元的类型，是一个系统相关的无符号整数类型，在64位系统中为32位(unsigned int)，在32位系统中为16位(unsigned short)，其位数记为UNITBITS，最大值记为UNITMAX。成员变量dat指向数据单元序列，存储在低地址的单元记录大整数的低位，高地址的单元记录大整数的高位，存储在最高地址的单元简称为最高单元。slen_t是有符号整数类型，len的绝对值表示有效单元的个数，其符号表示number_t对象的符号，即len < 0时为负数，len > 0时为正数，len = 0时为0。cap表示所有单元的个数，cap永远大于或等于len的绝对值。

显然，可以将具有n个数据单元的序列理解成一个具有n位进制为BASE的数(n >= 0; BASE = UNITMAX + 1)，第i位的值即是第i个单元U<sub>i</sub>的值(i∈[0, n)，这个数的值即是number_t对象的值：U<sub>n-1</sub> \* BASE<sup>n-1</sup> + ... + U<sub>1</sub> \* BASE + U<sub>0</sub>

对于任意的正整数n、i、b、d<sub>i</sub>，i∈[0, n)，d<sub>i</sub> < b，
可以将式子：d<sub>n-1</sub> \* b<sup>n-1</sup> + ... + d<sub>1</sub> \* b + d<sub>0</sub> 简写为：〈d<sub>n-1</sub>, ..., d<sub>1</sub>, d<sub>0</sub>〉<sub>b</sub>，其中下标b如果省略则b的值为BASE。

再举一个例子，构造一个number_t对象，其值为0xaaaabbbbccccddddeeeeffff，  
在32位系统中，其单元序列为:〈0xaaaa, 0xbbbb, 0xcccc, 0xdddd, 0xeeee, 0xffff〉<sub>0x10000</sub>  
在64位系统中，其单元序列为:〈0xaaaabbbb, 0xccccdddd, 0xeeeeffff〉<sub>0x100000000</sub>

根据表示16进制数的字符串"aaaabbbbccccddddeeeeffff"来构造number_t对象还是比较简单的，我们将在后面讨论如何用表示其它进制数的字符串构造number_t对象。

大整数之间的运算也就是数据单元之间的运算，对于两个数据单元而言，加法和乘法有可能溢出，减法可能产生借位，引入dunit_t类型可以解决这个问题。dunit_t亦为无符号整型，其位数是unit_t的2倍。unit_t为字长(word size)的二分之一，dunit_t的位数与字长相同，我们便可以利用标准C/C++语言获取各数据单元在运算时的进位或借位信息。
```C++
// *res = a + b, and return the carry
unit_t add(unit_t a, unit_t b, unit_t& res)
{
    dunit_t sum = (dunit_t)a + b;
    *res = sum & UNITMAX;
    return sum >> UNITBITS;
}

// *res = a * b + c, and return the carry
unit_t muladd(unit_t a, unit_t b, unit_t c, unit_t& res)
{
    dunit_t sum = (dunit_t)a * b + c;
    *res = sum & UNITMAX;
    return sum >> UNITBITS;
}
```
0xffff * 0xffff + 0xffff = 0xffff0000，所以这些函数在32位环境中不会产生溢出错误，同理在64位环境中也不会溢出

综上所述，现在我们可以给出number_t对象与一个数据单元的乘法和加法，
已知dat为unit_t型指针，指向数据单元序列，len为数组元素个数（暂不考虑负数），伪代码如下（为简明起见，略去一些细节）：
```C++
number_t::mul_unit(unit_t x)
{
    unit_t carry = 0;
    for (slen_t i = 0; i < len; i++)
    {
        carry = muladd(dat[i], x, carry, &dat[i]);
    }
    if (carry)
    {
        dat[len++] = carry; // 假设有充足空间
    }
}

number_t::add_unit(unit_t x)
{
    unit_t carry = add(dat[0], x, &dat[0])
    for (slen_t i = 1; i < len && carry != 0; i++)
    {
        carry = add(dat[i], carry, &dat[i]);
    }
    if (carry)
    {
        dat[len++] = carry;
    }
}
```

slen_t 也是一个系统相关的类型，在64位系统中为64位有符号整数(long long)，在32位系统中为32位有符号整数(int)。slen_t型的变量多用来表求数据单元的个数，其最大值在32位系统中为2147483647（2Gb），在64位系统中为9223372036854775807（8191Pb），可以说，在内存条件允许的条件下，number_t可以表示任意大的整数。

下一章《[大整数对象的初始化](https://github.com/brotherbeer/mydocument/blob/master/mynum/Initialization-ch.md)》
