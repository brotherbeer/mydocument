其它
-------------

##绝对值
Set the absolute value of _a_ to _res_
```C++
void abs(const number_t& a, number_t& res);
```

Return the absolute value of _a_ 
```C++
number_t abs(const number_t& a);
```

Set _a_ to its absolute value
```C++
number_t& set_abs(number_t& a);
```

Member functions
```C++
number_t number_t::abs() const;
number_t& number_t::set_abs();
```

##负值
Set the negative value of _a_ to _res_
```C++
void neg(const number_t& a, number_t& res);
```

Return the negative value of _a_ 
```C++
number_t neg(const number_t& a);
```

Set _a_ to its negative value
```C++
number_t& set_neg(number_t& a);
```

成员函数
```C++
number_t number_t::neg() const;
number_t& number_t::set_neg();
```

##整数属性
Return true if *this is even
```C++
bool number_t::is_even() const;
```

Return true if *this is odd
```C++
bool number_t::is_odd() const;
```

Return true if *this is zero
```C++
bool number_t::is_zero() const;
```

Return true if *this is 1
```C++
bool number_t::is_one() const
```

Return true if *this is -1
```C++
bool number_t::is_neg_one() const;
```

Return true if *this is the power of 2
```C++
bool number_t::is_po2() const;
```

Return true if *this is positive
```C++
bool number_t::is_pos() const;
```

Return true if *this is negative
```C++
bool number_t::is_neg() const;
```

Return true if *this is not _another_
```C++
bool number_t::is_not(const number_t& another) const;
```

Return true if *this != 0
```C++
operator number_t::bool () const;
```

Return true if *this = 0
```C++
bool number_t::operator ! () const;
```

##符号
Unary operator that leaves *this unchanged, and return *this
```C++
number_t number_t::operator + () const;
```

The minus sign overloaded
```C++
number_t number_t::operator - () const;
```

If _sign_ = -1, set _a_ to be negative, else if _sign_ = 1, set _a_ to be positive
```C++
number_t& set_sign(number_t& a, int sign);
```

If _a_ >= 0 return 1 else if _a_ < 0 return -1
```C++
int sign(const number_t& a);
```

If _a_ and _b_ have the same sign, return 1, else return 0
```C++
int sign(const number_t& a, const number_t& b);
```

Return true if _a_ and _b_ have the same sign
```C++
bool same_sign(const number_t& a, const number_t& b);
```

##交换
```C++
void swap(number_t& a, number_t& b);
```
