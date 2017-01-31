mynum的数据存储方式
-------------

`注意：目前mynum只适用于小尾序机型（即整数的低位存储在低地址，高位存储在高地址）。`

大整数类即number_t类，在内存中以二进制方式存储数据，在原理上与C语言整数类型的存储方式相似，但不受固定内存空间的限制。例如，用4个字节的int型变量存储整数0xabcdef，那么这个int变量的4个字节从低地址址到高地址依次为0xef、0xcd、0xab、0x00，number_t对象的存储方式与之相同，如果构造一个值为0xabcdef的number_t对象，该对象用一个数组记录整数的值，数组的第一个字节是0xef，第二个字节是0xcd，第三个字节是0xab。当一个整数需要n个字节存储时，相应的number_t对象会至少分配n个字节来存放数据，当有其它number_t对象与之相加或相乘时，其内存空间还会动态增大。

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
const unit_t  SHIFT = sizeof(unit_t) << 3;
const dunit_t BASE = (dunit_t)1 << SHIFT;
const unit_t  MASK = ~unit_t(0);
```
其中，unit_t是一个系统相关的无符号整数类型，在64位系统中为32位(unsigned int)，在32位系统中为16位(unsigned short)。
unit_t是mynum基本计算单元的类型，其位数记为SHIFT，最大值记为MASK，以下unit_t型变量简称计算单元或单元。dunit_t为无符号基本整数类型，其位数是unit_t的2倍。slen_t是有符号整数类型，用以表示长度。

因为number_t对象在内存中用二进制方式存储数据，一个内存比特位记录大整数的一个二进制位，所有比特位都是连续的，所以可以将其理解为具有连续内存地址的计算单元序列，成员变量dat指向该序列，len的绝对值表示该序列中有效单元的个数，cap表示序列中所有单元的个数，cap永远大于或等于len的绝对值，len的符号表示number_t对象的符号，即len < 0时为负数，len > 0时为正数，len = 0时为0。

显然，可以将计算单元序列理解成一个具有n位进制为BASE的数(n=abs(len); BASE=MASK+1)，第i位的值即是第i个单元U<sub>i</sub>的值(n > i >= 0)，这个数的值即是number_t对象的值，其值为：U<sub>n-1</sub> \* BASE<sup>n-1</sup> + ... + U<sub>1</sub> \* BASE + U<sub>0</sub>

对于任意的正整数n，i，b，d<sub>i</sub>，如果i∈[0,n)，d<sub>i</sub> < b，
可以将式子：d<sub>n-1</sub> \* b<sup>n-1</sup> + ... + d<sub>1</sub> \* b + d<sub>0</sub> 简写为：〈d<sub>n-1</sub>, ..., d<sub>1</sub>, d<sub>0</sub>〉<sub>b</sub>，其中下标b如果省略则b的值为BASE。

再举一个例子，构造一个number_t对象，其值为0xaaaabbbbccccddddeeeeffff，  
在32位系统中，其单元序列为:〈0xaaaa, 0xbbbb, 0xcccc, 0xdddd, 0xeeee, 0xffff〉<sub>0x10000</sub>  
在64位系统中，其单元序列为:〈0xaaaabbbb, 0xccccdddd, 0xeeeeffff〉<sub>0x100000000</sub>

根据表示16进制数的字符串"aaaabbbbccccddddeeeeffff"来构造number_t对象还是比较简单的，我们将在后面讨论如何用表示其它进制数的字符串构造number_t对象。

一个计算单元的大小是字长的二分之一，dunit_t表示字长大小的整数类型，我们便可以利用标准C/C++语言获取各计算单元在运算时的进位或借位信息。
```C++
// res = a + b, and return the carry
unit_t add(unit_t a, unit_t b, unit_t& res)
{
    dunit_t sum = (dunit_t)a + b;
    *res = sum & MASK;
    return sum >> SHIFT;
}

// res = a * b + c, and return the carry
unit_t muladd(unit_t a, unit_t b, unit_t c, unit_t& res)
{
    dunit_t sum = (dunit_t)a * b + c;
    *res = sum & MASK;
    return sum >> SHIFT;
}
```
0xffff * 0xffff + 0xffff = 0xffff0000，所以这些函数在32位环境中不会产生溢出错误，同理在64位环境中也不会溢出

综上所述，现在我们可以给出number_t对象与一个计算单元的乘法和加法，
已知dat为unit_t型指针，指向计算单元序列，len为数组元素个数（暂不考虑负数的情况），伪代码如下（为简明起见，略去一些细节）：
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

slen_t 也是一个系统相关的类型，在64位系统中为64位有符号整数(long long)，在32位系统中为32位有符号整数(int)。slen_t型的变量多用来表求计算单元的个数，其最大值在32位系统中为2147483647（2Gb），在64位系统中为9223372036854775807（8191Pb），可以说，在内存条件允许的条件下，number_t可以表示任意大的整数。

下一章《[大整数对象的初始化](https://github.com/brotherbeer/mydocument/blob/master/mynum/Initialization-ch.md)》
