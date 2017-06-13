<h1>Exponentiation</h1>

 * [Functions](#functions)
 * [Member functions](#memberfunctions)

<h2 id="functions">Functions</h2>

Set _res_ to _a<sup>2</sup>_, using basic algorithm  
```C++
void sqr(const number_t& a, number_t& res);
```

Set _res_ to _a<sup>2</sup>_, using Karatsuba algorithm  
```C++
void ksqr(const number_t& a, number_t& res);
```

Set _res_ to _a<sup>2</sup>_, using NTT(Number Theoretic Transform) algorithm
```C++
void fsqr(const number_t& a, number_t& res);
```

Set _res_ to _a<sup>b</sup>_
```C++
void pow(const number_t& a, size_t b, number_t& res);
```

<h2 id="memberfunctions">Member functions</h2>

```C++
number_t& number_t::sqr();
number_t& number_t::ksqr();
number_t& number_t::pow(size_t);
```
