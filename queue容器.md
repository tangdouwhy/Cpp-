queue容器是一种先进先出的数据结构,它有两个出口

## 常用接口:

### 构造函数:

queue<T> que;//queue采用模板类实现,queue对象的默认构造形式

queue(const queue &que);//拷贝构造函数

### 赋值操作:

queue& operator=(const queue &que);//重载等号操作符

### 数据存取:

push(elem);//往队尾添加元素

pop();//从队头移除第一个元素

back();//返回最后一个元素

front();//返回第一个元素

### 大小操作:

empty();//判断队列是否为空

size();//返回队列的大小

```c++
class Person
{
public:
	Person(string name, int age) :m_name(name),m_age(age)
	{

	}
	string m_name;
	int m_age;
};
void test01()
{
	//queue是一种先进先出的数据结构,有两个出口
	//queue不允许有遍历行为
	queue<Person>q,q1;
	//入队push 出队pop
	//队头front 队尾back
	//只能看到队头队尾
	//empty size
	q.push(Person("唐僧",30));
	q.push(Person("孙悟空",1000));
	q.push(Person("猪八戒",900));
	q.push(Person("沙僧",800));
	q1 = q;
	cout << "q1的大小: " << q1.size() << endl;
	cout << "q1的队尾: " << q1.back().m_name << " " << q1.back().m_age << endl;
	cout << "q1的队头: " << q1.front().m_name << " " << q1.front().m_age << endl;
	//出队
	q1.pop();
	cout << "q1的队头: " << q1.front().m_name << " " << q1.front().m_age << endl;
	cout << "q1的大小: " << q1.size() << endl;
}
```

