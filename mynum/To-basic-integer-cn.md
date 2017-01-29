����������תΪ�������ͱ���
-------------

 * [��س�Ա����](#��س�Ա����)
 * [ע������](#ע������)
 * [ʾ��](#ʾ��)

##��س�Ա����

�ж϶����ֵ�Ƿ���ָ���Ļ������ͷ�Χ��
```C++
bool number_t::in_range_char() const;
bool number_t::in_range_short() const;
bool number_t::in_range_int() const;
bool number_t::in_range_long() const;
bool number_t::in_range_longlong() const;
bool number_t::in_range_uchar() const;
bool number_t::in_range_ushort() const;
bool number_t::in_range_uint() const;
bool number_t::in_range_ulong() const;
bool number_t::in_range_ulonglong() const;
bool number_t::in_range_word() const;
bool number_t::in_range_sword() const;
```

�������ֵתΪ��Ӧ�������ͱ���
```C++
char number_t::to_char() const;
short number_t::to_short() const;
int number_t::to_int() const;
long number_t::to_long() const;
long long number_t::to_longlong() const;
unsigned char number_t::to_uchar() const;
unsigned short number_t::to_ushort() const;
unsigned int number_t::to_uint() const;
unsigned long number_t::to_ulong() const;
unsigned long long number_t::to_ulonglong() const;
```

����ת�����������
```C++
operator bool () const;
bool operator ! () const;
operator char () const;
operator short () const;
operator int () const;
operator long () const;
operator long long () const;
operator unsigned char () const;
operator unsigned short () const;
operator unsigned int () const;
operator unsigned long () const;
operator unsigned long long () const;
```

##ע������
������������תΪ�������ͱ���֮ǰӦ���ж���ֵ�Ƿ�����Ӧ�������͵ķ�Χ�ڣ�������ڸ÷�Χ�ڣ�ת�����ֵΪ����ȷ��ֵ��  
���⣬ֵΪ��ʱ����������Ӧ�޷������͵ķ�Χ�ڣ���-1����unsigned int��Χ�ڣ�-2����unsigned long��Χ�ڡ�  
�����ͷ�Χ��
|char| [-128, 127]|
|short| [-32768, 32767]|
|int| [-2147483648, 2147483647]|
|long| �����������|
|long long| [-9223372036854775808, 9223372036854775807] |
|unsigned char| [0, 255]|
|unsigned short|[0, 65535]|
|unsigned int| [0, 4294967295] |
|unsigned long| �����������|
|unsigned long long| [0, 18446744073709551615] |
���У�long/unsigned long�͵ķ�Χ�������������gcc���뻷������long long/unsigned long long��ͬ��MSVC��������int/unsigned int��ͬ��

##ʾ��
```C++
number_t a(0xffffffff), b(-1);
if (a.in_range_int()) cout << a.to_int() << endl;
if (a.in_range_uint()) cout << a.to_uint() << endl;
if (b.in_range_int()) cout << a.to_int() << endl;
if (b.in_range_uint()) cout << a.to_uint() << endl;
```
�����
```
4294967295
-1
```