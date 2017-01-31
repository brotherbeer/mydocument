乘方
-------------

##Functions

Set _res_ to _a<sup>b</sup>_
```C++
void pow(const number_t& a, size_t b, number_t& res);
```

Set _res_ to _a<sup>b</sup>_ % _c_
```C++
int pom(const number_t& a, const number_t& b, const number_t& c, number_t& res);
```

Return the result
```C++
number_t pow(const number_t& a, size_t b);
number_t pom(const number_t& a, const number_t& b, const number_t& c);
```

##Member Functions

```C++
number_t& number_t::pow(size_t);
number_t& number_t::pom(const number_t&, const number_t&);
```
