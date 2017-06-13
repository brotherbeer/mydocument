Random number
-------------

 * [Random number generator](#rng)
 * [Functions](#functions)
 * [Algorithms](#Algorithms)

<h2 id="rng">Random number generator</h2>

<h3>The virtual base class</h3>

```C++
struct RNG
{
    virtual word_t gen() = 0;

    virtual bool valid() const = 0;

    virtual bool gen_bytes(void* buf, size_t n);

    word_t operator () () { return gen(); }

    virtual ~RNG() {}

    bool chance(size_t x) { return x && (gen() % x == 1); }
};
```
Interfaces:

Generate a random word
```C++
word_t gen();
```
Generate _n_ bytes random data in the memory _buf_ points to,  
if the function succeeds, the return value is true, otherwise, the return value is false
```C++
bool gen_bytes(void* buf, size_t n);
```
If the generator is valid, returns true, otherwise returns false
```
bool valid() const;
```

<h3>Linear congruence generator</h3>
```
struct LCG_t: public RNG
```

<h3>Improved linear congruence generator</h3>
```
struct XLCG_t: public RNG
```

<h3>XOR-shift generator</h3>
```C++
struct XORSP_t: public RNG
```

<h3>Cryptography generator</h3>
```C++
struct CRNG_t: public RNG
```

<h2 id="functions">Functions</h2>

Return the reference of the default generator
```C++
RNG& default_RNG();
```

Set current default generator
```C++
void set_default_RNG(RNG& rng);
```

Get a seed
```C++
word_t get_seed();
```

Generate an unit using default generator
```C++
unit_t rand_unit();
```

Generate a word using default generator
```C++
word_t rand_word();
```

Returns true with the probability of 1 / _n_, using default generator
```C++
bool chance(size_t n);
```

Set _n_ to a random number, the bits count of _n_ is no more than _maxbits_, using default generator
```C++
bool rand(size_t maxbits, number_t& n);
```

Set _n_ to a random number, the bits count of _n_ is no more than _maxbits_, using default generator,  
If _holdmsb_ is ture, then _n_ must have _maxbits_ bits,  
if the function succeeds, the return value is true, otherwise, the return value is false
```C++
bool rand(size_t maxbits, bool holdmsb, number_t& n);
```

Set _n_ to a random number, the bits count of _n_ is uniform in [minbits, maxbits], using default generator,  
the return value indicates whether the function succeeded
```C++
bool rand(size_t minbits, size_t maxbits, number_t& n);
```

Set _s_ to a random string whose chars are randomly chosen by the default generator in _chars_,  
the length of _s_ is _length_,  
the return value indicates whether the function succeeded
```C++
bool rand(size_t length, const string_t& chars, string_t& s);
```

Set _n_ to a random number, the bits count of _n_ is no more than _maxbits_, using the specified generator _rng_,  
the return value indicates whether the function succeeded
```C++
bool rand(size_t maxbits, RNG& rng, number_t& n);
```

Set _n_ to a random number, the bits count of _n_ is no more than _maxbits_, using the specified generator _rng_,  
If _holdmsb_ is ture, then _n_ must have _maxbits_ bits,    
the return value indicates whether the function succeeded
```C++
bool rand(size_t maxbits, RNG& rng, bool holdmsb, number_t& n);
```

Set _n_ to a random number, the bits count of _n_ is uniform in [minbits, maxbits], using the specified generator _rng_,  
the return value indicates whether the function succeeded
```C++
bool rand(size_t minbits, size_t maxbits, RNG& rng, number_t& n);
```

Set _s_ to a random string whose chars are randomly chosen by the specified generator _rng_ in _chars_,  
the length of _s_ is _length_,  
the return value indicates whether the function succeeded
```C++
bool rand(size_t length, const string_t& chars, RNG& rng, string_t& s);
```
