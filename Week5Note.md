# C++程序设计 WEEK 5  继承与派生

## 第一课

__继承和派生__

```cpp
class A{
	
};

class B:public A{
	

};
```

__复合关系和继承关系__

继承关系：“是”

复合关系：“有”，class C中有member variable是class D的object，则class C和class D是复合关系

```cpp
class CPoint{
	int x;
	int y;
};
class CCircle{
	double r;
	CPoint p;
};
```

## 第一课

__基类、派生类同名成员和protected访问范围__

基类的private成员，只能被基类的成员函数和友元函数访问，不能被派生类的成员函数访问。

__派生类的构造函数__

```cpp
class Skill{
	public:
		Skill(int skills);
	private:
		int ns;
};

class Bug{
	public:
		Bug(int color, int legs);
	private:
		int ncolor;
		int nlegs;
};

class FlyBug{
	public:
		FlyBug(int color, int legs, int skills, int wings);
	private:
		int nwings;
		Skill skills;
};

Flybug::FlyBug(int color, int legs, int skills, int wings):Bug(color, legs),Skill(skills),nwings(wings){
	//基类构造 -> 成员对象类构造 -> 派生类构造
}
```

__public继承的赋值兼容规则__

```cpp
Bug b;
Flybug f;

b = f;
b& br = f;
b* pb = &f;
```












