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

没有返回值，void也不行
类一定有构造函数。
默认构造函数无参数，不做任何参数。
定义构造函数后，不再生成默认构造函数。
对象生成时调用构造函数。
一个类有多个构造函数，调用时依参数而定。

优点：避免没有初始化对象就使用，导致程序出错。



