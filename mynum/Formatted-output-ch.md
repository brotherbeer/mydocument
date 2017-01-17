����������ĸ�ʽ�����
-------------

 * [��ʽ������](#��ʽ������)
 * [����](#����)
 * [ע������](#ע������)
 * [ʾ��](#ʾ��)
 * [�㷨](#�㷨)

##��ʽ������

��ʽ��������format_t���ɳ�Ա����ָ�����ָ�ʽ����Ϣ���ɳ�Ա����dump��ָ���Ĵ����������ʽ��Ϊ�ַ�����
```C++
struct format_t
{
    format_flags_t flags;  // ��ʽ����־λ
    int base;              // ����
    size_t group;          // ÿ�������е��ַ�����
    string_t separator;    // ��ָ���
    char filler;           // ������
 
    /** Ĭ�Ϲ��캯��*/
    format_t();
    /** ���캯������ff��ʼ����Աflags*/
    format_t(format_flags_t ff);
    /** ���캯������ff��ʼ����Աflags��b��ʼ����Աbase*/
    format_t(format_flags_t ff, int b);

    /** ��ffָ���ı�־λ����flags */
    void set(format_flags_t ff);
    /** ��ffָ���ı�־λ��flags����� */
    void clear(format_flags_t ff);
    /** ������б�־λ */
    void clear_all();

    /** �ж��Ƿ����ffָ���ı�־λ */
    bool has(format_flags_t ff) const;
	/** �������б�־λ*/
    format_flags_t get() const;

	/** ������������a��ָ���ĸ�ʽ����Ϣת�ɽ���Ϊb���ַ���str */
    string_t& dump(const number_t& a, int b, string_t& str) const;

	/** �����ָ��b��������ɳ�Ա����base���� */
    string_t  dump(const number_t& a) const;
    string_t& dump(const number_t& a, string_t& str) const;
}; 
```
###����


###��ʽ����־λ
|��־λ|����|
|------|----|
|UPPER_CASE| �ô�д��ĸ����ַ��������޴˱�־λ����Сд��ĸ|
|SHOW_POS| ���ָ������������Ϊ�����������+��|
|SHOW_LEADING| ���ǰ���ַ���ʮ�����ƶ�Ӧ0x�������ƶ�Ӧ0b�ȣ�ǰ���ַ������趨|
|SIGN_RIGHT_LEADING| ������ǰ���ַ��Ҳ࣬��0x-ab�����޴˱�־λ������ǰ���ַ���࣬��-0xab|
|GROUP_COMPELTE| ������һ�������е��ַ�����С��group������fillerָ�����ַ����|
|ZERO_NO_LEADING| 0��ǰ���ַ�|
|ZERO_POS| �������SHOW_POS��־λ��ָ������������Ϊ0�������+��|
|ZERO_NEG| ָ������������Ϊ0�����-��|
|EMPTY_AS_ERROR| ���ַ���Ϊ�����ַ���������Ϊ0|

###�趨ǰ���ַ�


##����

������������תΪ�������ַ���
```C++
string_t& number_t::to_bin_string(string_t& str) const;
```

������������תΪ�˽����ַ���
```C++
string_t& number_t::to_oct_string(string_t& str) const;
```

������������תΪʮ�����ַ���
```C++
string_t& number_t::to_dec_string(string_t& str) const;
```

������������תΪʮ�������ַ���
```C++
string_t& number_t::to_hex_string(string_t& str) const;
```

������������תΪbase�����ַ���
```C++
string_t& number_t::to_string(string_t& str, int base = 10) const;
```

����string_t����
```C++
string_t to_bin_string() const;
string_t to_oct_string() const;
string_t to_dec_string() const;
string_t to_hex_string() const;
string_t to_string(int base = 10) const;
```

