## 概述：

!!!!    类名()  代表匿名对象

算法主要是由头文件 `<algorithm>` `<functional>` `<numeric>`组成

`<algorithm>`是所有STL头文件中最大的一个,范围涉及到比较,交换,查找,遍历操作,复制,修改等等

`<numeric>`体积很小,只包括几个在序列上面进行简单数学运算的模板函数

`<functional>`定义了一些模板类,用以声明函数对象

## 1.常用遍历算法

for_each //遍历容器

transform //搬运容器到另一个容器中

### for_each:

```c++
//普通函数
void print01(int val)
{
	cout << val << " ";
}
//仿函数
class print02
{
public:
	void operator()(int val)
	{
		cout << val << " ";
	}
};
void test01()
{
	vector<int>v;
	for (int i = 0; i < 10; i++)
	{
		v.push_back(i);
	}
	for_each(v.begin(), v.end(), print01);
	cout << endl;
	for_each(v.begin(), v.end(), print02());
}
```

### transform:

transform(iterator beg1,iterator end1,iterator beg2, _func_);

//beg1 源容器开始迭代器

//end1 源容器结束迭代器

//beg2 目标容器开始迭代器

//_func 函数或者函数对象

```c++
class myprint
{
public:
	void operator()(int v)
	{
		cout << v << " ";
	}
};
class Transform
{
public:
	int operator()(int v)
	{
		return v*2;
	}
};
void test01()
{
	vector<int>v;
	for (int i = 0; i < 10; i++)
	{
		v.push_back(i);
	}
	cout << v.size() << endl;
	vector<int>vTarget;//目标容器
	vTarget.resize(v.size());//不能用reserve，reserve只改变容量不申请内存
	transform(v.begin(), v.end(), vTarget.begin(), Transform());
	for_each(vTarget.begin(), vTarget.end(), myprint());
	cout << endl;
}
```

## 2.常用查找算法

 find //查找元素

find_if //按条件查找元素

adjacent_find //查找相邻重复元素

binary_search //二分查找法

count //统计元素个数

count_if //按条件统计元素个数

### find

```c++
//常用查找算法
//find
class Person
{
public:
    bool operator==(Person a)
    {
        return (a.age==age)&&(a.name==name);
    }
    Person(string namea,int agea):name(namea),age(agea)
    {

    }
    string name;
    int age;

};
//查找 内置数据类型
void test01()
{
    vector`<int>`v;
    for(int i=0;i<10;i++)
    {
        v.push_back(i);
    }
    //查找容器中是否有5这个元素
    vector`<int>`::iterator it=find(v.begin(),v.end(),5);
    cout<<*it<<endl;
}
//查找 自定义数据类型
void test02()
{
    vector`<Person>`v;
    Person p1("aaa",10);
    v.push_back(p1);
    v.push_back(Person("bbb",20));
    v.push_back(Person("ccc",30));
    v.push_back(Person("ddd",10));
    v.push_back(Person("eee",40));
    vector`<Person>`::iterator it=find(v.begin(),v.end(),p1);
    cout<<(*it).name<<(*it).age<<endl;
}`
```
