String conversion
-------------

##Member Functions

Conver the value of *this to _str_
```C++
string_t& number_t::to_bin_string(string_t& str) const;
string_t& number_t::to_oct_string(string_t& str) const;
string_t& number_t::to_dec_string(string_t& str) const;
string_t& number_t::to_hex_string(string_t& str) const;
```

Conver the value of *this to _str_, which is in specified base _base_
```C++
string_t& number_t::to_string(string_t& str, int base = 10) const;
```

Return the string_t object
```C++
string_t number_t::to_bin_string() const;
string_t number_t::to_oct_string() const;
string_t number_t::to_dec_string() const;
string_t number_t::to_hex_string() const;
string_t number_t::to_string(int base = 10) const;
```

Return the string_t object, which is in base _base_
```C++
string_t number_t::operator () (int base) const;
```
