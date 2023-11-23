##基本概念

本质:

string是C++风格的字符串,而string本质上是一个类

### string和char*的区别:

char*是一个指针

string是一个类,类内部封装了char*,管理这个字符串,是一个char*型的容器

### 特点:

string内部封装了很多成员方法

例如:查找find,拷贝copy,删除delete,替换replace,插入insert

string管理char*所分配的内存,不用担心复制越界和取值越界,由内部进行负责

## 构造函数:

string();//创建一个空字符串 例如:string str;

string(const char*s);//使用字符串s初始化;

string(const string&str);//使用一个string对象初始化另一个string对象;

string(int n,char c);//使用n个字符c初始化

```c++
string s1;//默认构造
string s2("aaa");//使用字符串初始化
const char* str = "aaa";
string s3(str);
string s4(s3);//拷贝构造
string s5(10, 'a');//十个a
cout << s5 << endl;
```

## 赋值操作:

string& operator=(const char* s);//char*类型字符串 赋值给当前字符串

string& operator=(const string &s);//把字符串s赋给当前字符串

string& operator=(char c);//把字符赋值给当前字符串

string& assign(const char *s);//把字符串s赋给当前的字符串

string& assign(const char *s, int n);//把字符串s的前n个字符赋给当前的字符串

string& assign(const string &s);//把字符串s赋给当前字符串

string& assign(int n, char c);//用n个字符c赋给当前字符串

```c++
string str1;
str1 = "hello world";
cout << str1 << endl;
string str2;
str2 = str1;
cout << str2 << endl;
string str3;
str3 = 'a';
cout << str3 << endl;
string str4;
str4.assign("hello C++");
cout << str4 << endl;
string str5;
str5.assign("hello C++", 5);//前几个字符去赋值
cout << str5 << endl;
string str6;
str6.assign(str5);
cout << str6 << endl;
string str7;
str7.assign(10, 'w');
cout << str7 << endl;
```

## 字符串拼接:

string& operator+=(const char* str);//重载+=操作符

string& operator+=(const char c);//重载+=操作符

string& operator+=(const string& str);//重载+=操作符

string& append(const char *s);//把字符串s连接到当前字符串结尾

string& append(const char *s, int n);//把字符串s的前n个字符连接到当前字符串结尾

string& append(const string &s);//同operator+=(const string& str)

string& append(const string &s, int pos, int n);//字符串s中从pos开始的n个字符连接到字符串结尾

```c++
//字符串拼接
string str1="我";
str1 += "爱玩游戏";
cout << str1 << endl;
str1 += ';';
cout << str1 << endl;
string str2="LOL DNF";
str1 += str2;
cout << str1 << endl;
string str3="I";
str3.append("Love");
cout << str3 << endl;
str3.append("game abcde", 4);
cout << str3 << endl;、
```

## 查找和替换:

int find(const string& str, int pos=0)const;//查找str第一次出现位置,从pos开始查找

未找到返回 string::npos;

int find(const char* s, int pos=0)const;//查找s第一次出现位置,从pos开始查找

int find(const char* s, int pos, int n)const;//从pos位置查找s的前n个字符第一次位置

int find(const char c, int pos=0)const;查找字符c第一次出现的位置

int rfind(const string& str, int pos=npos)const;//查找s最后一次出现位置,从pos开始查找

int rfind(const char* s, int pos=npos)const;//查找s最后一次出现的位置,从pos开始查找

int rfind(const char* s, int pos, int n)const;//从pos查找s的前n个字符最后一次位置

int rfind(const char c,int pos=0)const;//查找字符c最后一次位置

string& replace(int pos, int n, const string& str);//替换从pos开始n个字符为字符串str

string& replace(int pos, int n, const char* s);//替换从pos开始的n个字符为字符串s

```c++
string str1="abcdefgde";
int pos=str1.find("de");
if (pos == string::npos)
{
	cout << "未找到字符串" <<pos<< endl;
}
else
{
	cout << "找到字符串 pos=" << pos << endl;
}
//rfind和find的区别
//rfind是从右往左查找 find从左往右查找
//find第一次出现的位置
//find最后一次出现的位置
pos=str1.rfind("de");
cout << "pos=" << pos << endl;
```

```c++
string str1 = "abcdefg";
str1.replace(1, 3, "1111");
//把bcd换成1111
cout << str1 << endl;
```

## 字符串比较:

=返回 0 >返回1 <返回-1

int compare(const string &s)const;//与字符串s比较

int compare(const char *s)const;//与字符串s比较

```c++
string str1 = "aello";
string str2 = "zello";
if (str1.compare(str2) == 0)
{
	cout << "str1等于str2" << endl;
}
else if (str1.compare(str2) == 1)
{
	cout << "str1大于str2" << endl;
}
else
{
	cout << "str1小于str2" << endl;
}
```

## 字符存取:

char& operator[] (int n);//通过[]方式取字符

char& at(int n);//通过at方式获取字符串,会检查越界

```c++
string str = "hello";
cout << str << endl;
//1.通过[]
for (int i = 0; i < str.length(); i++)
{
	cout << str[i];
}
cout << endl;
//2.通过at
for (int i = 0; i < str.length(); i++)
{
	cout << str.at(i) << " "; //会检查下标
}
cout << endl;
```

## 插入和删除:

string& insert(int pos, const char* s);//插入字符串

string& insert(int pos, const string& str);//插入字符串

string& insert(int pos, int n, char c);//在指定位置插入n个字符c

string& erase(int pos, int n=npos);//删除从pos开始的n个字符

```c++
//字符串插入和删除
string str = "hello";
str.insert(1, "111");
cout << str << endl;
//删除
str.erase(1, 3);//不填第二个参数就是从pos开始删完,包括pos
cout << str << endl;
```

## 子串获取:

string substr(int pos=0, int n=npos)const;//返回由pos开始的n个字符组成的字符串

```c++
string str = "abcdef";
string substr = str.substr(1, 3);
cout << substr << endl;
```

```c++
string emaill = "zhangshan@sina.com";
string substr = emaill.substr(0, emaill.find('@'));//能刚好截到@前面,不包括@
cout << substr << endl;
```
