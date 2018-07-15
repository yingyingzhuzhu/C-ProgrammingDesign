# C++程序设计 WEEK 5 

## 第一课

_继承和派生_

```cpp
class A{
	
};

class B:public A{
	

};
```

_复合关系和继承关系_

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











