## 基本概念:

### 功能:

将数组进行链式存储

### 链表:(list)

是一种物理存储单元上非连续的存储结构,数据元素的逻辑顺序是通过链表中的指针链接实现的

### 链表的组成:

链表由一系列结点组成

### 结点的组成:

一个是存储数据元素的数据域,另一个是存储下一个结点地址的指针域

STL中的链表是一个双向循环链表

## 构造函数:

list<T>list;//list采用模板类实现,对象的默认构造形式

list(beg,end);//构造函数将区间[beg,end)区间中的元素拷贝给本身,左闭右开

list(n,elem);//构造函数将n个elem拷贝给本身

list(const list &lst);//拷贝构造函数

```c++
void print(const list<int>& L)
{
	for (list<int>::const_iterator it = L.begin(); it != L.end(); it++)
	{
		cout << *it << " ";
	}
	cout << endl;
}
void test01()
{
	list<int>L1;//默认构造
	L1.push_back(10);
	L1.push_back(20);
	L1.push_back(30);
	L1.push_back(40);
	print(L1);
	list<int>L2(L1);//拷贝构造
	print(L2);
	list<int>L3(L1.begin(), L1.end());//区间构造
	print(L3);
	list<int>L4(10, 1000);//n个elem
	print(L4);
}
```

## 赋值和交换:

assign(beg,end);//将[beg,end)区间中的数据拷贝赋值给本身

assign(n,elem);//将n个elem拷贝赋值给本身

list& operator=(const list &list);//重载等号操作符

swap(lst);//将lst与本身的元素互换

```c++
void print(const list<int>& L)
{
	for (list<int>::const_iterator it = L.begin(); it != L.end(); it++)
	{
		cout << *it << " ";
	}
	cout << endl;
}
void test01()
{
	list<int>L1;
	L1.push_back(10);
	L1.push_back(20);
	L1.push_back(30);
	L1.push_back(40);
	print(L1);
	list<int>L2 = L1;//=赋值
	print(L2);
	list<int>L3;
	L3.assign(L2.begin(), L2.end());//区间赋值
	print(L3);
	list<int>L4;
	L4.assign(10, 100);//n个elem
	print(L4);
}
void test02()
{
	list<int>L1;
	L1.push_back(10);
	L1.push_back(20);
	L1.push_back(30);
	L1.push_back(40);

	list<int>L2;
	L2.assign(10, 100);
	print(L1);
	print(L2);
	L1.swap(L2);
	print(L1);
	print(L2);
}
```

## 容量和大小:

empty();//判断容器是否为空

size();//返回容器中元素的个数

resize(int num);//重新指定容器的长度为num,若容器变长,则以默认值填充新位置

//如果容器变短,则末尾超出容器长度的元素被删除

resize(int num,elem);//重新指定容器的长度为num,若容器变长,则以elem值填充新位置

//如果容器变短,则末尾超出容器长度的元素被删除

```c++
void print(const list<int>& L)
{
	for (list<int>::const_iterator it = L.begin(); it != L.end(); it++)
	{
		cout << *it << " ";
	}
	cout << endl;
}
void test01()
{
	//大小操作
	list<int>L1;
	L1.push_back(10);
	L1.push_back(20);
	L1.push_back(30);
	L1.push_back(40);
	print(L1);
	if (L1.empty())
	{
		cout << "L1为空!" << endl;
	}
	else
	{
		cout << "L1不为空!" << endl;
		cout << "L1的元素个数为: " << L1.size() << endl;
	}
	L1.resize(10, 10000);
	print(L1);
	L1.resize(2);
	print(L1);
}
```

## 插入和删除:

push_back(elem);//在容器尾部加入一个元素

pop_back();//删除容器中最后一个元素

push_from(elem);//在容器开头插入一个元素

insert(pos,elem);//在pos位置插elem元素的拷贝,返回新数据的位置

insert(pos,n,elem);//在pos位置插入n个elem数据,无返回值

insert(pos,beg,end);//在pos位置插入[beg,end)区间的数据,返回下一个数据的位置,左闭右开

clear();//移除容器的所有数据

erase(beg,end);//删除[beg,end)区间的数据,返回下一个数据的位置

erase(pos);//删除pos位置的数据,返回下一个数据的位置

remove(elem);//删除容器中所有与elem值匹配的元素

```c++
void print(const list<int>& L)
{
	for (list<int>::const_iterator it = L.begin(); it != L.end(); it++)
	{
		cout << *it << " ";
	}
	cout << endl;
}
void test01()
{
	list<int>L;
	//尾插
	L.push_back(10);
	L.push_back(20);
	L.push_back(30);
	//头插
	L.push_front(100);
	L.push_front(200);
	L.push_front(300);
	print(L);
	//尾删
	L.pop_back();
	print(L);
	//头删
	L.pop_front();
	print(L);
	//insert插入
	list<int>::iterator it = L.begin();
	it++;
	L.insert(it, 1000);
	print(L);
	it = L.begin();
	//erase删除
	L.erase(it++);
	print(L);
	//移除
	L.push_back(10000);
	print(L);
	L.remove(10000);
	print(L);
	//清空
	L.clear();
	print(L);
}
```

## 数据存取:

front();//返回第一个元素

back();//返回最后一个元素

```c++
void test01()
{
	list<int>L;
	L.push_back(10);
	L.push_back(20);
	L.push_back(30);
	L.push_back(40);
	for (list<int>::iterator it = L.begin(); it != L.end(); it++)
	{
		cout << *it << " ";
	}
	cout << endl;
	cout << "L第一个元素: " << L.front() << endl;
	cout << "L最后一个元素: " << L.back() << endl;
}
//list<int>::iterator it=L.begin();
//it++;it--;支持双向
//it=it+1;//不报错就支持随机访问，在list里面这种写法报错
```

## 反转和排序:

reverse();//反转链表

sort();//链表排序

```c++
void print(const list<int>& L)
{
	for (list<int>::const_iterator it = L.begin(); it != L.end(); it++)
	{
		cout << *it << " ";
	}
	cout << endl;
}
bool cmp(int a1,int a2)
{
	//降序,第一个数 > 第二个数
	return a1 > a2;
}
void test01()
{
	list<int>L1;
	L1.push_back(20);
	L1.push_back(10);
	L1.push_back(50);
	L1.push_back(40);
	L1.push_back(30);
	print(L1);
	//反转后
	L1.reverse();
	print(L1);
	//排序
	//所有不支持随机访问迭代器的容器,不可以用标准算法
	//不支持随机访问迭代器的容器,内部会提供对应的一些算法
	L1.sort();//从小到大
	print(L1);
	L1.sort(cmp);//从大到小 , 用reverse会浪费效率
	print(L1);
}
```

## 排序案例:

案例描述:将Person自定义数据类型进行排序,Person中属性有姓名,年龄,身高

排序规则:按照年龄进行升序,如果年龄相同按照身高进行降序

```c++
class Person
{
public:
	Person(string name, int age, int height) :m_name(name),m_age(age),m_height(height)
	{

	}
	string m_name;
	int m_age;
	int m_height;
};
void print(const list<Person>& L)
{
	for (list<Person>::const_iterator it = L.begin(); it != L.end(); it++)
	{
		cout << (*it).m_name << " " << (*it).m_age << " " << (*it).m_height << endl;
	}
}
bool cmp(Person p1, Person p2)
{
	if (p1.m_age == p2.m_age)
	{
		return p1.m_height > p2.m_height;
	}
	return p1.m_age < p2.m_age;
}
void test01()
{
	list<Person>L;
	Person p1("刘备", 35, 175);
	Person p2("曹操", 45, 180);
	Person p3("孙权", 40, 170);
	Person p4("赵云", 25, 190);
	Person p5("张飞", 35, 160);
	Person p6("关羽", 35, 200);
	L.push_back(p1);
	L.push_back(p2);
	L.push_back(p3);
	L.push_back(p4);
	L.push_back(p5);
	L.push_back(p6);
	L.sort(cmp);
	print(L);
}
```

