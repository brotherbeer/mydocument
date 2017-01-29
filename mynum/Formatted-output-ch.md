����������תΪ��ʽ���ַ���
-------------

������(number_t)������԰�ָ���ĸ�ʽת��Ϊ�ַ���(string_t)���󡣿���format_t��Ķ���ָ����ʽ�����磺
```C++
string_t s;
number_t a("1234567890");
format_t fmt;
cout << fmt.dump(a, 16, s) << endl;  // ��aתΪ��ʾ16���������ַ���

fmt.set(UPPER_CASE | SHOW_LEADING);
cout << fmt.dump(a, 16, s) << endl;
```
�����
```
499602d2
0x499602D2
```
���У�UPPER_CASE��SHOW_LEADING������ָ����ʽ����Ϣ�ı�־λ���ֱ��ʾ�ô�д��ĸ��¼��λ��ֵ����ʾǰ���ַ���Ĭ���������Сд��ĸ������ʾǰ���ַ���dump����������������תΪָ�����Ƶ��ַ�����ʾ����Ϊ16���ơ�
����format_t�����ϸ��Ϣ���£�

 * [��־λ](#��־λ)
 * [format_t���캯��](#���캯��)
 * [format_t��Ա����](#��Ա����)
 * [ǰ���ַ�](#ǰ���ַ�)
 * [�����뻻��](#�����뻻��)
 * [ע������](#ע������)

##��־λ
��ʽ����־λΪformat_flags_t�͵ĳ���������־λ����'\|'������ϣ�����־λ�������£�
|��־λ|����|
|------|----|
|UPPER_CASE| �ô�д��ĸ����ַ������޴˱�־λ����Сд��ĸ|
|UPPER_LEADING| �ô�д��ĸ���ǰ���ַ�����Ĭ�������ʮ�����ƶ�Ӧ0X�������ƶ�Ӧ0B��|
|SHOW_POS| ���ָ���Ĵ���������Ϊ�����������+��|
|SHOW_LEADING| ���ǰ���ַ�����Ĭ�������ʮ�����ƶ�Ӧ0x�������ƶ�Ӧ0b�ȣ�ǰ���ַ������趨|
|SIGN_RIGHT_LEADING| ������ǰ���ַ��Ҳ࣬��0x-ab���޴˱�־λ�������ǰ���ַ���࣬��-0xab|
|GROUP_COMPLETE| ������һ�������е��ַ�����С��group������fillerָ�����ַ����|
|GROUP_FROM_MSB| �Ӹ�λ��ʼ��ָ���ַ������ַ�����|
|ZERO_NO_LEADING| ���ָ���Ĵ�����Ϊ0�������ǰ���ַ����޴˱�־λ�����|
|ZERO_POS| �������SHOW_POS��־λ��ָ���Ĵ���������Ϊ0�������+��|
|ZERO_NEG| ���ָ���Ĵ���������Ϊ0�����-��|
|EMPTY_AS_ERROR| ���ڴ˱�־λʱ�����ַ�����Ϊ�����ַ�����������Ϊ0|
|MULTISIGN_AS_ERROR| ���ฺ�Ż��������Ϊ����|

�磺
```C++
format_t fmt;
fmt.set(UPPER_CASE | SHOW_POS | SHOW_LEADING);
fmt.clear(SHOW_POS); // ���SHOW_POS��־λ
assert(fmt.get() == UPPER_CASE | SHOW_LEADING)
fmt.set(NO_FLAGS);   // ������б�־λ
assert(fmt.get() == 0);
```

##���캯��
���ڹ���ʱָ����־λ��Ĭ��ֵΪ0�������趨�κα�־λ
```C++
format_t(format_flags_t ff = 0):
```
##��Ա����
�趨ĳ��Щ����־λ
```C++
void set(format_flags_t ff);
```
���ĳ��Щ����־λ
```C++
void clear(format_flags_t ff);
```
������б�־λ
```C++
void clear_all() { _flags = 0; }
```
�ж��Ƿ��趨��ĳ��Щ����־λ
```C++
bool has(format_flags_t ff) const;
```
�������б�־λ
```C++
format_flags_t flags() const;
```
���ط����С�����[�����뻻��](#�����뻻��)
```C++
size_t group_size() const;
```
�������ڷ�����������[�����뻻��](#�����뻻��)
```C++
size_t line_group_count() const;
```
������ָ���
```C++
const string_t& group_separator() const;
```
�����зָ���
```C++
const string_t& line_separator() const;
```
������������
```C++
char group_filler() const;
```
������ָ���
```C++
void set_group_separator(const char* p);
```
����������
```C++
void set_group_filler(char c);
```
�������ַ�����
```C++
void set_group_size(size_t size);
```
�������������
```C++
void set_line_group_count(size_t cnt);
```
�����зָ�����Ĭ��Ϊ'\n'
```C++
void set_line_separator(const char* p);
```
������������aתΪ����Ϊbase���ַ���str
```C++
string_t& dump(const number_t& a, int _base, string_t& str) const;
```

##�����뻻��
�ɽ�����ַ�����ָ�����ַ��������з��飬�������ָ����ָ������ַ�������set_group_size�����趨����ָ���ַ�����Ϊ0ʱ�����飬Ĭ�ϲ����顣�磺
```C++
string_t s;
number_t a("3141592653589");
format_t fmt;
fmt.set_group_size(3);
fmt.set_group_separator(", ");
assert(fmt.dump(a, 10, s) == "3, 141, 592, 653, 589");
```
������趨GROUP_FROM_MSB�����ӵ�λ��ʼÿ��ָ�����ַ��������ָ���������趨GROUP_FROM_MSB����Ӹ�λ��ʼ����һ�����鲻��ָ�����ַ�����ʱ������ͨ������GROUP_COMPLETE��־λ�Է�����в�ȫ��Ĭ�ϲ�ȫ�ַ�Ϊ'0'����ȫ�ַ�������set_group_filler�����趨����������GROUP_FROM_MSBʱ��GROUP_COMPLETE��־λ��Ч���磺
```C++
fmt.set(GROUP_COMPLETE);
fmt.set_group_size(4);
fmt.set_group_separator(" ");
assert(fmt.dump(a, 16, s) == "02db 7583 9f15");

fmt.set(GROUP_FROM_MSB);
assert(fmt.dump(a, 16, s) == "2db7 5839 f15");
```
Ҳ���Խ���������������������set_line_group_countָ��ÿ�е��������磺
```C++
string_t s;
format_t fmt(UPPER_CASE �� GROUP_FROM_MSB);
number_t a("2718281828459045235360287471352662497757247093699959574966");
fmt.set_group_size(8);
fmt.set_group_separator(" ");
fmt.set_line_group_count(4);
cout << fmt.dump(a, 16, s) << endl;
```
�����
```
6EDC2FBE 41B6E8CA 1A10B710 5509E711
40F58F3B 79A7D1B6
```
����set_line_separator�趨�зָ�����Ĭ��Ϊ'\n'��

##ǰ���ַ�
���԰��չ�������������ַ���ǰ���ϡ�ǰ���ַ����Ա�ʾ���ƣ���8����Ϊ��0����16����Ϊ��0x����������set_leading�����趨ĳ���Ƶ�ǰ���ַ���Ҳ������get_leading������ȡĳ���Ƶ�ǰ���ַ���

��ȡָ������base��ǰ���ַ��������ַ�����'\0'��β�������ǰ���ַ����򷵻�NULL  
16���Ƶ�ǰ���ַ���Ĭ��Ϊ"0x"��2����Ϊ"0b"��8����Ϊ"0"
```C++
const char* get_leading(int base);
```

��leadingָ��Ϊ����base��ǰ���ַ�����һ���趨��ȫ����Ч��  
�����ɾ��ĳ�����Ƶ�ǰ���ַ�������leading��ΪNULL���ɡ�
ע�⣡leading�в�Ӧ�����κοհ׷�
```C++
void set_leading(int base, const char* leading);
```

����趨SHOW_LEADING��־λ�������ǰ���ַ�������������磺
```C++
number_t a("1234567890");
string_t s;
set_leading(36, "b36:");

format_t fmt(SHOW_LEADING);
assert(fmt.dump(a, 36, s) == "b36:kf12oi");

fmt.set(UPPER_CASE);
assert(fmt.dump(a, 36, s) == "b36:KF12OI");

fmt.set(UPPER_LEADING);
assert(fmt.dump(a, 36, s) == "B36:KF12OI");
```
ע�⣬ǰ���ַ���mynum���ǲ����ִ�Сд�ģ������Ҫ�ô�д��ĸ��ʾǰ���ַ�����������UPPER_LEADING��־λ��

�����з��Ŵ��������󣬻�����һ�����⣬������Ӧ����ʾ��ǰ���ַ�����໹���Ҳ࣬Ĭ�������mynum��������ʾ��ǰ���ַ�����࣬����ͨ������SIGN_RIGHT_LEADING��־λ��ʹ������ʾ��ǰ���ַ����ұߣ��磺
```C++
number_t a("-1234567890");
string_t s;
set_leading(36, "b36:");

format_t fmt(SHOW_LEADING);
assert(fmt.dump(a, 36, s) == "-b36:kf12oi");

fmt.set(SIGN_RIGHT_LEADING);
assert(fmt.dump(a, 36, s) == "b36:-kf12oi");
```

##ע������
ǰ���ַ�Ϊȫ�����ݣ����ú�load��dump�����Լ���׼�������������Ч����û���κ��̰߳�ȫ��ʩ���ʾ�����Ҫĳ���߳��е���set_leading����������һ���߳��е���load��dump�Ⱥ�����
