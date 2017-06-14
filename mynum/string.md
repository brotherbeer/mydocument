<h1>string_t class</h1>

 * [Constructors](#constructors)
 * [Destructor](#destructor)
 * [Member functions](#memberfunctions)
 * [Member operators](#memberoperators)
 * [Static constants](#staticconstants)
 * [Global functions](#globalfunctions)
 * [Global operators](#globaloperators)
 
<h2 id="constructors">Constructors</h2>

The default constructor
```C++
string_t();
```

Construct a string from a single character _c_
```C++
string_t(char c);
```

Construct a string from a null-terminated character array(_p_)
```C++
string_t(const char* p);
```

Construct a string from a character array(_p_) and a length(_l_).
```C++
string_t(const char* p, size_t l);
```

Copy constructor
```C++
string_t(const string_t&);
```

Construct a string from a range of another string_t object,  
the range is [_bpos_, _epos_) of _another_, _bpos_ and _epos_ are position indices

```C++
string_t(const string_t& another, size_t bpos, size_t epos);
```

Construct a string which can hold _n_ characters,  
`T` must be a type which can indicate size
```C++
template<class T> explicit string_t(T n);
```

Construct a string with _n_ copies of _c_,  
`T` must be a type which can indicate size
```C++
template<class T> explicit string_t(char c, T n);
```

<h2 id="destructor">Destructor</h2>

```C++
~string_t();
```

<h2 id="memberfunctions">Member functions</h2>

Return a pointer to a C string(null-terminated array of characters), which represents the contents of _*this_
```C++
const char* c_str() const;
```

Return the length of the string
```C++
size_t length() const;
```

Return the count of characters can be holden without memory reallocation
```C++
size_t capacity() const;
```

Return whether the size of _*this_ is 0 or not
```C++
bool empty() const;
```

Erase all the characters
```C++
void clear();
```

Release the memory
```C++
void release();
```

Set the count of characters can be holden without memory reallocation
```C++
void reserve(size_t n);
```

Append character(s) or string in the back of _*this_'s contents
```C++
string_t& append(char);
string_t& append(char, size_t);
string_t& append(const char*, size_t);
string_t& append(const string_t&, size_t bpos, size_t epos);
string_t& append(const char* p);
string_t& append(const string_t& another);
```

Insert character(s) or string in front of _*this_'s contents
```C++
string_t& prepend(char c);
string_t& prepend(char c, size_t n);
string_t& prepend(const char* p);
string_t& prepend(const char* p, size_t l);
string_t& prepend(const string_t& another);
string_t& prepend(const string_t& another, size_t bpos, size_t epos);
```

Insert character(s) or string in the specified position of _*this_'s contents
```C++
string_t& insert(size_t pos, char, size_t);
string_t& insert(size_t pos, const char*, size_t);
string_t& insert(size_t pos, const string_t&, size_t bpos, size_t epos);
string_t& insert(size_t pos, const char* p);
string_t& insert(size_t pos, const string_t& another);
```

Remove the character(s) at specified position _pos_ or range [_bpos_, _epos_)
```C++
string_t& remove(size_t pos);
string_t& remove(size_t bpos, size_t epos);
string_t& remove_to_begin(size_t pos);
string_t& remove_to_end(size_t pos);
```

Replace the characters in specified range [_bpos_, _epos_] with characters or string
```C++
string_t& replace(size_t bpos, size_t epos, char c, size_t l);
string_t& replace(size_t bpos, size_t epos, const char* p);
string_t& replace(size_t bpos, size_t epos, const char* p, size_t l);
string_t& replace(size_t bpos, size_t epos, const string_t& s);
string_t& replace(size_t bpos, size_t epos, const string_t& s, size_t sbpos, size_t sepos);
```

Set the characters to upper case or lower case
```C++
string_t& to_upper();
string_t& to_lower();
string_t& to_upper(string_t& res) const;
string_t& to_lower(string_t& res) const;
```

Assignment functions
```C++
string_t& assign(char);
string_t& assign(char, size_t);
string_t& assign(const char*, size_t);
string_t& assign(const string_t&, size_t bpos, size_t epos);
string_t& assign(const char* p);
string_t& assign(const string_t& another);
```

Remove blank or specified characters at the left or right of the contents
```C++
string_t& strip_left(const char*);
string_t& strip_right(const char*);
string_t& strip(const char*);
string_t& strip_left(const string_t& another);
string_t& strip_right(const string_t& another);
string_t& strip_left();
string_t& strip_right();
string_t& strip(const string_t& another);
string_t& strip();
```

Return the position of the specified character(s) or string,  
if there is not such a string, return string_t::npos
```C++
size_t find(size_t pos, char c) const;
size_t find(size_t pos, const char* p) const;
size_t find(size_t pos, const string_t& str) const;
size_t find(char c) const;
size_t find(const char* p) const;
size_t find(const string_t& str) const;
```

Return whether the contents starts with the specified character(s) or string
```C++
bool starts_with(size_t pos, const char*, size_t, bool ignorecase = false) const;
bool starts_with(size_t pos, const char* p, bool ignorecase = false) const;
bool starts_with(size_t pos, const string_t& another, bool ignorecase = false) const;
bool starts_with(const char* p, bool ignorecase = false) const;
bool starts_with(const char* p, size_t l, bool ignorecase = false) const;
bool starts_with(const string_t& another, bool ignorecase = false) const;
```

Return whether the contents ends with the specified character(s) or string
```C++
bool ends_with(size_t pos, const char*, size_t, bool ignorecase = false) const;
bool ends_with(size_t pos, const char* p, bool ignorecase = false) const;
bool ends_with(size_t pos, const string_t& another, bool ignorecase = false) const;
bool ends_with(const char* p, bool ignorecase = false) const;
bool ends_with(const char* p, size_t l, bool ignorecase = false) const;
bool ends_with(const string_t& another, bool ignorecase = false) const;
```

Return whether the contents have a sub-string or a character
```C++
bool contains(char c) const;
bool contains(const char* p) const;
```

Reverse the order of the characters
```C++
string_t& reverse();
string_t& reverse(size_t bpos, size_t epos);
```

Return the next position of the last character, the position indicates the end of the string
```C++
size_t end_pos() const;
```

Return the position of the last character
```C++
size_t last_pos() const;
```

```C++
size_t pos_not_chars(size_t pos, const char* p) const;
```

```C++
size_t rpos_not_chars(size_t pos, const char*) const;
```

The assignment operator
```C++
string_t& operator = (char c);
string_t& operator = (const char* p);
string_t& operator = (const string_t& another);
```

Equivalent to `append` functions
```C++
string_t& operator += (char c);
string_t& operator += (const char* p);
string_t& operator += (const string_t& another);
```

<h2 id="memberoperators">Member operators</h2>

Returns the _n_'th character
```C++
char& operator [] (size_t n);
char operator [] (size_t n) const;
```

<h2 id="staticconstants">Static constants</h2>

```C++
static const size_t npos = -1;
```

<h2 id="globalfunctions">Global functions</h2>

Three-way lexicographical comparison of _a_ and _b_
```C++
int cmp(const string_t& a, const string_t& b);
int cmp(const string_t& a, const char* b);
int cmp(const char* a, const string_t& b);
```

<h2 id="globaloperators">Global operators</h2>

Lexicographical comparison of _a_ and _b_
```C++
bool operator == (const string_t& a, const string_t& b);
bool operator != (const string_t& a, const string_t& b);
bool operator >  (const string_t& a, const string_t& b);
bool operator <  (const string_t& a, const string_t& b);
bool operator >= (const string_t& a, const string_t& b);
bool operator <= (const string_t& a, const string_t& b);
bool operator == (const string_t& a, const char* b);
bool operator != (const string_t& a, const char* b);
bool operator >  (const string_t& a, const char* b);
bool operator <  (const string_t& a, const char* b);
bool operator >= (const string_t& a, const char* b);
bool operator <= (const string_t& a, const char* b);
bool operator == (const char* a, const string_t& b);
bool operator != (const char* a, const string_t& b);
bool operator >  (const char* a, const string_t& b);
bool operator <  (const char* a, const string_t& b);
bool operator >= (const char* a, const string_t& b);
bool operator <= (const char* a, const string_t& b);
```

Concatenate _a_ and _b_
```C++
string_t operator + (char a, const string_t& b);
string_t operator + (const char* a, const string_t& b);
string_t operator + (const string_t& a, char b);
string_t operator + (const string_t& a, const char* b);
string_t operator + (const string_t& a, const string_t& b);
```

If _b_ is a sub-string of _a_, remove all _b_ from _a_
```C++
string_t operator - (const string_t& a, char b);
string_t operator - (const string_t& a, const string_t& b);
string_t& operator -= (string_t& a, char b);
string_t& operator -= (string_t& a, const string_t& b);
```

Create a new string_t object which repeats _a_ for _n_ times
```C++
string_t operator * (const string_t& a, size_t n);
string_t operator * (size_t n, const string_t& a);
string_t operator * (const string_t& a, int n);
string_t operator * (int n, const string_t& a);
string_t& operator *= (string_t& a, size_t n);
string_t& operator *= (string_t& a, int n);
```

Split _a_ into a std list by character or string _b_
```C++
std::list<string_t> operator / (const string_t& a, char b);
std::list<string_t> operator / (const string_t& a, const char* b);
std::list<string_t> operator / (const string_t& a, const string_t& b);
std::list<string_t> operator / (const char* a, const string_t& b);
```
