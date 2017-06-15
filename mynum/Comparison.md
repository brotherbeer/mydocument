<h1>Comparison</h1>

 * [Functions](#functions)
 * [Operators overloaded](#operatorsoverloaded)

<h2 id="functions">Functions</h2>

Compare _a_ and _b_, return 1 if _a_ > _b_, 0 if _a_ = _b_, -1 if _a_ < _b_
```C++
int cmp(const number_t& a, const number_t& b);
int cmp(const number_t& a, int b);
int cmp(const number_t& a, unsigned int b);
int cmp(const number_t& a, long b);
int cmp(const number_t& a, unsigned long b);
int cmp(const number_t& a, long long b);
int cmp(const number_t& a, unsigned long long b);
int cmp(int a, const number_t& b);
int cmp(unsigned int a, const number_t& b);
int cmp(long a, const number_t& b);
int cmp(unsigned long a, const number_t& b);
int cmp(long long a, const number_t& b);
int cmp(unsigned long long a, const number_t& b);
```

Compare the absolute values of _a_ and _b_
```C++
int cmp_abs(const number_t& a, const number_t& b);
```

Return true if _a_ != _b_
```C++
bool neq(const number_t& a, const number_t& b);
bool neq(const number_t& a, int b);
bool neq(const number_t& a, unsigned int b);
bool neq(const number_t& a, long b);
bool neq(const number_t& a, unsigned long b);
bool neq(const number_t& a, long long b);
bool neq(const number_t& a, unsigned long long b);
bool neq(int a, const number_t& b);
bool neq(unsigned int a, const number_t& b);
bool neq(long a, const number_t& b);
bool neq(unsigned long a, const number_t& b);
bool neq(long long a, const number_t& b);
bool neq(unsigned long long a, const number_t& b);
```

Return true if _a_ = _b_
```C++
bool eq(const number_t& a, const number_t& b);
bool eq(const number_t& a, int b);
bool eq(const number_t& a, unsigned int b);
bool eq(const number_t& a, long b);
bool eq(const number_t& a, unsigned long b);
bool eq(const number_t& a, long long b);
bool eq(const number_t& a, unsigned long long b);
bool eq(int a, const number_t& b);
bool eq(unsigned int a, const number_t& b);
bool eq(long a, const number_t& b);
bool eq(unsigned long a, const number_t& b);
bool eq(long long a, const number_t& b);
bool eq(unsigned long long a, const number_t& b);
```

Return true if _a_ < _b_
```C++
bool lt(const number_t& a, const number_t& b);
bool lt(const number_t& a, int b);
bool lt(const number_t& a, unsigned int b);
bool lt(const number_t& a, long b);
bool lt(const number_t& a, unsigned long b);
bool lt(const number_t& a, long long b);
bool lt(const number_t& a, unsigned long long b);
bool lt(int a, const number_t& b);
bool lt(unsigned int a, const number_t& b);
bool lt(long a, const number_t& b);
bool lt(unsigned long a, const number_t& b);
bool lt(long long a, const number_t& b);
bool lt(unsigned long long a, const number_t& b);
```

Return true if _a_ > _b_
```C++
bool gt(const number_t& a, const number_t& b);
bool gt(const number_t& a, int b);
bool gt(const number_t& a, unsigned int b);
bool gt(const number_t& a, long b);
bool gt(const number_t& a, unsigned long b);
bool gt(const number_t& a, long long b);
bool gt(const number_t& a, unsigned long long b);
bool gt(int a, const number_t& b);
bool gt(unsigned int a, const number_t& b);
bool gt(long a, const number_t& b);
bool gt(unsigned long a, const number_t& b);
bool gt(long long a, const number_t& b);
bool gt(unsigned long long a, const number_t& b);
```

Return true if _a_ <= _b_
```C++
bool elt(const number_t& a, const number_t& b);
bool elt(const number_t& a, int b);
bool elt(const number_t& a, unsigned int b);
bool elt(const number_t& a, long b);
bool elt(const number_t& a, unsigned long b);
bool elt(const number_t& a, long long b);
bool elt(const number_t& a, unsigned long long b);
bool elt(int a, const number_t& b);
bool elt(unsigned int a, const number_t& b);
bool elt(long a, const number_t& b);
bool elt(unsigned long a, const number_t& b);
bool elt(long long a, const number_t& b);
bool elt(unsigned long long a, const number_t& b);
```

Return true if _a_ >= _b_
```C++
bool egt(const number_t& a, const number_t& b);
bool egt(const number_t& a, int b);
bool egt(const number_t& a, unsigned int b);
bool egt(const number_t& a, long b);
bool egt(const number_t& a, unsigned long b);
bool egt(const number_t& a, long long b);
bool egt(const number_t& a, unsigned long long b);
bool egt(int a, const number_t& b);
bool egt(unsigned int a, const number_t& b);
bool egt(long a, const number_t& b);
bool egt(unsigned long a, const number_t& b);
bool egt(long long a, const number_t& b);
bool egt(unsigned long long a, const number_t& b);
```

<h2 id="operatorsoverloaded">Operators overloaded</h2>

Defined in [myoperators.h](https://github.com/brotherbeer/mynum/blob/master/myoperators.h)

```C++
bool operator == (const number_t& a, const number_t& b);
bool operator == (const number_t& a, bool b);
bool operator == (bool a, const number_t& b);
bool operator == (const number_t& a, char b);
bool operator == (char a, const number_t& b);
bool operator == (const number_t& a, short b);
bool operator == (short a, const number_t& b);
bool operator == (const number_t& a, int b);
bool operator == (int a, const number_t& b);
bool operator == (const number_t& a, long b);
bool operator == (long a, const number_t& b);
bool operator == (const number_t& a, long long b);
bool operator == (long long a, const number_t& b);
bool operator == (const number_t& a, unsigned char b);
bool operator == (unsigned char a, const number_t& b);
bool operator == (const number_t& a, unsigned short b);
bool operator == (unsigned short a, const number_t& b);
bool operator == (const number_t& a, unsigned int b);
bool operator == (unsigned int a, const number_t& b);
bool operator == (const number_t& a, unsigned long b);
bool operator == (unsigned long a, const number_t& b);
bool operator == (const number_t& a, unsigned long long b);
bool operator == (unsigned long long a, const number_t& b);

bool operator != (const number_t& a, const number_t& b);
bool operator != (const number_t& a, bool b);
bool operator != (bool a, const number_t& b);
bool operator != (const number_t& a, char b);
bool operator != (char a, const number_t& b);
bool operator != (const number_t& a, short b);
bool operator != (short a, const number_t& b);
bool operator != (const number_t& a, int b);
bool operator != (int a, const number_t& b);
bool operator != (const number_t& a, long b);
bool operator != (long a, const number_t& b);
bool operator != (const number_t& a, long long b);
bool operator != (long long a, const number_t& b);

bool operator != (const number_t& a, unsigned char b);
bool operator != (unsigned char a, const number_t& b);
bool operator != (const number_t& a, unsigned short b);
bool operator != (unsigned short a, const number_t& b);
bool operator != (const number_t& a, unsigned int b);
bool operator != (unsigned int a, const number_t& b);
bool operator != (const number_t& a, unsigned long b);
bool operator != (unsigned long a, const number_t& b);
bool operator != (const number_t& a, unsigned long long b);
bool operator != (unsigned long long a, const number_t& b);

bool operator > (const number_t& a, const number_t& b);
bool operator > (const number_t& a, bool b);
bool operator > (bool a, const number_t& b);
bool operator > (const number_t& a, char b);
bool operator > (char a, const number_t& b);
bool operator > (const number_t& a, short b);
bool operator > (short a, const number_t& b);
bool operator > (const number_t& a, int b);
bool operator > (int a, const number_t& b);
bool operator > (const number_t& a, long b);
bool operator > (long a, const number_t& b);
bool operator > (const number_t& a, long long b);
bool operator > (long long a, const number_t& b);
bool operator > (const number_t& a, unsigned char b);
bool operator > (unsigned char a, const number_t& b);
bool operator > (const number_t& a, unsigned short b);
bool operator > (unsigned short a, const number_t& b);
bool operator > (const number_t& a, unsigned int b);
bool operator > (unsigned int a, const number_t& b);
bool operator > (const number_t& a, unsigned long b);
bool operator > (unsigned long a, const number_t& b);
bool operator > (const number_t& a, unsigned long long b);
bool operator > (unsigned long long a, const number_t& b);

bool operator < (const number_t& a, const number_t& b);
bool operator < (const number_t& a, bool b);
bool operator < (bool a, const number_t& b);
bool operator < (const number_t& a, char b);
bool operator < (char a, const number_t& b);
bool operator < (const number_t& a, short b);
bool operator < (short a, const number_t& b);
bool operator < (const number_t& a, int b);
bool operator < (int a, const number_t& b);
bool operator < (const number_t& a, long b);
bool operator < (long a, const number_t& b);
bool operator < (const number_t& a, long long b);
bool operator < (long long a, const number_t& b);
bool operator < (const number_t& a, unsigned char b);
bool operator < (unsigned char a, const number_t& b);
bool operator < (const number_t& a, unsigned short b);
bool operator < (unsigned short a, const number_t& b);
bool operator < (const number_t& a, unsigned int b);
bool operator < (unsigned int a, const number_t& b);
bool operator < (const number_t& a, unsigned long b);
bool operator < (unsigned long a, const number_t& b);
bool operator < (const number_t& a, unsigned long long b);
bool operator < (unsigned long long a, const number_t& b);

bool operator >= (const number_t& a, const number_t& b);
bool operator >= (const number_t& a, bool b);
bool operator >= (bool a, const number_t& b);
bool operator >= (const number_t& a, char b);
bool operator >= (char a, const number_t& b);
bool operator >= (const number_t& a, short b);
bool operator >= (short a, const number_t& b);
bool operator >= (const number_t& a, int b);
bool operator >= (int a, const number_t& b);
bool operator >= (const number_t& a, long b);
bool operator >= (long a, const number_t& b);
bool operator >= (const number_t& a, long long b);
bool operator >= (long long a, const number_t& b);
bool operator >= (const number_t& a, unsigned char b);
bool operator >= (unsigned char a, const number_t& b);
bool operator >= (const number_t& a, unsigned short b);
bool operator >= (unsigned short a, const number_t& b);
bool operator >= (const number_t& a, unsigned int b);
bool operator >= (unsigned int a, const number_t& b);
bool operator >= (const number_t& a, unsigned long b);
bool operator >= (unsigned long a, const number_t& b);
bool operator >= (const number_t& a, unsigned long long b);
bool operator >= (unsigned long long a, const number_t& b);

bool operator <= (const number_t& a, const number_t& b);
bool operator <= (const number_t& a, bool b);
bool operator <= (bool a, const number_t& b);
bool operator <= (const number_t& a, char b);
bool operator <= (char a, const number_t& b);
bool operator <= (const number_t& a, short b);
bool operator <= (short a, const number_t& b);
bool operator <= (const number_t& a, int b);
bool operator <= (int a, const number_t& b);
bool operator <= (const number_t& a, long b);
bool operator <= (long a, const number_t& b);
bool operator <= (const number_t& a, long long b);
bool operator <= (long long a, const number_t& b);
bool operator <= (const number_t& a, unsigned char b);
bool operator <= (unsigned char a, const number_t& b);
bool operator <= (const number_t& a, unsigned short b);
bool operator <= (unsigned short a, const number_t& b);
bool operator <= (const number_t& a, unsigned int b);
bool operator <= (unsigned int a, const number_t& b);
bool operator <= (const number_t& a, unsigned long b);
bool operator <= (unsigned long a, const number_t& b);
bool operator <= (const number_t& a, unsigned long long b);
bool operator <= (unsigned long long a, const number_t& b);
```
