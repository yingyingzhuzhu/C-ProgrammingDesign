# C++程序设计 WEEK 4 运算符重载

## 第一课---运算符重载的基本概念

优点：对抽象数据类型也能够直接使用C++提供的运算符，扩展C++中提供的运算符的适用范围, 以用于类所表示的抽象数据类型。程序简洁，易于理解。

运算符重载 即 函数重载

返回值类型 operator 运算符（形参表）
{
	……
}

__运算符重载为普通函数:__

• 重载为普通函数时, 参数个数为运算符目数

```cpp
class Complex {
public:
	Complex( double r = 0.0, double i= 0.0 ){
	 	real = r;
	 	imaginary = i;
	}
	double real; // real part
	double imaginary; // imaginary part
};

Complex operator+ (const Complex & a, const Complex & b)
{
 	return Complex( a.real+b.real, a.imaginary+b.imaginary);
} // “类名(参数表)” 就代表一个对象
```

__运算符重载为成员函数:__

• 重载为成员函数时, 参数个数为运算符目数减一

```cpp
class Complex {
public:
	Complex( double r= 0.0, double m = 0.0 ):
	 real(r), imaginary(m) { } // constructor
	Complex operator+ ( const Complex & ); // addition
	Complex operator- ( const Complex & ); // subtraction
	private:
	double real; // real part
	double imaginary; // imaginary part
};

// Overloaded addition operator
Complex Complex::operator+(const Complex & operand2) {
	return Complex( real + operand2.real, imaginary + operand2.imaginary );
}

// Overloaded subtraction operator
Complex Complex::operator- (const Complex & operand2){
	return Complex( real - operand2.real, imaginary - operand2.imaginary );
}
int main(){
	 Complex x, y(4.3, 8.2), z(3.3, 1.1);
	 x = y + z; // x = y.operator+(z);
	 x = y - z; // x = y.operator-(z);
	 return 0;
} 
```

## 第一课---赋值运算符的重载

只能重载为成员函数！

__重载赋值运算符的意义 – 浅复制和深复制:__


S1 = S2;
__浅复制/浅拷贝__

• 执行逐个字节的复制工作

• 指向同一个地址

可怕的后果：1. S1指向的原内存成为垃圾内存；2. 同一内存释放2次 error。

__深复制/深拷贝__

• 将一个对象中指针变量指向的内容, 复制到另一个对象中指针成员对象指向的地方

```cpp
// 在 class MyString 里添加成员函数:
String & operator = (const String & s) {
	if(str == s.str) return * this;
	if(str) delete [] str;
	if(s.str) { //s.str不为NULL才会执行拷贝
		str = new char[strlen(s.str)+1];
		strcpy(str, s.str);
	}
	else
		str = NULL;
	return * this;
}
```
