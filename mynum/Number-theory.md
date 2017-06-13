<h1>Number theoretic functions</h1>

 * [Functions](#functions)
 * [Attentions](#attentions)
 * [Algorithms](#algorithms)

<h2 id="functions">Functions</h2>

Return the Jacobi symbol of _a_ and _b_
```C++
int jacobi(const number_t& a, const number_t& b);
```

Set _res_ to the greatest common divisor of _a_ and _b_ (if either _a_ or _b_ is negative, use the absolute value)  
If _a_ and _b_ are all zero, the function returns 0, otherwise returns 1
```C++
int gcd(const number_t& a, const number_t& b, number_t& res);
```

Set _g_ to the greatest common divisor of _a_ and _b_ (if either _a_ or _b_ is negative, use the absolute value)  
Set _x_ and _y_ to the coefficients satisfying _a_ * _x_ + _b_ * _y_ = _g_  
If _a_ and _b_ are all zero, the function returns 0, otherwise returns 1
```C++
int gcd_ext(const number_t& a, const number_t& b, number_t& x, number_t& y, number_t& g);
```

Set _res_ to the least common multiple of _a_ and _b_ (if either _a_ or _b_ is negative, use the absolute value)
```C++
void lcm(const number_t& a, const number_t& b, number_t& res);
```

Set _res_ to _a<sup>b</sup>_ % _c_
If _c_ is zero, returns 0, otherwise returns 1
```C++
int pom(const number_t& a, const number_t& b, const number_t& c, number_t& res);
```

Set _res_ to the modular multiplicative inverse of _a_, i.e., _a_ * _res_ % _m_ = 1  
If the inverse dose not exist, returns 0, otherwise returns 1
```C++
int inv(const number_t& a, const number_t& m, number_t& res);
```

<h2 id="attentions">Attentions</h2>

<h2 id="algorithms">Algorithms</h2>