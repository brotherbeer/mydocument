素数测试
-------------

 * [全局函数](#全局函数)
 * [算法](#算法)
 
##全局函数

对大整数n进行粗略的测试，通过返回true，否则返回false  
如果返回true，n可能为素数，如果返回false，n一定为合数
```C++
bool prime_test_roughly(const number_t& n);
```

将大整数res设为n的下一个通过粗略测试的疑似素数
```C++
void prime_next_roughly(const number_t& n, number_t& res);
```

将大整数res设为n的前一个通过粗略测试的疑似素数
```C++
void prime_prev_roughly(const number_t& n, number_t& res);
```

对大整数n进行Miller-Rabin测试，times为测试次数
```C++
bool MR_prime_test(const number_t& n, size_t times);
```

##算法

粗略测试先用一组小素数对待测整数进行试除，如果可以除得开，则返回false，如果除不开，再用2、31、181等小整数作为底进行Miller-Rabin测试。