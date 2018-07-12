# C++程序设计 WEEK 3 类和对象

```cpp
class CRectangle{
	public: //缺省默认是private
		int w, h;
		void Init(int w_, int h_){
			w = w_; h = h_;
		}
		int Area(){
			return w * h;
		}
		int Perimeter(){
			return 2* (w + h);
		}
}; //必须有分号，与Java不同

CRectangle r;
r.Init(3, 2);
cout << r.Area() << endl << r.Perimeter();

```


## 第一课---内联成员函数和重载成员函数

__内联成员函数__

第1种：class里对函数定义使用关键字: "inline"，函数体在class外写

```cpp
class B{
	inline void func1();
};

void B::func1(){}
```
第2种：函数体直接写在class里(与Week2讲的普通内联函数不太一样)

```cpp
class B{
	void func2(){
		...
	}; //定义内联成员函数时，有分号？
};
```


__重载成员函数__

注意：使用缺省参数要避免有函数重载时的二义性！

```cpp
class Location{
	private:
		int x,y;
	public:
		void init(int x=0,int y=0);
		void valueX(int val=0){x=val;}
		int valueX(){return x;}
};

Location A;
A.valueX(); //Error! 编译器无法判断调用哪个valueX: (1)value=0 缺省参数; (2)无参数valueX
```

## 第一课---构造函数

没有返回值，void也不行。

类一定有构造函数。

默认构造函数无参数，不做任何参数。

定义构造函数后，不再生成默认构造函数。

```cpp
class Complex {
	private:
		double real, imag;
	public:
		Complex(double r, double i = 0);
};

Complex c1; // error, 缺少构造函数的参数
Complex* pc = new Complex; // error, 没有参数
Complex c1(2); // OK, 不同于Java，不一定要new一个对象
Complex c1(1,4), c2(3,5); // OK
Complex* pc = new Complex(3,4); // OK
```

对象生成时调用构造函数。

一个类有多个构造函数，调用时依参数而定。

优点：避免没有初始化对象就使用，导致程序出错。

__构造函数在数组中的使用__

```cpp
class Test{
	public:
		Test(int n){} // (1)
		Test(int n, int m){} // (2)
		Test(){} // (3)
};

Test array1[3]={1, Test(1,2)}; // 三个元素分别用(1)(2)(3)初始化。不用new Test(1,2)？
Test array2[3]={Test(2,3),Test(1,2),1}; // 三个元素分别用(2)(2)(1)
Test* pArray[3]={new Test(4),new Test(1,2)};// 前两个元素分别用(1)(2)初始化。与array1[3]不同，pArray是指针数组，不必须初始化对象！

```

## 第二课---copy constructor 复制(拷贝)构造函数

只有一个参数，即对同类对象的引用：
X::X(X&)或X::X(const X &)

不允许这样的形式：X::X(X)
```cpp
class CSample{
	CSample(CSample c){
		// error, 参数不对
	}
	CSample(CSample & c){
		// correct
	}
};
```


如果没有定义，则编译器生成默认复制构造函数，完成复制功能。

```cpp
class Complex{
	private:
		double real, imag;
};

Complex c1;// 调用缺省的无参构造函数
Complex c2(c1); // 调用缺省的复制构造函数
```

定义复制构造函数后，不再生成默认的复制构造函数。

(1)用一个对象去初始化同类的另一个对象时：
```cpp
Complex c2(c1);
Complex c2=c1; // 初始化语句，而非赋值语句
c2=c1; // 赋值语句
```

(2)如果某函数有一个参数是类A的对象，那么该函数被调用时，类A的复制构造函数将被调用，用来初始化形参。

(3)如果函数的返回值是类A的对象，则函数返回时，A的复制构造函数被调用，用来初始化返回值类A的对象。


## 第二课---类型转换构造函数

只有一个参数

```cpp
class Complex{
	public:
		double real, imag;
		Complex(int i){ // 类型转换构造函数
			real=i; imag=0;
		}
		Complex(double r, double i){
			real=r; imag=i;
		}
};
Complex c1(7,8);
Complex c2=12; // 不是赋值语句，虽然调用类型转换构造函数，但是不会生成临时Complex对象
c1=9; // 9被自动转换成一个临时Complex对象
```

## 第二课---析构函数

没有参数和返回值

一个类最多只有一个析构函数

名字与类名相同，在前面加“~”

对象消亡时，自动被调用，释放分配的空间等

__析构函数和数组__

对象数组生命期结束时，对象数组的每个元素的析构函数都会被调用，即调用数组长度次析构函数。

```cpp
Ctest * pTest;
pTest = new Ctest[3]; // 构造函数调用3次
delete [] pTest; // 析构函数调用3次
```

__析构函数和运算符delete__

delete运算导致析构函数调用

```cpp
Ctest* pTest;
pTest = new Ctest; // 构造函数被调用
delete pTest; // 析构函数被调用
```

## 第三课---静态成员变量和静态成员函数

无需通过对象来访问，本质上是全局变量/全局函数。

__静态成员变量__：加了关键字“static”

普通成员变量每个对象有各自的一份，而静态成员变量一共就一份，为所有对象共享。

sizeof(类) 不会计算静态成员变量的大小

__静态成员函数__：

__访问方式：__

```cpp
class CRectangle{
	private:
		int w, h;
		static int nTotalArea;
		static int nTotalNumber;
	public:
		CRectangle(int w_, int h_); // 构造函数
		CRectangle(CRectangle & r); // 复制构造函数
		~CRectangle(); // 析构函数
		static void PrintTotal();
};

CRectangle::CRectangle(int w_, int h_){
	w = w_;
	h = h_;
	nTotalNumber ++;
	nTotalArea += w * h;
}
CRectangle::CRectangle(CRectangle & r){
	w=r.w; h=r.h;
	nTotalNumber ++;
	nTotalArea += w * h;
}
CRectangle::~CRectangle(){
	nTotalNumber --;
	nTotalArea -= w * h;
}
void CRectangle::PrintTotal(){
	cout<<nTotalNumber<<","<<nTotalArea<<endl;
}
//必须在定义类的文件中对静态成员变量进行一次说明或初始化，否则编译能过，链接过不了。
int CRectangle::nTotalNumber = 0;
int CRectangle::nTotalArea = 0;
```

(1)类名::成员名
```cpp
CRectangle::PrintTotal();
```

(2)对象名.成员名
```cpp
CRectangle r; r.PrintTotal();
```
(3)指针->成员名
```cpp
CRectangle* p = &r; p->PrintTotal();
```

(4)引用.成员名
```cpp
CRectangle& ref = r; int n=ref.nTotalNumber;
```

Attention: 在静态成员函数中，不能访问非静态成员变量，也不能调用非静态成员函数。

## 第三课---成员对象和封闭类Enclosing

__成员对象：__一个类的成员变量是另一个类的对象。

__封闭类Enclosing：__包含成员对象的类叫封闭类Enclosing

```cpp
class CTyre{ // 轮胎类
	private:
		int radius;
		int width;
	public:
		CTyre(int r, int w):radius(r), width(w){} // 构造函数，不使用赋值语句的写法,使用初始化列表。
};

class CEngine{}; // 引擎类

class CCar{ // 汽车类，封闭类
	private:
		int price;
		CTyre tyre;
		CEngine engine;
	public:
		CCar(int p, int tr, int tw);
};
CCar::CCar(int p, int tr, int w):price(p),tyre(tr,w){

};

int main(){
	CCar car(20000,17,225);
	return 0;
}
```

__调用顺序：__

当封闭类对象生成时：

step 1：执行所有__成员对象__的构造函数

step 2： 执行__封闭类__的构造函数

成员对象的构造函数调用顺序：

与成员对象在类中说明顺序一致，与初始化列表顺序无关

当封闭类的对象消亡时：

先生成的后析构


## 第四课---友元Friend

__友元函数__

一个类的友元函数可以访问该类的私有成员。

__友元类__

A是B的友元类 -> A的成员函数可以访问B的私有成员。

不能传递，不能继承

```cpp
class CCar{
	private:
		int price;
	friend class CDriver; // 声明CDriver为友元类
};

class CDriver{
	public:
		CCar myCar;
		void ModifyCar(){
			myCar.price += 1000; // CDriver是CCar的友元类，可以访问其私有成员price
		}
};
```

## 第四课---this指针

```cpp
class A{
    int i;
public:
    void printHello(){
        cout<<"hello"<<endl;
    }
    void printiHello(){
        cout<<i<<"hello"<<endl;
    }
};
int main() {
    A* p = NULL; // 空指针，this为NULL
    p->printHello(); // output: hello
    p->printiHello(); // Error
    return 0;
}
```

__this指针与静态成员函数__：

不能使用this指针，因为静态成员函数并不具体作用于某个对象。


## 常量对象、常量成员函数和常引用

__关键字：const__

__常量成员函数：__

```cpp
class Sample{
public:
	int value;
	void GetValue() const; // 常量成员函数
	void func(){};
};
void Sample::GetValue() const{
	value=0; // error，不能修改成员变量的值
	func(); // error，不能调用非常量成员函数
}
```


__常量对象：__

```cpp
int main(){
	const Sample o; // 常量对象
	o.vlaue = 100; // error, 常量对象不可被修改
	o.func(); // error, 常量对象上面不能执行非常量成员函数
	o.GetValue(); // ok, 常量对象上可以执行常量成员函数
	return 0;
}
```

__常量成员函数的重载:__

两个成员函数，名字和参数表都一样，但是一个是const，一个不是，算重载。

__常引用：__

引用前面可以加const关键字，成为常引用。不能通过常引用，修改其引用的变量。

优点：对象作为函数的参数时，生成该参数需要调用复制构造函数，效率比较低。用指针作参数，代码又不好看。

```cpp
class Sample {
…
};
void PrintfObj(const Sample& o)
{
……
} 
```

