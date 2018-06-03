第二课---位运算

优点：程序计算速度快

左移运算符：<<
1. 左移后，原值不改变

e.g. a<<b, a左移b位，a值不改变。

2. 移除的位丢弃

3. 符号位不改变

右移运算符：>>

1. 如果不能整除，则计算结果往小里取整


第二课---引用

void swap(int &a, int &b){
	int temp = a;
	a = b;
	b = temp;
}
int n1=2;
int n2=3;
swap(n1,n2);

【常引用】
不能通过常引用修改变量值，并非变量值不能修改。不能把常引用赋值给非常引用。
int n = 100;
const int &r = n;
r = 200;//编译错误
n = 300;//编译正确


第三课---动态内存分配

1. 
e.g.
```cpp
int * pn;
pn = new int;//动态分配出一片大小为sizeof(int)的内存空间，并把起始地址赋给pn
* pn = 5;
```

2. P = new T[N];//分配长度为N的数组，内存空间为N*sizeof(T)

e.g.
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

e.g.
```cpp
int * p = new int;
* p = 5;
delete p;
delete p; //异常，一片空间不能被delete多次！
```

e.g. delete array
```cpp
int * p = new int[20];
p[0] = 1;
delete [] p;
```
第三课---内联函数和重载函数







