map中所有元素都是pair

pair中第一个元素为key(键值),起到索引作用,第二个元素为value(实值)

所有元素都会根据元素的键值自动排序

map/multimap属于关联式容器,底层结构是用二叉树实现

可以根据key值快速找到value值

map和multimap的区别:

map不允许容器中有重复key值元素

multimap允许容器中有重复key值元素

## 构造与赋值:

map<T1,T2>mp;//map默认构造函数

map(const map &mp);//拷贝构造函数

map& operator=(const map &mp);//重载等号操作符

```c++
void print(const map<int, int>& m)
{
	for (map<int, int>::const_iterator it = m.begin(); it != m.end(); it++)
	{
		cout << (*it).first << " " << (*it).second << endl;
	}
}
void test01()
{
	map<int, int>m1;
	//按照key自动排序
	m1.insert(pair<int, int>(1, 10));
	m1.insert(pair<int, int>(3, 10));
	m1.insert(pair<int, int>(2, 10));
	m1.insert(pair<int, int>(4, 10));
	print(m1);
	map<int, int>m2(m1);
	print(m2);
	//赋值
	map<int, int>m3 = m2;
	print(m3);
}
```

## 大小和交换:

size();//返回容器中元素的数目

empty();//判断容器是否为空

swap(st);//交换两个集合容器

```c++
void print(const map<int, int>& m)
{
	for (map<int, int>::const_iterator it = m.begin(); it != m.end(); it++)
	{
		cout << (*it).first << " " << (*it).second << endl;
	}
}
void test01()
{
	map<int, int>m;
	m.insert(pair<int, int>(1, 10));
	m.insert(pair<int, int>(2, 10));
	m.insert(pair<int, int>(5, 10));
	m.insert(pair<int, int>(6, 10));
	if (m.empty())
	{
		cout << "m为空" << endl;
	}
	else
	{
		cout << "m不为空" << endl;
		cout << "m的大小" << m.size() << endl;
	}
}
void test02()
{
	map<int, int>m;
	m.insert(pair<int, int>(1, 10));
	m.insert(pair<int, int>(2, 10));
	m.insert(pair<int, int>(5, 10));
	m.insert(pair<int, int>(6, 10));

	map<int, int>m2;
	m2.insert(pair<int, int>(20, 10));
	m2.insert(pair<int, int>(21, 10));
	m2.insert(pair<int, int>(50, 10));
	m2.insert(pair<int, int>(30, 10));
	m.swap(m2);
	print(m);
	print(m2);
}
```

## 插入和删除:

insert(elem);//在容器中插入元素

[]的重载;

clear();//清除所有元素

erase(pos);//删除pos迭代器所指的元素,返回下一个元素的迭代器

erase(beg,end);//删除区间[beg,end)的所有元素,返回下一个元素的迭代器

erase(key);//删除容器中值为key的元素

```c++
	//第一种
	map<int, int>m;
	m.insert(pair<int, int>(1, 10));
	m.insert(pair<int, int>(2, 10));
	m.insert(pair<int, int>(5, 10));
	m.insert(pair<int, int>(6, 10));
	//第二种
	m.insert(make_pair(2, 20));//不用写模板参数
	//第三种
	m.insert(map<int, int>::value_type(3, 30));
	//第四种
	m[4] = 40;//不建议使用
	print(m);
	//cout << m[7] << endl;//会自动创建一个,key为7,value为0的数
	//主要用于通过key访问value
	m.erase(m.begin());
	//删除
	print(m);
	m.erase(m.begin(), m.end());//区间删除
	m.clear();//清空
```

## 查找和统计:

find(key);//查找key是否存在,若存在,返回该键的元素的迭代器,若不存在,返回map.end();

count(key);//统计key的元素个数

```c++
	map<int, int>m;
	m.insert(pair<int, int>(1, 10));
	m.insert(pair<int, int>(2, 10));
	m.insert(pair<int, int>(5, 10));
	m.insert(pair<int, int>(6, 10));

	map<int, int>m2;
	m2.insert(pair<int, int>(20, 10));
	m2.insert(pair<int, int>(21, 10));
	m2.insert(pair<int, int>(50, 10));
	m2.insert(pair<int, int>(30, 10));
	m.swap(m2);
	print(m);
	print(m2);
	cout << (*m.find(20)).first << " " << (*m.find(20)).second << endl;
	cout << m.count(20);
```

## 排序:

利用仿函数

```c++
class cmp
{
public:
	bool operator()(int v1, int v2)const
	{
		return v1 > v2;
	}
};
void print(const map<int, int,cmp>& m)
{
	for (map<int, int,cmp>::const_iterator it = m.begin(); it != m.end(); it++)
	{
		cout << (*it).first << " " << (*it).second << endl;
	}
}
void test01()
{
	//第一种
	map<int, int,cmp>m;
	m.insert(pair<int, int>(1, 10));
	m.insert(pair<int, int>(2, 10));
	m.insert(pair<int, int>(5, 10));
	m.insert(pair<int, int>(6, 10));
	//第二种
	m.insert(make_pair(2, 20));//不用写模板参数
	//第三种
	m.insert(map<int, int>::value_type(3, 30));
	//第四种
	//m[4] = 40;//不建议使用
	print(m);
	//cout << m[7] << endl;//会自动创建一个,key为7,value为0的数
	//主要用于通过key访问value
	m.erase(m.begin());
	//删除
	//print(m);
	//m.erase(m.begin(), m.end());//区间删除
	//m.clear();//清空
}
```

