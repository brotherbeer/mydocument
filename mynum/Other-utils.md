<h1>Other utils</h1>

 * [Global memory interface](#title1)
 * [Object memory management](#title2)
 * [Absolute value](#title3)
 * [Negative value](#title4)
 * [Number property](#title5)
 * [Sign](#title6)
 * [Units iteration](#title7)
 * [Swap](#title8)
 * [Standard IO stream](#title9)

<h2 id="title1">Global memory interface</h2>

```C++
struct mem
{
    static void* allocate(size_t s, size_t u)
    {
        return malloc(s * u);
    }

    static void deallocate(void* p)
    {
        free(p);
    }

private:
    mem() {}
    mem(const mem&) {}
   ~mem() {}
};
```

All memory is allocated via `allocate` interface and released via `deallocate` interface,  
if you need change the memory allocation method, you can alter `struct mem`

<h2 id="title2">Object memory management</h2>

Return how many units can be holden by the current memory space
```C++
size_t number_t::unit_capacity() const;
```

Set the capacity of _*this_ to the same as _another_, and copy the data from _another_,  
if you don't need let _*this_ have the same capacity, use `assign` function instead
```C++
void number_t::copy(const number_t& another);
```

Release all memory of _*this_, and set the value of *this to 0
```C++
void number_t::release();
```

Increase the capacity of the units to _newcap_,  
if _newcap_ is greater than the current `unit_capacity()`, new storage is allocated,  
otherwise the method does nothing
```C++
void number_t::reserve(size_t newcap);
```

Increase the capacity of the bits to _newbitcap_,  
if _newbitcap_ is greater than the current `unit_capacity() * UNITBITS`, new storage is allocated,  
otherwise the method does nothing
```C++
void number_t::bits_reserve(size_t newbitcap);
```

Set the value of *this to 0, the memory is not changed
```C++
void number_t::clear();
```

Clear and reserve
```C++
void number_t::clear_and_reserve(size_t unitsize);
```

Release *this, and set all the data of _another_ to _*this_,  
in some cases, it can save the memory allocation and copy time
```C++
void number_t::steal(number_t& another);
```

<h2 id="title3">Absolute value</h2>

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

<h2 id="title4">Negative value</h2>

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

Member functions
```C++
number_t number_t::neg() const;
number_t& number_t::set_neg();
```

<h2 id="title5">Number property</h2>

Return whether _*this_ is even or not
```C++
bool number_t::is_even() const;
```

Return whether _*this_ is odd or not
```C++
bool number_t::is_odd() const;
```

Return whether _*this_ is zero or not
```C++
bool number_t::is_zero() const;
```

Return whether _*this_ is 1 or not
```C++
bool number_t::is_one() const
```

Return whether _*this_ is -1 or not
```C++
bool number_t::is_neg_one() const;
```

Return whether _*this_ is 2 or not
```C++
bool is_two() const;
```

Return whether _*this_ is the power of 2 or not
```C++
bool number_t::is_po2() const;
```

Return whether _*this_ is positive or not
```C++
bool number_t::is_pos() const;
```

Return whether _*this_ is negative or not
```C++
bool number_t::is_neg() const;
```

Return whether _*this_ is not _another_
```C++
bool number_t::is_not(const number_t& another) const;
```

Return whether *this != 0 or not
```C++
operator number_t::bool () const;
```

Return whether *this = 0 or not
```C++
bool number_t::operator ! () const;
```

<h2 id="title6">Sign</h2>

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

<h2 id="title7">Units iteration</h2>

Return the count of the valid units
```C++
size_t number_t::unit_count() const;
```

Return the address of the first unit
```C++
unit_t* number_t::unit();
const unit_t* number_t::unit() const;
```

```C++
unit_t* number_t::unit_end();
const unit_t* number_t::unit_end() const;
```

Return the address of the last unit
```C++
unit_t* number_t::unit_last();
const unit_t* number_t::unit_last() const;
```

```C++
unit_t* number_t::unit_rend();
const unit_t* number_t::unit_rend() const;
```

<h2 id="title8">Swap</h2>

Swap the value of _a_ and _b_
```C++
void swap(number_t& a, number_t& b);
```

<h2 id="title9">Standard IO stream</h2>

Defined in myoperators.h
```C++
std::istream& operator >> (std::istream& is, number_t& a);
std::ostream& operator << (std::ostream& os, const number_t& a);
```
