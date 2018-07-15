# C++程序设计 Week6 多态与虚函数

## 第一课

__基本概念__

__虚函数：__ 在类的定义中，前面有_virtual_关键字的成员函数是_虚函数_

```cpp
class base{
	virtual int get();
};

int base::get(){}
```

__Note: __

1. virtual关键字只用在类定义里的函数声明中，写函数体时不用

2. 构造函数和静态成员函数不能是虚函数


__多态：__ 

```cpp
class Base{
	public:
		virtual int get();
};

class Derived:public base{
	public:
		virtual int get(); // 同名虚函数
};

Derived obj;
Base* p = &obj;
p -> get(); // 调用derived的get(), 因为调用哪个虚函数取决于p指向哪种类型的对象

Base& r = obj;
r.get(); // 调用derived的get(), 因为调用哪个虚函数取决于r是哪种类型的对象的引用
```

## 第三课

__多态实现原理：__

__虚函数表__

每个拥有虚函数的类中都存放着一个虚函数表的地址（4 byte），虚函数表中存放该类的虚函数的地址。

代价：程序运行时额外的时间、空间开销


__虚析构函数：__

拥有虚函数的类的析构函数也必须是虚函数


__纯虚函数：__ 

没有函数体的虚函数

```cpp
class Base{
	public:
		virtual int get() = 0;
};
```

构造函数和析构函数中不能调用纯虚构函数，其他成员函数可以

包含纯虚函数的类 -> __抽象类__

不能创建抽象类的对象





