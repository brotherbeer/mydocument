<h1>乘方</h1>

 * [函数](#functions)
 * [成员函数](#memberfunctions)

<h2 id="functions">函数</h2>

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

<h2 id="memberfunctions">成员函数</h2>

```C++
number_t& number_t::sqr();
number_t& number_t::ksqr();
number_t& number_t::pow(size_t);
```
