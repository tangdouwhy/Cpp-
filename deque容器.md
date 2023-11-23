## 基本概念:

功能:双端数组,可以对头端进行插入删除操作

### deque和vector的区别:

vector对于头部的插入和删除效率低,数据量越大效率越低

deque相对而言,对头部的插入删除速度会比vector快

vector访问元素时的速度会比deque快,这和两者内部实现有关

### deque内部工作原理:

deque内部有个中控器,维护每段缓冲区中的内容,缓冲区中存放真实数据

中控器维护的是每个缓冲区的地址,使得使用deque时像一片连续的内存空间

## 赋值操作:

deque& operator=(const deque &deq);//重载等号操作符

assign(beg,end);//将[beg，end)区间中的数据拷贝赋值给本身,左闭右开

assign(n,elem);//将n个elem拷贝赋值给本身

```c++
    void print(const deque<int>& d)
    {
        for (deque<int>::const_iterator it = d.begin(); it != d.end(); it++)
        {
            cout << *it << " ";
        }
        cout << endl;
	}
	deque<int>d1;
	for (int i = 0; i < 10; i++)
	{
		d1.push_back(i);
	}
	print(d1);
	//等号赋值
	deque<int>d2;
	d2 = d1;
	print(d2);
	//assign赋值
	deque<int>d3;
	d3.assign(d1.begin(), d1.end());
	print(d3);
	deque<int>d4;
	d4.assign(10, 100);
	print(d4);
```

## 大小操作:

deque.empty();//判断容器是否为空

deque.size();//返回容器中元素的个数

deque.resize(num);//重新指定容器的长度为num,若容器变长,则以默认值填充新位置

//如果容器变短,则末尾超出容器长度部分的元素被删除

deque.resize(num,elem);//重新指定容器的长度为num,若容器变长,则以elem值填充新位置

//如果容器变短,则末尾超出容器长度部分的元素被删除

```c++
    void print(const deque<int>& d)
    {
        for (deque<int>::const_iterator it = d.begin(); it != d.end(); it++)
        {
            cout << *it << " ";
        }
        cout << endl;
    }
	deque<int>d1;
	for (int i = 0; i < 10; i++)
	{
		d1.push_back(i);
	}
	print(d1);
	//deque没有容量,只有元素个数
	cout << "deque的大小" << d1.size() << endl;
	cout << "deque是否为空" << d1.empty() << endl;
	//deque重新指定大小
	d1.resize(5);
	print(d1);
	//第二个参数为如果空间变大填入的数
	d1.resize(10, 100);
	print(d1);
```

## 插入和删除:

```c++
void print(const deque<int>& d)
{
	for (deque<int>::const_iterator it = d.begin(); it != d.end(); it++)
	{
		cout << *it << " ";
	}
	cout << endl;
}
```

push_back(elem);//在容器尾部添加一个数据

push_front(elem);//在容器头部插入一个数据

pop_back();//删除容器最后一个数据

pop_front();//删除容器第一个数据

```c++
deque<int>d1;
//尾插
d1.push_back(10);
d1.push_back(100);
//头插
d1.push_front(200);
d1.push_front(20);
print(d1);
//尾删
d1.pop_back();
print(d1);
//头删
d1.pop_front();
print(d1);
```

insert(pos,elem);//在pos位置插入一个elem元素的拷贝,返回新数据的位置

insert(pos,n,elem);//在pos位置插入n个elem数据,无返回值

insert(pos,beg,end);//在pos位置插入[beg,end)区间的数据,无返回值

```c++
deque<int>d1,d2;
d2.push_back(1);
d2.push_back(2);
d2.push_back(3);
d1.push_back(10);
d1.push_back(20);
d1.push_front(100);
d1.push_front(200);
print(d1);
//insert插入
d1.insert(d1.begin() + 1, 2000);
print(d1);
d1.insert(d1.begin(), 2, 10000);//两个一万
print(d1);
d1.insert(d1.begin(), d2.begin(), d2.end());//在头部插一个区间
print(d1);
```

clear();//清空容器的所有数据

erase(beg,end);//删除[beg,end)区间的数据，返回下一个数据的位置

erase(pos);//删除pos位置的数据,返回下一个数据的位置

```c++
//deque删除
deque<int>d1;
d1.push_back(10);
d1.push_back(20);
d1.push_front(100);
d1.push_front(200);
print(d1);
d1.erase(d1.begin()+1);
print(d1);
d1.erase(d1.begin() + 1, d1.end());//左闭右开区间删除
print(d1);
d1.clear();
if (d1.empty() == true)
{
	cout << "d1为空" << endl;
}
```

## 数据存取:

at(int idx);//返回索引idx所指的数据

operator[];//返回索引idx所指的数据

front();//返回容器中第一个数据元素

back();//返回容器中最后一个元素

```c++
void print(const deque<int>& d)
{
	for (deque<int>::const_iterator it = d.begin(); it != d.end(); it++)
	{
		cout << *it << " ";
	}
	cout << endl;
}
deque<int>d1;
d1.push_back(10);
d1.push_back(100);
d1.push_back(20);
d1.push_back(30);
d1.push_front(100);
d1.push_front(200);
for (int i = 0; i < d1.size(); i++)
{
	//通过中括号方式
	cout << d1[i] << " ";
}
cout << endl;
//通过at的方式
for (int i = 0; i < d1.size(); i++)
{
	cout << d1.at(i) << " ";
}
cout << endl;
cout << "第一个元素为: " << d1.front() << endl;
cout << "最后一个元素为: " << d1.back() << endl;
```

## 排序操作:

sort(iterator beg,iterator end);//对beg和end区间内元素进行排序

```c++
void print(const deque<int>& d)
{
	for (deque<int>::const_iterator it = d.begin(); it != d.end(); it++)
	{
		cout << *it << " ";
	}
	cout << endl;
}
void test01()
{
	deque<int>d1;
	d1.push_back(100);
	d1.push_back(1000);
	d1.push_back(20);
	print(d1);
	sort(d1.begin(), d1.end());//随机访问迭代器均支持sort排序
	print(d1);
}
```

