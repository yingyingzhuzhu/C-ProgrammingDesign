# C++程序设计 WEEK 2

## 第二课---位运算

优点：程序计算速度快

__左移运算符：<<__
1. 左移后，原值不改变

e.g. a<<b, a左移b位，a值不改变。

2. 移除的位丢弃

3. 符号位不改变

__右移运算符：>>__

1. 如果不能整除，则计算结果往小里取整


## 第二课---引用

```cpp
void swap(int &a, int &b){
	int temp = a;
	a = b;
	b = temp;
}
int n1=2;
int n2=3;
swap(n1,n2);
```

__常引用__

不能通过常引用修改变量值，并非变量值不能修改。不能把常引用赋值给非常引用。
```cpp
int n = 100;
const int &r = n;
r = 200;//编译错误
n = 300;//编译正确
```

## 第三课---动态内存分配

1. P = new T;
```cpp
int * pn;
pn = new int;//动态分配出一片大小为sizeof(int)的内存空间，并把起始地址赋给pn
* pn = 5;
```

2. P = new T[N]; //分配长度为N的数组，内存空间为N*sizeof(T)

```cpp
int * pn;
int i = 5;
pn = new int[i * 20]; // 数组长度为100
pn[0] = 20;
```
```cpp
new T; //返回值类型是T *(指针)。
new T[n]; //返回值类型是T *(指针)。
```

3. 用“delete”运算符释放动态分配的内存空间

```cpp
int * p = new int;
* p = 5;
delete p;
delete p; //异常，一片空间不能被delete多次！
```

delete array
```cpp
int * p = new int[20];
p[0] = 1;
delete [] p;
```

## 第三课---内联函数和重载函数

__内联函数__

关键字：“__inline__”

优点：为了减少函数调用的时间开销，引入内联函数机制。编译器将函数代码插入到调用函数的地方。

缺点：函数代码体积增大。

```cpp
inline int Max(int a, int b){
	if(a > b){
		return a;
	}
	return b;
}
```

__重载函数__

一个或多个函数，函数名相同，函数参数个数或参数类型不同。

优点：函数命名简单


## 第三课---函数缺省参数

优点：提升程序的可扩充性

```cpp
void func(int n1, int n2 = 5, int n3 = 10){}

func(2); // 相当于func(2,5,10)
func(2,7); // 相当于func(2,7,10)
func(2,,12); // error
```

比如：画图，缺省参数颜色是黑色



## 第四课---面向对象程序设计方法





