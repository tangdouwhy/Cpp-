stack容器是一种先进后出的数据结构,他只有一个出口

栈中只有顶端的元素才可以被外界使用,因此栈不允许有遍历行为

## 常用接口:

### 构造函数:

stack<T>stk;//stack采用模板类实现,stack对象的默认构造形式

stack(const stack &stk);//拷贝构造函数

### 赋值操作:

stack& operator=(const stack &stk);//重载等号操作符

### 数据存取:

push(elem);//向栈顶添加元素

pop();//从栈顶移除第一个元素

top();//返回栈顶元素

### 大小操作:

empty();//判断堆栈是否为空

size();//返回栈的大小

```c++
//栈不允许有遍历行为
//栈可以判断是否为空 empty
//栈可以返回元素个数 size 是在入栈的时候统计的
//构造只有默认构造和拷贝构造
void test01()
{
	stack<int> s;
	//特点：先进后出的数据结构
	//入栈操作
	s.push(10);
	s.push(20);
	cout << "s的大小: " << s.size() << endl;
	//只要栈不为空就，查看栈顶，并且执行出栈操作
	while (!s.empty())
	{
		cout << s.top() << " ";
		s.pop();
	}
	cout << endl;
	cout << "s的大小: " << s.size();
	s.push(10);
	s.push(20);
}
```

