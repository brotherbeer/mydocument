<h1>Primality test</h1>

 * [Functions](#functions)
 * [Algorithms](#algorithms)
 
<h2 id="functions">Functions</h2>

A roughly primality test for _n_, if true is returned, _n_ may be a prime, if false is returned, _n_ must be a composite number
```C++
bool prime_test_roughly(const number_t& n);
```

Set _res_ to be the next number of _n_ who can pass the roughly primality test
```C++
void prime_next_roughly(const number_t& n, number_t& res);
```

Set _res_ to be the previous number of _n_ who can pass the roughly primality test
```C++
void prime_prev_roughly(const number_t& n, number_t& res);
```

Do Miller-Rabin test for _n_, _times_ is the test times
```C++
bool MR_prime_test(const number_t& n, size_t times);
```

<h2 id="algorithms">Algorithms</h2>
