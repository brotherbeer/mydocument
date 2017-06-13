<h1>数论相关函数</h1>

 * [函数](#functions)
 * [注意事项](#attentions)
 * [算法](#algorithms)

<h2 id="functions">Functions</h2>

返回a和b的Jacobi符号
```C++
int jacobi(const number_t& a, const number_t& b);
```

求a和b的最大公约数res  
如果a和b均为0，返回0，否则返回1  
如果a和b中有负数，则res为a和b的绝对值的最大公约数  
```C++
int gcd(const number_t& a, const number_t& b, number_t& res);
```

扩展最大公约数  
g = a * x + b * y，g为a和b的最大公约数
如果a和b中有负数，则res为a和b的绝对值的最大公约数 
```C++
int gcd_ext(const number_t& a, const number_t& b, number_t& x, number_t& y, number_t& g);
```

求a和b的最小公倍数res
```C++
void lcm(const number_t& a, const number_t& b, number_t& res);
```

幂取模，res = a<sup>b</sup> % c
如果c为零，返回0，否则返回1
```C++
int pom(const number_t& a, const number_t& b, const number_t& c, number_t& res);
```

求a模m的乘法逆元res，即a * res % m = 1
如果乘法逆元不存在，返回0，否则返回1
```C++
int inv(const number_t& a, const number_t& m, number_t& res);
```

<h2 id="attentions">注意事项</h2>

<h2 id="algorithms">算法</h2>
