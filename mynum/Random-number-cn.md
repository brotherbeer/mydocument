<h1>随机数</h1>

 * [随机数生成器](#rng)
 * [函数](#functions)
 * [注意事项](#attentions)
 * [算法](#algorithms)

<h2 id="rng">随机数生成器</h2>

<h3>随机数生成器虚基类</h3>


```C++
struct RNG
{
    virtual word_t gen() = 0;

    virtual bool valid() const = 0;

    virtual bool gen_bytes(void* buf, size_t n);

	virtual ~RNG() {}
};
```
接口定义：

返回随机数
```C++
word_t gen();
```
在buf指向的连续内存空间中，成生n个字节的随机数，成功返回true，失败返回false
```C++
bool gen_bytes(void* buf, size_t n);
```
生成器当前可用返回true，否则返回false
```
bool valid() const;
```

<h3>原始线性同余生成器</h3>
```
struct LCG_t;
```

<h3>改进的线性同余生成器</h3>
```
struct XLCG_t;
```

<h3>异或移位生成器</h3>
```C++
struct XORSP_t: public RNG
```

<h3>加密随机数生成器</h3>
```C++
struct CRNG_t: public RNG
```

<h2 id="functions">函数</h2>

返回当前默认成生器的引用
```C++
RNG& default_RNG();
```

设置当前默认成生器
```C++
void set_default_RNG(RNG& rng);
```

获取随机数种子
```C++
word_t get_seed();
```

用默认生成器生成unit_t型的随机数
```C++
unit_t rand_unit();
```

用默认生成器生成word_t型的随机数
```C++
word_t rand_word();
```

用默认生成器以1 / n的概率返回true
```C++
bool chance(size_t n);
```

用默认生成器生成二进制位数不超过maxbits的随机数n  
成功返回true，失败返回false
```C++
bool rand(size_t maxbits, number_t& n);
```

用默认生成器生成二进制位数不超过maxbits的随机数n  
如果holdmsb为ture，则n一定为maxbits位  
成功返回true，失败返回false
```C++
bool rand(size_t maxbits, bool holdmsb, number_t& n);
```

用默认生成器生成二进制位数在[minbits, maxbits]之间均匀分布的随机数n  
成功返回true，失败返回false
```C++
bool rand(size_t minbits, size_t maxbits, number_t& n);
```

用默认生成器随机挑选chars中的字符，生成长度为length的随机字符串s  
成功返回true，失败返回false
```C++
bool rand(size_t length, const string_t& chars, string_t& s);
```

用指定的生成器rng生成二进制位数不超过maxbits的随机数n  
成功返回true，失败返回false
```C++
bool rand(size_t maxbits, RNG& rng, number_t& n);
```

用指定的生成器rng生成二进制位数不超过maxbits的随机数n  
如果holdmsb为ture，则n一定为maxbits位  
成功返回true，失败返回false
```C++
bool rand(size_t maxbits, RNG& rng, bool holdmsb, number_t& n);
```

用指定的生成器rng生成二进制位数在[minbits, maxbits]之间均匀分布的随机数n  
成功返回true，失败返回false
```C++
bool rand(size_t minbits, size_t maxbits, RNG& rng, number_t& n);
```

用指定的生成器rng随机挑选chars中的字符，生成长度为length的随机字符串s  
成功返回true，失败返回false
```C++
bool rand(size_t length, const string_t& chars, RNG& rng, string_t& s);
```

<h2 id="attentions">注意事项</h2>

`bool rand(size_t maxbits, RNG& rng, number_t& n)` 函数并非生成二进制位数在[0, maxbits]区间内均匀分布的随机数，如果想生成位数在某区间内均匀分布的随机数，请用`bool rand(size_t minbits, size_t maxbits, RNG& rng, number_t& n)`函数。

在默认情况下，默认随机数数生成器为异位移位生成器XORSP_t。

<h2 id="algorithms">算法</h2>

<h3>随机数生成器</h3>

利用随机数生成器生成序列{x<sub>0</sub>, x<sub>1</sub>, ..., x<sub>n</sub>, x<sub>n+1</sub>} (x<sub>i</sub>为字长型变量，i <= n + 1)

原始线性同余生成器LCG_t遵循x<sub>n+1</sub> = (A * x<sub>n</sub> + C) % M
其中A、C、M为常数，在32位环境中，A为0x9d832a31，C为0x11，M为2<sup>32</sup>，周期为M；在64位环境中，A为0x5851f42d4c957f2d，C为0x11，M为2<sup>64</sup>，周期为M。

由于M为2的幂，所以不必进行实际的取模运算，比较之下，原始线性同余随机数生成器的效率最高，但随机质量较差，一个明显的问题是生成序列往往是一个奇数一个偶数。

XLCG_t为改进的线性同余生成器，遵循t = (A * x<sub>n</sub> + C) % M，x<sub>n+1</sub> = t ^ (t >> UNITBITS)，t为临时变量。随机数质量有所提高。

XORSP_t 为异或移位生成器，生成随机数的效率和质量均较高，具体算法请参见[Further scramblings of Marsaglia’s xorshift generators](http://vigna.di.unimi.it/ftp/papers/xorshiftplus.pdf)。

CRNG_t利用操作系统的接口实现(类Unix上为/dev/urandom，Windows上为系统API CryptGenRandom)，效率较低，但生成随机数的质量非常高，是可以满足加密需求的随机数成生器，具体实现请参见源代码。

<h3>关于随机数种子</h3>

随机数种子可以作为随机数生成器构造函数的参数赋于生成器，CRNG_t是可以生成近乎于真随机数的生成器，故不需要指定种子。

随机数生成器默认构造函数通过`get_seed`函数来获取种子，该函数利用操作系统提供的高精度计时机制来增强随机性。