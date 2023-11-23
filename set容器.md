## set:

### 简介:

所有元素都会在插入时自动被排序

自动排序!

### 本质:

set/multiset属于关联式容器,底层结构是用二叉树实现

### set和multiset区别:

set不允许容器中有重复的元素

multiset允许容器中有重复的元素

包含set头文件就都可以用了

## 构造函数:

set<T> st;//默认构造函数

set(const set &st);//拷贝构造函数

## 赋值:

set& operator=(const set &st);//重载等号操作符

```c++
void print(const set<int>& s)
{
	for (set<int>::const_iterator it = s.begin(); it != s.end(); it++)
	{
		cout<<*it<<" ";
	}
	cout<<endl;
}
void test01()
{
	set<int>s1;
	//插入数据只有insert方式
	s1.insert(10);
	s1.insert(40);
	s1.insert(30);
	s1.insert(20);
	s1.insert(30);
	print(s1);
	//set容器特点:所有元素在插入时候自动被排序
	//set容器不允许插入重复值

	//拷贝构造
	set<int>s2(s1);
	print(s2);

	//赋值操作
	set<int>s3;
	s3 = s2;
	print(s3);
}
```

## 大小和交换:

size();//返回容器中元素的数目

empty();//判断容器是否为空

swap(st);//交换两个set容器

不允许重新指定大小

```c++
void print(const set<int>& s)
{
	for (set<int>::const_iterator it = s.begin(); it != s.end(); it++)
	{
		cout << *it << " ";
	}
	cout << endl;
}
void test01()
{
	set<int>s1;
	//插入数据
	s1.insert(10);
	s1.insert(30);
	s1.insert(20);
	s1.insert(40);
	print(s1);
	//判断是否为空
	if (s1.empty())
	{
		cout << "s1为空" << endl;
	}
	else
	{
		cout << "s1不为空" << endl;
		cout << "s1的大小为:" << s1.size() << endl;
	}
	set<int>s2;
	s2.insert(100);
	s2.insert(300);
	s2.insert(200);
	cout << "s1  ";
	print(s1);
	cout << "s2  ";
	print(s2);
	s1.swap(s2);
	cout << "s1  ";
	print(s1);
	cout << "s2  ";
	print(s2);
}
```

## 插入和删除:

insert(elem);//在容器中插入元素

clear();//清除所有元素

erase(pos);//删除pos迭代器所指的元素,返回下一个元素的迭代器

erase(beg,end);//删除区间[beg,end)的所有元素,返回下一个元素的迭代器,左闭右开

erase(elem);//删除容器中值为elem的元素

```c++
void print(const set<int>& s)
{
	for (set<int>::const_iterator it = s.begin(); it != s.end(); it++)
	{
		cout << *it << " ";
	}
	cout << endl;
}
void test01()
{
	set<int>s;
	//插入
	s.insert(20);
	s.insert(10);
	s.insert(30);
	s.insert(40);
	//遍历
	print(s);
	//删除
	set<int>::iterator it = s.begin();
	it++;
	s.erase(it);
	print(s);
	//重载版本
	s.erase(30);
	print(s);
	//清空
	s.clear();
	//s.erase(s.begin(), s.end());
}
```

## 查找和统计:

find(key);//查找key是否存在,若存在,返回该键的元素的迭代器;若不存在,返回set.end();

count(key);//统计key的元素个数

```c++
void print(const set<int>& s)
{
	for (set<int>::const_iterator it = s.begin(); it != s.end(); it++)
	{
		cout << *it << " ";
	}
	cout << endl;
}
void print(const multiset<int>& s)
{
	for (multiset<int>::const_iterator it = s.begin(); it != s.end(); it++)
	{
		cout << *it << " ";
	}
	cout << endl;
}
void test01()
{
	set<int>s;
	s.insert(10);
	s.insert(30);
	s.insert(20);
	s.insert(50);
	print(s);
	multiset<int>s1;
	s1.insert(30);
	s1.insert(40);
	s1.insert(20);
	s1.insert(30);
	print(s1);
	set<int>::iterator it;
	//查找,返回值是迭代器
	it = s.find(60);
	if (it != s.end())
	{
		cout << "找到元素" << *it << endl;
	}
	else
	{
		cout << "未找到元素" << endl;
	}
	//统计三十的个数
	int num = s.count(10);
	int num1 = s1.count(30);
	cout << num << endl;
	cout << num1 << endl;
}
```

## set和multiset的区别:

set不可以插入重复数据,而multiset可以

set插入数据的同时会返回插入结果,表示插入是否成功

multiset不会检测数据,因此可以插入重复数据

```c++
void print(const set<int>& s)
{
	for (set<int>::const_iterator it = s.begin(); it != s.end(); it++)
	{
		cout << *it << " ";
	}
	cout << endl;
}
void print(const multiset<int>& s)
{
	for (multiset<int>::const_iterator it = s.begin(); it != s.end(); it++)
	{
		cout << *it << " ";
	}
	cout << endl;
}
void test01()
{
	set<int>s1;
	multiset<int>s2;
	//pair 返回值
	//s1.insert(20);
	pair<set<int>::iterator,bool> ret=s1.insert(20);
	if (ret.second)
	{
		cout << "插入成功!" << endl;
	}
	else
	{
		cout << "插入失败" << endl;
	}
	s1.insert(30);
	s1.insert(10);
	s1.insert(40);
	s2.insert(20);
	s2.insert(20);
	//multiset允许插入重复值
	//返回迭代器
	s2.insert(40);
	s2.insert(30);
	print(s1);
	print(s2);
}
```

## 内置类型指定排序规则:

set容器默认排序规则为从小到大

利用仿函数,可以改变排序规则

```C++
class mycmp
{
public:
	//仿函数
	bool operator()(const int v1, const int v2) const
	{
		return v1 > v2;
	}
};
void print(const set<int>& s)
{
	for (set<int>::const_iterator it = s.begin(); it != s.end(); it++)
	{
		cout << *it << " ";
	}
	cout << endl;
}
void print(const set<int,mycmp>& s)
{
	for (set<int,mycmp>::const_iterator it = s.begin(); it != s.end(); it++)
	{
		cout << *it << " ";
	}
	cout << endl;
}
void test01()
{
	set<int>s1;
	//必须要在插之前
	s1.insert(10);
	s1.insert(40);
	s1.insert(20);
	s1.insert(50);
	s1.insert(30);
	print(s1);
	//指定排序规则为从大到小
	set<int,mycmp>s2;
	//必须要在插之前
	s2.insert(10);
	s2.insert(40);
	s2.insert(20);
	s2.insert(50);
	s2.insert(30);
	print(s2);
}
```

## 自定义类型指定排序规则:

```c++
class Person
{
public:
	Person(string name, int age) :m_name(name), m_age(age)
	{

	}
	string m_name;
	int m_age;
};
class cmp
{
public:
	bool operator()(const Person& p1, const Person& p2) const{return p1.m_age > p2.m_age;}
};
void test()
{
	//自定义数据类型指定排序规则
	set<Person,cmp>s;
	//创建person对象
	Person p1("刘备", 24);
	Person p2("关羽", 28);
	Person p3("张飞", 25);
	Person p4("赵云", 21);
	s.insert(p1);
	s.insert(p2);
	s.insert(p3);
	s.insert(p4);
	for (set<Person,cmp>::const_iterator it = s.begin(); it != s.end(); it++)
	{
		cout << (*it).m_name << (*it).m_age << endl;
	}

}
```

