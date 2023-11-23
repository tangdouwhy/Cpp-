## 基本概念:

### 容器:vector;

vector数据结构和数组非常相似,也称为单端数组,可以动态扩展

### 算法:for_each;

```c++
class Person
{
public:
	Person(string name, int age) :m_Name(name), m_age(age)
	{

	}
	string m_Name;
	int m_age;
};
void print(Person s)
{
	cout << s.m_Name << " " << s.m_age << endl;
}
for_each(v.begin(), v.end(), print);//只需要函数名
```

### 迭代器:vector<T>::iterator;

![起始迭代器和结束迭代器位置解析图](F:\学习笔记\STL资料\day1\1-课堂资料\起始迭代器和结束迭代器位置解析图.png)

### 类似动态数组

动态分配内存，并不是原有空间下分配，而是找一个新空间，将原有数据拷贝到新空间下，然后释放掉原有空间

## 容器嵌套容器:

```c++
//容器嵌套容器
vector<vector<int>>v;
//创建小容器
vector<int>v1;
vector<int>v2;
vector<int>v3;
vector<int>v4;
//向小容器添加数据
for (int i = 0; i < 4; i++)
{
	v1.push_back(i + 1);
	v2.push_back(i + 2);
	v3.push_back(i + 3);
	v4.push_back(i + 4);
}
//将小容器插入到大容器
v.push_back(v1);
v.push_back(v2);
v.push_back(v3);
v.push_back(v4);
//通过大容器，把所有数据遍历一遍
for (vector<vector<int>>::iterator it = v.begin(); it != v.end(); it++)
{
	for (vector<int>::iterator vit = (*it).begin(); vit != (*it).end(); vit++)
	{
		cout << *vit;
	}
	cout << endl;
}
```

## 构造函数:

vector<T> v;//默认构造函数

```c++
vector<int>v1;//默认构造函数
```

vector<T>(v.begin(),v.end());//将v[begin(),end())区间中的元素拷贝给本身，左闭右开

```c++
int a[10];
vector<int>v2(a, a+10);//左闭右开的区间构造 可以放迭代器也可以放指针 会发生隐式转换
```

vector<T>(n,elem);//构造函数将n个elem拷贝给本身

```c++
vector<int>v3(10, 100);//十个一百初始化
```

vector<T>(const vector &vec);//拷贝构造函数

```c++
vector<int>v4(v3);//拷贝构造函数
```

## 赋值操作:

vector& operator=(const vector &vec);//重载等号运算符

```c++
	vector<int>v1;
	for (int i = 0; i < 10; i++)
	{
		v1.push_back(i);
	}
	vector<int>v2;
	v2 = v1;
```

assign(beg,end);//将[beg,end)区间中的数据拷贝赋值给本身，左闭右开

```c++
	vector<int>v3;
	v3.assign(v1.begin(), v1.end());
```

assign(n,elem);//将n个elem拷贝复制给本身

```c++
	vector<int>v4;
	v4.assign(10, 100);
```

## 容量和大小:

empty();//判断容器是否为空

capacity();//容器的容量

size();//返回容器中元素的个数

```c++
	vector<int>v1;
	for (int i = 0; i < 10; i++)
	{
		v1.push_back(i);
	}
	if (v1.empty())//为真代表容器为空
	{
		cout << "v1为空" << endl;
	}
	else
	{
		cout << "v1不为空" << endl;
		cout << "v1的容量" << v1.capacity() << endl;
		cout << "v1的元素个数" << v1.size() << endl;//容量大于大小
	}
```

resize(int num);//重新指定容器的长度为num,若容器变长,则以默认值填充新位置

//如果容器变短,则末尾超出容器长度的元素被删除

resize(int num,elem);//重新指定容器的长度为num,若容器变长,则以elem值填充新位置

//如果容器变短,则末尾超出容器长度的元素被删除

```C++
	v1.resize(15);
	for_each(v1.begin(), v1.end(), print);
	cout << endl;
	v1.resize(25, 10);
	for_each(v1.begin(), v1.end(), print);
	cout << endl;
	v1.resize(10);
	for_each(v1.begin(), v1.end(), print);//大了添加默认值，小了删除尾部多余的
```

## 插入和删除:

push_back(ele);//尾部插入元素ele

```C++
	vector<int>v1;
	for (int i = 0; i < 10; i++)
	{
		v1.push_back(i);
	}
```

pop_back();//删除最后一个元素

```c++
	void print(int a)
	{
		cout << a << " ";
	}
	v1.pop_back();
	for_each(v1.begin(), v1.end(), print);
	cout << endl;
```

insert(const_iterator pos,ele);//迭代器指向位置pos插入元素ele

```c++
	v1.insert(v1.begin()+1, 100);
	for_each(v1.begin(), v1.end(), print);
	cout << endl;
```

insert(const_iterator pos,int count,ele);//迭代器指向位置pos插入count个元素ele

```c++
	v1.insert(v1.begin(), 2, 1000);
	for_each(v1.begin(), v1.end(), print);
	cout << endl;
```

erase(const_iterator pos);//删除迭代器指向的元素

```c++
	v1.erase(v1.begin());
	for_each(v1.begin(), v1.end(), print);
	cout << endl;
```

erase(const_iterator start,const_iterator end);//删除迭代器从start到end之间的元素,左闭右开

```c++
	v1.erase(v1.begin(), v1.begin() + 2);//左闭右开
	for_each(v1.begin(), v1.end(), print);
	cout << endl;
```

clear();//删除容器中所有元素

```c++
	v1.clear();
	for_each(v1.begin(), v1.end(), print);
	cout << endl;
```

## 数据存取:

at(int idx);//返回索引idx所指的数据

operator[];//返回索引idx所指的数据

front();//返回容器中第一个数据元素

back();//返回容器中最后一个数据元素

```c++
	void print(int a)
	{
		cout << a << " ";
	}
	vector<int>v1;
	for (int i = 0; i < 10; i++)
	{
		v1.push_back(i);
	}
    for_each(v1.begin(), v1.end(), print);
    cout << endl;
    cout << v1.at(1);
    cout << endl;
    cout << v1[1];
    cout << endl;
    for_each(v1.begin(), v1.end(), print);
    cout << endl;
    cout << "第一个元素为: " << v1.front() << endl;
    cout << "最后一个元素为: " << v1.back() << endl;
```

## 互换容器:

swap(vec);//将vec与本身的元素互换

```C++
	vector<int>v;
	for (int i = 0; i < 100000; i++)
	{
		v.push_back(i);
	}
	cout << "v的容量为: " << v.capacity() << endl;
	cout << "v的大小为: " << v.size() << endl;
	v.resize(3);
	cout << "v的容量为: " << v.capacity() << endl;//容量未变
	cout << "v的大小为: " << v.size() << endl;
```

## 巧用swap来收缩:

```c++
    vector<int>v;
    for (int i = 0; i < 100000; i++)
    {
        v.push_back(i);
    }
    cout << "v的容量为: " << v.capacity() << endl;
    cout << "v的大小为: " << v.size() << endl;
    v.resize(3);
    cout << "v的容量为: " << v.capacity() << endl;//容量为变
    cout << "v的大小为: " << v.size() << endl;
    //巧用swap来收缩
    vector<int>(v).swap(v);//!!!!!!
    //vector<int>(v)匿名对象
    //vector<int>x();调用拷贝构造函数，x不写就是匿名，拷贝一个v
    //此时会按照v的大小进行构造
    //所以x的大小和容量为3
    //x和v进行互换；
    //匿名对象结束自动释放,调用析构函数
    cout << "v的容量为: " << v.capacity() << endl;
    cout << "v的大小为: " << v.size() << endl;
```

<img src="F:\学习笔记\STL资料\day1\1-课堂资料\巧用swap收缩内存原理.png" alt="巧用swap收缩内存原理" style="zoom:75%;" />

## 预留空间:

减少vector在动态扩展容量时的扩展次数

reserve只是为了不让迭代器指向的地址发生改变

只改变容量不申请内存

reserve()函数预分配出的空间没有被初始化,不可访问

```C++
	vector<int>v1;
	//利用reserve预留空间
	v1.reserve(100000);
	int num = 0;//统计开辟的次数
	int* p = NULL;
	for (int i = 0; i < 100000; i++)
	{
		v1.push_back(i);
		if (p != &v1[0])
		{
			p = &v1[0];
			num++;
		}
	}
	cout << "v1开辟的次数: " << num << endl;
```
