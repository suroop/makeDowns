## 继承

- 继承与派生是同一过程从不同的角度来看
  - 保持已有类的特性而构造新类的过程称为继承。
  - 在已有类的基础上新增自己的特性而产生新类的过程称为派生
- 被继承的已有类称为基类（或父类）。
- 派生出的新类称为派生类。
- 直接参与派生出某类的基类称为直接基类，基类的基类甚至更高层的基类称为间接基类。

### 单继承时

```c++
class 派生类名：继承方式  基类名
{
  //  成员声明；
}
//例如：
class Derived: public Base1, private Base2
{
public:
	Derived ();
	~Derived ();
};

```

### 多继承时

```c++
class 派生类名：继承方式1  基类名1，继承方式2  基类名2，...
{
//	成员声明；
}

```

### 派生类生成过程

+ 吸收基类成员
  + 吸收基类成员之后，派生类实际上就包含了它的全部基类中除构造和析构函数之外的所有成员
+ 改造基类成员
  + 如果派生类声明了一个和某基类成员同名的新成员（如果是成员函数，则参数表也要相同，参数不同的情况属于重载），派生的新成员就覆盖了外层同名成员
+ 添加新的成员
  + 派生类新成员的加入是继承与派生机制的核心，是保证派生类在功能上有所发展

### 访问控制

+ 三种继承方式
  + 公有继承
  + 私有继承
  + 保护继承

+ 不同继承方式的影响主要体现在：
  + 派生类成员对基类成员的访问权限
  + 通过派生类对象对基类成员的访问权限

### 公有继承

+ 基类的public和protected成员的访问属性在派生类中保持不变，但基类的private成员不可直接访问。

+ 派生类中的成员函数可以直接访问基类中的public和protected成员，但不能直接访问基类的private成员。
+ 通过派生类的对象只能访问基类的public成员。

```c++
#ifndef _POINT_H
#define _POINT_H
class Point {	//基类Point类的定义
public:		//公有函数成员
	void initPoint(float x = 0, float y = 0)
  { this->x = x; this->y = y;}
	void move(float offX, float offY)
  { x += offX; y += offY; }
	float getX() const { return x; }
	float getY() const { return y; }
private:		//私有数据成员
	float x, y;
};
#endif //_POINT_H


#ifndef _RECTANGLE_H
#define _RECTANGLE_H
#include "Point.h"
class Rectangle: public Point {	//派生类定义部分
public:	//新增公有函数成员
	void initRectangle(float x, float y, float w, float h) {
		initPoint(x, y); //调用基类公有成员函数
		this->w = w;
		this->h = h;
	}
	float getH() const { return h; }
	float getW() const { return w; }
private:	//新增私有数据成员
	float w, h;
};
#endif //_RECTANGLE_H
#include <iostream>
#include <cmath>
using namespace std;
int main() {
	Rectangle rect;	//定义Rectangle类的对象
	//设置矩形的数据
	rect.initRectangle(2, 3, 20, 10);	
	rect.move(3,2);	//移动矩形位置
	cout << "The data of rect(x,y,w,h): " << endl;
	//输出矩形的特征参数
	cout << rect.getX() <<", "
		<< rect.getY() << ", "
		<< rect.getW() << ", "
		<< rect.getH() << endl;
	return 0;
}

```

### 私有继承

+ 基类的public和protected成员都以private身份出现在派生类中，但基类的private成员不可直接访问。

+ 派生类中的成员函数可以直接访问基类中的public和protected成员，但不能直接访问基类的private成员。

+ 通过派生类的对象不能直接访问基类中的任何成员。

```C++
#ifndef _POINT_H
#define _POINT_H
class Point {	//基类Point类的定义
public:	//公有函数成员
	void initPoint(float x = 0, float y = 0) 
  { this->x = x; this->y = y;}
	void move(float offX, float offY) 
  { x += offX; y += offY; }
	float getX() const { return x; }
	float getY() const { return y; }
private:	//私有数据成员
	float x, y;
};	
#endif //_POINT_H


#ifndef _RECTANGLE_H
#define _RECTANGLE_H
#include "Point.h"
class Rectangle: private Point {	//派生类定义部分
public:	//新增公有函数成员
	void initRectangle(float x, float y, float w, float h) {
		initPoint(x, y); //调用基类公有成员函数
		this->w = w;
		this->h = h;
	}
	void move(float offX, float offY) { 
		Point::move(offX, offY);
	}
	float getX() const { return Point::getX(); }
	float getY() const { return Point::getY(); }
	float getH() const { return h; }
	float getW() const { return w; }
private:	//新增私有数据成员
	float w, h;
};
#endif //_RECTANGLE_H


#include <iostream>
#include <cmath>
using namespace std;

int main() {
	Rectangle rect;	//定义Rectangle类的对象
	rect.initRectangle(2, 3, 20, 10);	//设置矩形的数据
	rect.move(3,2);	//移动矩形位置
	cout << "The data of rect(x,y,w,h): " << endl;
	cout << rect.getX() <<", "	//输出矩形的特征参数
		<< rect.getY() << ", "
		<< rect.getW() << ", "
		<< rect.getH() << endl;
	return 0;
}

```

### 保护继承

- 基类的public和protected成员都以protected身份出现在派生类中，但基类的private成员不可直接访问。

- 派生类中的成员函数可以直接访问基类中的public和protected成员，但不能直接访问基类的private成员。

- 通过派生类的对象不能直接访问基类中的任何成员

> protected &private 区别

+ 对建立其所在类对象的模块来说，它与 private 成员的性质相同。

+ 对于其派生类来说，它与 public 成员的性质相同。

+ 既实现了数据隐藏，又方便继承，实现代码重用

```
class A {
protected:
	int x;
};

int main() {
	A a;
	a.x = 5;    //错误
}
```

```
class A {
protected:
	int x;
};
class B: public A{
public:
	void function();
};
void B:function() {
	x = 5;   //正确
}
```

### 多继承举例

```
class A {
public:
	void setA(int);
	void showA() const;
private:
	int a;
};
class B {
public:
	void setB(int);
	void showB() const;
private:
	int b;
};
class C : public A, private B { 
public:
	void setC(int, int, int);
	void showC() const;
private const:
	int c;
};
void  A::setA(int x) {
	a=x; 
}
void B::setB(int x) {
	b=x; 
}
void C::setC(int x, int y, int z) {
	//派生类成员直接访问基类的
	//公有成员
	setA(x); 
	setB(y); 
	c = z;
}
//其他函数实现略
int main() {
	C obj;
	obj.setA(5);
	obj.showA();
	obj.setC(6,7,9);
	obj.showC();
// obj.setB(6);  错误
// obj.showB(); 错误
	return 0;
}

```



### 类型转换规则

+ 通过基类对象名、指针只能使用从基类继承的成员
+ 一个公有派生类的对象在使用上可以被当作基类的对象，反之则禁止。具体表现在
  + 派生类的对象可以隐含转换为基类对象
  + 派生类的对象可以初始化基类的引用
  + 派生类的指针可以隐含转换为基类的指针

```C++
#include <iostream>
using namespace std;
class Base1 { //基类Base1定义
public:
	void display() const {
		cout << "Base1::display()" << endl;
	}
};
class Base2: public Base1 { //公有派生类Base2定义
public:
	void display() const {
		cout << "Base2::display()" << endl;
	}
};
class Derived: public Base2 { //公有派生类Derived定义
public:
	void display() const {
		cout << "Derived::display()" << endl;
	}
};
void fun(Base1 *ptr) { 	//参数为指向基类对象的指针
	ptr->display();		//"对象指针->成员名"
}
int main() {	//主函数
	Base1 base1;	//声明Base1类对象
	Base2 base2;	//声明Base2类对象
	Derived derived;	//声明Derived类对象

	fun(&base1);	//用Base1对象的指针调用fun函数
	fun(&base2);	//用Base2对象的指针调用fun函数
	fun(&derived);     //用Derived对象的指针调用fun函数

	return 0;
//Base1::display()
//Base1::display()
//Base1::display()

```

### 继承时的构造函数

+ 基类的构造函数不被继承，派生类中需要声明自己的构造函数。

+ 定义构造函数时，只需要对本类中新增成员进行初始化，对继承来的基类成员的初始化，自动调用基类构造函数完成。

+ 派生类的构造函数需要给基类的构造函数传递参数

#### 单一继承时的构造函数

派生类名::派生类名(基类所需的形参，本类成员所需的形参):基类名(参数表), 本类成员初始化列表

{

 //其他初始化；

}；

```C++
#include<iostream>
using namecpace std;
class B {
public:
	B();
	B(int i);
	~B();
	void print() const;
private:
	int b;
};
B::B() {
	b=0;
	cout << "B's default constructor called." << endl;
}
B::B(int i) {
	b=i;
	cout << "B's constructor called." << endl;
}
B::~B() {
	cout << "B's destructor called." << endl;
}
void B::print() const {
	cout << b << endl;
}
class C: public B {
public:
	C();
	C(int i, int j);
	~C();
	void print() const;
private:
	int c;
};
C::C() {
	c = 0;
	cout << "C's default constructor called." << endl;
}
C::C(int i,int j): B(i), c(j){
	cout << "C's constructor called." << endl;
}
C::~C() {
	cout << "C's destructor called." << endl;
}
void C::print() const {
	B::print();
	cout << c << endl;
}

int main() {
	C obj(5, 6);
	obj.print();
	return 0;
}

```

#### 多继承时的构造函数

派生类名::派生类名(参数表):基类名1(基类1初始化参数表), 基类名2(基类2初始化参数表), ...基类名n(基类n初始化参数表), 本类成员初始化列表

{

​    //其他初始化；

}；

+ 当基类中声明有缺省构造函数或未声明构造函数时，派生类构造函数可以不向基类构造函数传递参数，也可以不声明，构造派生类的对象时，基类的缺省构造函数将被调用。

+ 当需要执行基类中带形参的构造函数来初始化基类数据时，派生类构造函数应在初始化列表中为基类构造函数提供参数

#### 多继承且有内嵌对象时的构造函数

派生类名::派生类名(形参表):基类名1(参数), 基类名2(参数), ...基类名n(参数), 本类对象成员和基本类型成员初始化列表

{

​    //其他初始化

}；

#### 构造函数的执行顺序

+ 调用基类构造函数，调用顺序按照它们被继承时声明的顺序（从左向右）。

+ 对本类成员初始化列表中的基本类型成员和对象成员进行初始化，初始化顺序按照它们在类中声明的顺序。对象成员初始化是自动调用对象所属类的构造函数完成的。

+ 执行派生类的构造函数体中的内容

#### demo

```c++
#include <iostream>
using namespace std;
class Base1 {	//基类Base1，构造函数有参数
public:
	Base1(int i) { cout << "Constructing Base1 " << i << endl; }
};
class Base2 {	//基类Base2，构造函数有参数
public:
	Base2(int j) { cout << "Constructing Base2 " << j << endl; }
};
class Base3 {	//基类Base3，构造函数无参数
public:
	Base3() { cout << "Constructing Base3 *" << endl; }
};
class Derived: public Base2, public Base1, public Base3 {
//派生新类Derived，注意基类名的顺序
public:	//派生类的公有成员
	Derived(int a, int b, int c, int d): Base1(a), member2(d), member1(c), Base2(b)
	{ }
	//注意基类名的个数与顺序，//注意成员对象名的个数与顺序
private:	//派生类的私有成员对象
	Base1 member1;
	Base2 member2;
	Base3 member3;
};

int main() {
	Derived obj(1, 2, 3, 4);
	return 0;
}
//constructing Base2 2
//constructing Base1 1
//constructing Base3 *
//constructing Base1 3
//constructing Base2 4
//constructing Base3 *

```

### 复制构造函数

+ 若建立派生类对象时没有编写复制构造函数，编译器会生成一个隐含的复制构造函数，该函数先调用基类的复制构造函数，再为派生类新增的成员对象执行拷贝。
+ 若编写派生类的复制构造函数，则需要为基类相应的复制构造函数传递参数

```C++
C::C(const C &c1): B(c1) {…}
```

### 析构函数

+ 析构函数也不被继承，派生类自行声明

+ 声明方法与一般（无继承关系时）类的析构函数相同。

+ 不需要显式地调用基类的析构函数，系统会自动隐式调用。

+ 析构函数的调用次序与构造函数相反

### demo

```c++
#include <iostream>
using namespace std;
class Base1 {	//基类Base1，构造函数有参数
public:
	Base1(int i) { cout << "Constructing Base1 " << i << endl; }
	~Base1() { cout << "Destructing Base1" << endl; }
};

class Base2 {	//基类Base2，构造函数有参数
public:
	Base2(int j) { cout << "Constructing Base2 " << j << endl; }
	~Base2() { cout << "Destructing Base2" << endl; }
};

class Base3 {	//基类Base3，构造函数无参数
public:
	Base3() { cout << "Constructing Base3 *" << endl; }
	~Base3() { cout << "Destructing Base3" << endl; }
};
class Derived: public Base2, public Base1, public Base3 {
//派生新类Derived，注意基类名的顺序
public:	//派生类的公有成员
	Derived(int a, int b, int c, int d): Base1(a), member2(d), member1(c), Base2(b) { }
	//注意基类名的个数与顺序，注意成员对象名的个数与顺序
private:	//派生类的私有成员对象
	Base1 member1;
	Base2 member2;
	Base3 member3;
};

int main() {
	Derived obj(1, 2, 3, 4);
	return 0;
}
//Constructing Base2 2
//Constructing Base1 1
//Constructing Base3 *
//Constructing Base1 3
//Constructing Base2 4
//Constructing Base3 *
//Destructing Base3
//Destructing Base2
//Destructing Base1
//Destructing Base3
//Destructing Base1
//Destructing Base2

```

### 作用域限定

当派生类与基类中有相同成员时：

+ 若未特别限定，则通过派生类对象使用的是派生类中的同名成员。

+ 如要通过派生类对象访问基类中被隐藏的同名成员，应使用基类名和作用域操作符（::）来限定

```
#include <iostream>
using namespace std;
class Base1 {	//定义基类Base1
public:
	int var;
	void fun() { cout << "Member of Base1" << endl; }
};
class Base2 {	//定义基类Base2
public:
	int var;
	void fun() { cout << "Member of Base2" << endl; }
};
class Derived: public Base1, public Base2 { //定义派生类Derived
public:
	int var;	//同名数据成员
	void fun() { cout << "Member of Derived" << endl; }	//同名函数成员
};
int main() {
	Derived d;
	Derived *p = &d;

	d.var = 1;	//对象名.成员名标识
	d.fun();	//访问Derived类成员
	
	d.Base1::var = 2;	//作用域操作符标识
	d.Base1::fun();	//访问Base1基类成员
	
	p->Base2::var = 3;	//作用域操作符标识
	p->Base2::fun();	//访问Base2基类成员

	return 0;
}

```

### 虚基类

+ 虚基类的引入
  + 用于有共同基类的场合

+ 声明
  + 以virtual修饰说明基类

+ 作用
  + 主要用来解决多继承时可能发生的对同一基类继承多次而产生的二义性问题
  + 为最远的派生类提供唯一的基类成员，而不重复产生多次拷贝

+ 注意：
  + 在第一级继承时就要将共同基类设计为虚基类

### demo

```C++
#include <iostream>
using namespace std;
class Base0 {	//定义基类Base0
public:
	int var0;
	void fun0() { cout << "Member of Base0" << endl; }
};
class Base1: virtual public Base0 {	//定义派生类Base1
public:	//新增外部接口
	int var1;
};
class Base2: virtual public Base0 {	//定义派生类Base2
public:	//新增外部接口
	int var2;
};
class Derived: public Base1, public Base2 {
//定义派生类Derived 
public:	//新增外部接口
	int var;
	void fun() {
		cout << "Member of Derived" << endl;
	}
};

int main() {	  //程序主函数
	Derived d;	  //定义Derived类对象d
	d.var0 = 2;  //直接访问虚基类的数据成员
	d.fun0();	  //直接访问虚基类的函数成员
	return 0;
}

```

















## 派生类的构成

派生类中的成员包括从基类继承过来的成员和自己增加的成员两大部分。在基类中包括数据成员和成员函数(或称数据与方法)两部分，派生类分为两大部分: 一部分是从基类继承来的成员，另一部分是在声明派生类时增加的部分。每一部分均分别包括数据成员和成员函数。

**在声明派生类时，一般还应当自己定义派生类的构造函数和析构函数，因为构造函数和析构函数是不能从基类继承的**

`note`:在`php`中子类可以继承父类的构造函数

注意以下几个问题:

+ 基类的成员函数访问基类成员。

+ 派生类的成员函数访问派生类自己增加的成员

+ 基类的成员函数访问派生类的成员

+ 派生类的成员函数访问基类的成员

+ 在派生类外访问派生类的成员

+ 在派生类外访问基类的成员

1.第(1)和第(2)种情况基类的成员函数可以访问基类成员，派生类的成员函数可以访问派生类成员。私有数据成员只能被同一类中的成员函数访问，公用成员可以被外界访问

2.第(3)种情况也比较明确，基类的成员函数只能访问基类的成员，而不能访问派生类的成员。第(5)种情况也比较明确，在派生类外可以访问派生类的公用成员，而不能访问派生类的私有成员

**私有基类的公用成员和保护成员在派生类中的访问属性相当于派生类中的私有成员，即派生类的成员函数能访问它们，而在派生类外不能访问它们。私有基类的私有成员在派生类中成为不可访问的成员，只有基类的成员函数可以引用它们。一个基类成员在基类中的访问属性和在派生类中的访问属性可能是不同的**

保护继承的特点是: 保护基类的公用成员和保护成员在派生类中都成了保护成员，其私有成员仍为基类私有。也就是把基类原有的公用成员也保护起来，不让类外任意访问

 在派生类中，成员有4种不同的访问属性:

① 公用的，派生类内和派生类外都可以访问。

② 受保护的，派生类内可以访问，派生类外不能访问，其下一层的派生类可以访问。

③ 私有的，派生类内可以访问，派生类外不能访问。

④ 不可访问的，派生类内和派生类外都不能访问

## **基类与派生类的转换**

**只有公用派生类才是基类真正的子类型，它完整地继承了基类的功能。**

基类与派生类对象之间有赋值兼容关系，由于派生类中包含从基类继承的成员，因此可以将派生类的值赋给基类对象，在用到基类对象的时候可以用其子类对象代替。具体表现在以下几个方面:

1. 派生类对象可以向基类对象赋值

**在赋值时舍弃派生类自己的成员。实际上，所谓赋值只是对数据成员赋值，对成员函数不存在赋值问题**

**应当注意，子类型关系是单向的、不可逆的。B是A的子类型，不能说A是B的子类型。只能用子类对象对其基类对象赋值，而不能用基类对象对其子类对象赋值，理由是显然的，因为基类对象不包含派生类的成员，无法对派生类的成员赋值。同理，同一基类的不同派生类对象之间也不能赋值**

2. 派生类对象可以替代基类对象向基类对象的引用进行赋值或初始化

```
A a1;           //定义基类A对象a1
B b1;                //定义公用派生类B对象b1
A& r1=a1;             //定义基类A对象的引用变量r，并用a1对其初始化
A& r2=b1;//定义基类A对象的引用变量r，并用派生类B对象b1
//对其初始化
```

此时`r`2并不是`b1`的别名，也不与`b`共享同一段存储单元。它只是`b1`中基类部分的别名，`r2`与`b1`中基类部分共享同一段存储单元，r与`b1`具有相同的起始地址

3. 如果函数的参数是基类对象或基类对象的引用，相应的实参可以用子类对象

void fun(A& r)//形参是类A的对象的引用变量

```
 {cout<<r.num<<endl;}      //输出该引用变量的数据成员num
```

函数的形参是类A的对象的引用变量，本来实参应该为A类的对象。由于子类对象与派生类对象赋值兼容，派生类对象能自动转换类型，在调用fun函数时可以用派生类B的对象`b1`作实参:

```
fun(b1);
```

输出类B的对象`b1`的基类数据成员`num`的值

与前相同，在fun函数中只能输出派生类中基类成员的值

4. 派生类对象的地址可以赋给指向基类对象的指针变量，也就是说，指向基类对象的指针变量也可以指向派生类对象

## 运算符重载

不能重载的运算符举例：“.”、“.*”、“::”、“?:”

•两种重载方式：重载为类的非静态成员函数和重载为非成员函数。

### 运算符重载为成员函数

•声明形式

函数类型 operator 运算符（形参）

{

​    ......

}

•重载为类成员函数时 
 参数个数=原操作数个数-1 （后置++、--除外）

•重载为非成员函数时 参数个数=原操作数个数，且至少应该有一个自定义类型的形参。

#### 双目运算符

```
#include <iostream>
using namespace std;
class Complex {	//复数类定义
public:	//外部接口
	Complex(double r = 0.0, double i = 0.0) : real(r), imag(i) { }	//构造函数
	Complex operator + (const Complex &c2) const;	//运算符+重载成员函数
	Complex operator - (const Complex &c2) const;	//运算符-重载成员函数
	void display() const;	//输出复数
private:	//私有数据成员
	double real;	//复数实部
	double imag;	//复数虚部
};
int main() {	//主函数
	Complex c1(5, 4), c2(2, 10), c3;	//定义复数类的对象
	cout << "c1 = "; c1.display();
	cout << "c2 = "; c2.display();
	c3 = c1 - c2;	//使用重载运算符完成复数减法
	cout << "c3 = c1 - c2 = "; c3.display();
	c3 = c1 + c2;	//使用重载运算符完成复数加法
	cout << "c3 = c1 + c2 = "; c3.display();
	return 0;
}

```

#### 前置单目运算符

无形参

```
operator ++ ();
```



#### 后置单目运算符

具有一个 int 类型形参。

```c++
operator ++ (int);
```

#### demo

```C++
#include <iostream>
using namespace std;
class Clock	{	//时钟类定义
public:	//外部接口
	Clock(int hour = 0, int minute = 0, int second = 0);
	void showTime() const;
	Clock& operator ++ ();		//前置单目运算符重载
	Clock operator ++ (int);	//后置单目运算符重载
private:	//私有数据成员
	int hour, minute, second;
};
 
Clock::Clock(int hour/* = 0 */, int minute/* = 0 */, int second/* = 0 */) {	
	if (0 <= hour && hour < 24 && 0 <= minute && minute < 60
		&& 0 <= second && second < 60) {
		this->hour = hour;
		this->minute = minute;
		this->second = second;
	} else
		cout << "Time error!" << endl;
}
void Clock::showTime() const {	//显示时间函数
	cout << hour << ":" << minute << ":" << second << endl;
}
 
Clock & Clock::operator ++ () {	//前置单目运算符重载函数
	second++;
	if (second >= 60) {
		second -= 60;
		minute++;
		if (minute >= 60) {
			minute -= 60;
			hour = (hour + 1) % 24;
		}
	}
	return *this;
}
 
Clock Clock::operator ++ (int) {	//后置单目运算符重载
	//注意形参表中的整型参数
	Clock old = *this;
	++(*this);	//调用前置“++”运算符
	return old;
}
int main() {
	Clock myClock(23, 59, 59);
	cout << "First time output: ";
	myClock.showTime();
	cout << "Show myClock++:    ";
	(myClock++).showTime();
	cout << "Show ++myClock:    ";
	(++myClock).showTime();
	return 0;
}

```

### 运算符重载为非成员函数

+ 函数的形参代表依自左至右次序排列的各操作数。

+ 后置单目运算符 ++和--的重载函数，形参列表中要增加一个int，但不必写形参名。

+ 如果在运算符的重载函数中需要操作某类对象的私有成员，可以将此函数声明为该类的友元。

```
#include <iostream>
using namespace std;
 
class Complex {	//复数类定义
public:	//外部接口
	Complex(double r = 0.0, double i = 0.0) : real(r), imag(i) { }	//构造函数
	friend Complex operator + (const Complex &c1, const Complex &c2);	//运算符+重载
	friend Complex operator - (const Complex &c1, const Complex &c2);	//运算符-重载
	friend ostream & operator << (ostream &out, const Complex &c); //运算符<<重载
private:	//私有数据成员
	double real;	//复数实部
	double imag;	//复数虚部
};
 
Complex operator + (const Complex &c1, const Complex &c2) {	//重载运算符函数实现
	return Complex(c1.real + c2.real, c1.imag + c2.imag); 
}
Complex operator - (const Complex &c1, const Complex &c2) {	//重载运算符函数实现
	return Complex(c1.real - c2.real, c1.imag - c2.imag); 
}
 
ostream & operator << (ostream &out, const Complex &c) {	//重载运算符函数实现
	out << "(" << c.real << ", " << c.imag << ")";
	return out;
}
 
int main() {	//主函数
	Complex c1(5, 4), c2(2, 10), c3;	//定义复数类的对象
	cout << "c1 = " << c1 << endl;
	cout << "c2 = " << c2 << endl;
	c3 = c1 - c2;	//使用重载运算符完成复数减法
	cout << "c3 = c1 - c2 = " << c3 << endl;
	c3 = c1 + c2;	//使用重载运算符完成复数加法
	cout << "c3 = c1 + c2 = " << c3 << endl;
	return 0;
}

```

## 虚函数

### 虚函数成员

- C++中引入了虚函数的机制在派生类中可以对基类中的成员函数进行覆盖（重定义）。

- 虚函数的声明

 

```c++
Virtual 函数类型 函数名（形参表）

 {

//    函数体

 }
```

### demo

```C++
#include <iostream>
using namespace std;

class Base1 { //基类Base1定义
public:
	virtual void display() const;	//虚函数
};
void Base1::display() const {
	cout << "Base1::display()" << endl;
}

class Base2::public Base1 { //公有派生类Base2定义
public:
	void display() const;	//覆盖基类的虚函数
};
void Base2::display() const {
	cout << "Base2::display()" << endl;
}
class Derived: public Base2 { //公有派生类
public:
	void display() const; 	//覆盖基类的虚函数
};
void Derived::display() const {
	cout << "Derived::display()" << endl;
}
 
void fun(Base1 *ptr) { //参数为指向基类对象的指针
	ptr->display();	//"对象指针->成员名"
}
 
int main() {	//主函数
	Base1 base1;	//定义Base1类对象
	Base2 base2;	//定义Base2类对象
	Derived derived;	//定义Derived类对象
	fun(&base1);//用Base1对象的指针调用fun函数
	fun(&base2);//用Base2对象的指针调用fun函数
	fun(&derived);//用Derived对象的指针调用fun函数
	return 0;
}
//Base1::display()
//Base2::display()
//Derived::display()

```

### 虚析构函数

- 可能通过基类指针删除派生类对象；

- 如果你打算允许其他人通过基类指针调用对象的析构函数（通过delete这样做是正常的），就需要让s基类的析构函数成为虚函数，否则执行delete的结果是不确定的。

### demo

```c++
#include <iostream>
using namespace std;
 
class Base {
public:
	~Base();   										//virtual ~Base();
};
Base::~Base() {
	cout<< "Base destructor" << endl;
 }
 
class Derived: public Base{
public:
	Derived();
	~Derived();
private:
	int *p;
};
Derived::Derived() {
	p = new int(0);
}
Derived::~Derived() { 
   cout <<  "Derived destructor" << endl;
	delete p;
}
 
void fun(Base* b) {
	delete b;
}
 
int main() {
	Base *b = new Derived();
	fun(b);
	return 0;
}
//Base destructor  没有执行派生类的析构函数            Derived destructor
												//Base destructor


```

### 纯虚函数

- 纯虚函数是一个在基类中声明的虚函数，它在该基类中没有定义具体的操作内容，要求各派生类根据实际需要定义自己的版本，纯虚函数的声明格式为：

+ virtual 函数类型 函数名(参数表) = 0;

+ 带有纯虚函数的类称为抽象类:

```
class  类名
 {
     virtual 类型 函数名(参数表)=0; //纯虚函数
     ...
}

```

### 抽象类

+ 作用
  + 抽象类为抽象和设计的目的而声明，将有关的数据和行为组织在一个继承层次结构中，保证派生类具有要求的行为。
  + 对于暂时无法实现的函数，可以声明为纯虚函数，留给派生类去实现

+ 注意
  +  抽象类只能作为基类来使用。
  + 不能声明抽象类的对象。
  + 构造函数不能是虚函数，析构函数可以是虚函数

```c++
#include <iostream>
using namespace std;
 
class Base1 { //基类Base1定义
public:
	virtual void display() const = 0;	//纯虚函数
};
 
class Base2: public Base1 { //公有派生类Base2定义
public:
	void display() const;	//覆盖基类的虚函数
};
void Base2::display() const {
	cout << "Base2::display()" << endl;
}
class Derived: public Base2 { //公有派生类Derived定义
public:
	void display() const;	//覆盖基类的虚函数
};
void Derived::display() const {
	cout << "Derived::display()" << endl;
}
 
void fun(Base1 *ptr) { //参数为指向基类对象的指针
	ptr->display();	//"对象指针->成员名"
}
 
int main() {	//主函数
	Base2 base2;	//定义Base2类对象
	Derived derived;	//定义Derived类对象
	fun(&base2);	//用Base2对象的指针调用fun函数
	fun(&derived);	//用Derived对象的指针调用fun函数
	return 0;
}
//Base2::display()
//Derived::display()
```



## 线性群体

### 线性群体概念

+ 群体是指由多个数据元素组成的集合体。群体可以分为两个大类：线性群体和非线性群体

+ 线性群体中的元素按位置排列有序，可以区分为第一个元素、第二个元素等
+ 非线性群体不用位置顺序来标识元素

+ 线性群体中的元素次序与其位置关系是对应的。在线性群体中，又可按照访问元素的不同方法分为直接访问、顺序访问和索引访问

### 直接访问群体——数组类

+ 静态数组是具有固定元素个数的群体，其中的元素可以通过下标直接访问
  + 缺点：大小在编译时就已经确定，在运行时无法修改
+ 动态数组由一系列位置连续的，任意数量相同类型的元素组成
  + 优点：其元素个数可在程序运行时改变
+ vector就是用类模板实现的动态数组

#### 实例

```c++
#ifndef ARRAY_H
#define ARRAY_H
#include <cassert>

template <class T>	//数组类模板定义
class Array {
private:
	T* list;		//用于存放动态分配的数组内存首地址
	int size;		//数组大小（元素个数）
public:
	Array(int sz = 50);		//构造函数
	Array(const Array<T> &a);	//拷贝构造函数
	~Array();			//析构函数
	Array<T> & operator = (const Array<T> &rhs); 	//重载"=“
	T & operator [] (int i); //重载"[]”
	const T & operator [] (int i) const;	
	operator T * ();		//重载到T*类型的转换
	operator const T * () const;
	int getSize() const;		//取数组的大小
	void resize(int sz);		//修改数组的大小
};

```

```c++
template <class T> Array<T>::Array(int sz) {//构造函数
	assert(sz >= 0);//sz为数组大小（元素个数），应当非负
	size = sz;	// 将元素个数赋值给变量size
	list = new T [size];	//动态分配size个T类型的元素空间
}
template <class T> Array<T>::~Array() { //析构函数
	delete [] list;
}
//拷贝构造函数
template <class T> Array<T>::Array(const Array<T> &a) {
	size = a.size; //从对象x取得数组大小，并赋值给当前对象的成员
	//为对象申请内存并进行出错检查
	list = new T[size];	// 动态分配n个T类型的元素空间
	for (int i = 0; i < size; i++) //从对象X复制数组元素到本对象 
		list[i] = a.list[i];
}
//重载"="运算符，将对象rhs赋值给本对象。实现对象之间的整体赋值
template <class T>
Array<T> &Array<T>::operator = (const Array<T>& rhs) {
	if (&rhs != this) {
//如果本对象中数组大小与rhs不同，则删除数组原有内存，然后重新分配
		if (size != rhs.size) {
			delete [] list;	//删除数组原有内存
			size = rhs.size;	//设置本对象的数组大小
			list = new T[size];	//重新分配n个元素的内存
		}
		//从对象X复制数组元素到本对象  
		for (int i = 0; i < size; i++)
			list[i] = rhs.list[i];
	}
	return *this;	//返回当前对象的引用
}
//重载下标运算符，实现与普通数组一样通过下标访问元素，并且具有越界检查功能
template <class T>
T &Array<T>::operator[] (int n) {
	assert(n >= 0 && n < size);	//检查下标是否越界
	return list[n];			//返回下标为n的数组元素
}
template <class T>
const T &Array<T>::operator[] (int n) const {
	assert(n >= 0 && n < size);	//检查下标是否越界
	return list[n];			//返回下标为n的数组元素
} 
//重载指针转换运算符，将Array类的对象名转换为T类型的指针
template <class T>
Array<T>::operator T * () {
	return list;	//返回当前对象中私有数组的首地址
}
template <class T>
Array<T>::operator const T * () const {
	return list;	//返回当前对象中私有数组的首地址
}
//取当前数组的大小
template <class T>
int Array<T>::getSize() const {
	return size;
}
// 将数组大小修改为sz
template <class T>
void Array<T>::resize(int sz) {
	assert(sz >= 0);	//检查sz是否非负
	if (sz == size)	//如果指定的大小与原有大小一样，什么也不做
		return;
	T* newList = new T [sz];	//申请新的数组内存
	int n = (sz < size) ? sz : size;//将sz与size中较小的一个赋值给n
	//将原有数组中前n个元素复制到新数组中
	for (int i = 0; i < n; i++)
		newList[i] = list[i];
	delete[] list;		//删除原数组
	list = newList;	// 使list指向新数组
	size = sz;	//更新size
}
#endif  //ARRAY_H

```

#### 深拷贝

### 顺序访问群体——链表类

#### 概念

+ 链表是一种动态数据结构，可以用来表示顺序访问的线性群体
+ 链表是由系列结点组成的，结点可以在运行时动态生成
+ 每一个结点包括数据域和指向链表中下一个结点的指针（即下一个结点的地址）。如果链表每个结点中只有一个指向后继结点的指针，则该链表称为单链表

#### 实例

```c++
//Node.h
#ifndef NODE_H
#define NODE_H
//类模板的定义
template <class T>
class Node {
private:
	Node<T> *next;	//指向后继结点的指针
public:
	T data;	//数据域
	Node (const T &data, Node<T> *next = 0);    //构造函数
	void insertAfter(Node<T> *p);	//在本结点之后插入一个同类结点p 
	Node<T> *deleteAfter();	//删除本结点的后继结点，并返回其地址
	Node<T> *nextNode();			//获取后继结点的地址
	const Node<T> *nextNode() const;	 //获取后继结点的地址
};
```

```c++

//类的实现部分
//构造函数，初始化数据和指针成员
template <class T>
Node<T>::Node(const T& data, Node<T> *next/* = 0 */) : data(data), next(next) { }
  
//返回后继结点的指针
template <class T>
Node<T> *Node<T>::nextNode() {
	return next;
}
 
//返回后继结点的指针
template <class T>
const Node<T> *Node<T>::nextNode() const {
	return next;
} 
//在当前结点之后插入一个结点p 
template <class T>
void Node<T>::insertAfter(Node<T> *p) {
    p->next = next; //p结点指针域指向当前结点的后继结点
    next = p;	 //当前结点的指针域指向p 
}
//删除当前结点的后继结点，并返回其地址
template <class T> Node<T> *Node<T>::deleteAfter() {
	Node<T> *tempPtr = next;	//将欲删除的结点地址存储到tempPtr中
	if (next == 0)	//如果当前结点没有后继结点，则返回空指针
		return 0;
	next = tempPtr->next;	//使当前结点的指针域指向tempPtr的后继结点
	return tempPtr;			//返回被删除的结点的地址
}
#endif //NODE_H

```

#### 链表的基本操作(先进先出)

+ 生成结点

+ 插入结点

+ 查找结点

+ 删除结点

+ 遍历链表

+ 清空链表

```c++
#ifndef LINKEDLIST_H
#define LINKEDLIST_H
#include "Node.h"

template <class T>
class LinkedList {
private:
	//数据成员：
	Node<T> *front, *rear
	Node<T> *prevPtr, *currPtr;   
	int size;
	int position;	

	Node<T> *newNode(const T &item,Node<T> *ptrNext=NULL);
	void freeNode(Node<T> *p);
	void copy(const LinkedList<T>& L);
public:
	LinkedList();	
	LinkedList(const LinkedList<T> &L);  
	~LinkedList();	
LinkedList<T> & operator = (const LinkedList<T> &L); 
	int getSize() const;
	bool isEmpty() const;
	void reset(int pos = 0);
	void next();
	bool endOfList() const;
	int currentPosition(void) const;
	void insertFront(const T &item);
	void insertRear(const T &item);
	void insertAt(const T &item);
	void insertAfter(const T &item);
	T deleteFront();	
	void deleteCurrent();
	T& data();
	const T& data() const
	void clear();
};

#endif  //LINKEDLIST_H

```

```c++
//9_7.cpp
#include <iostream>
#include "LinkedList.h"
using namespace std;
int main() {
	LinkedList<int> list;
	for (int i = 0; i < 10; i++) {
		int item;
		cin >> item;
		list.insertFront(item);
	}
	cout << "List: ";
	list.reset();
	while (!list.endOfList()) {
	cout << list.data() << "  ";
		list.next();	
	}
	cout << endl;
int key;
	cout << "Please enter some integer needed to be deleted: ";
	cin >> key;
	list.reset();
	while (!list.endOfList()) {
		if (list.data() == key) 
			list.deleteCurrent();
		list.next();
	}
	cout << "List: ";
	list.reset();
	while (!list.endOfList()) {
	 cout << list.data() << "  ";
		list.next
	}
	cout << endl;
	return 0;
}

```



### 栈类(先进后出)

+ 栈是只能从一端访问的线性群体
+ 可以访问的这一端称栈顶，另一端称栈底

#### 栈的基本状态

+ 栈空
  + 栈中没有元素
+ 栈满
  + 栈中元素个数达到上限
+ 一般状态
  + 栈中有元素，但未达到栈满状态

#### 栈的基本操作

+ 初始化

+ 入栈

+ 出栈

+ 清空栈

+ 访问栈顶元素

+ 检测栈的状态（满、空）

#### 实例

```c++
//Stack.h
#ifndef STACK_H
#define STACK_H
#include <cassert> 

template <class T, 
    int SIZE = 50>
class Stack {
private:
	T list[SIZE];
	int top;
public:
	Stack();
	void push(const T &item);
	T pop();
	void clear();
	const T &peek() const;
	bool isEmpty() const;
	bool isFull() const;
};

```

```c++
//模板的实现
template <class T, int SIZE>
Stack<T, SIZE>::Stack() : top(-1) { }	
template <class T, int SIZE>
void Stack<T, SIZE>::push(const T &item) {	
	assert(!isFull());	
	list[++top] = item;	
}
template <class T, int SIZE>
T Stack<T, SIZE>::pop() {	
	assert(!isEmpty());	
	return list[top--];	
}
template <class T, int SIZE>
const T &Stack<T, SIZE>::peek() const {
	assert(!isEmpty());	
	return list[top];	//返回栈顶元素
}
template <class T, int SIZE>
bool Stack<T, SIZE>::isEmpty() const {
	return top == -1;
}
template <class T, int SIZE>
bool Stack<T, SIZE>::isFull() const {	
	return top == SIZE - 1;
}
 
template <class T, int SIZE>
void Stack<T, SIZE>::clear() {	
	top = -1;
}
 
#endif	//STACK_H

```

### 队列类

+ 队列是只能向一端添加元素，从另一端删除元素的线性群(先进先出)

#### 队列的基本状态

+ 队空
  + 队列中没有元素

+ 队满
  + 队列中元素个数达到上限

+ 一般状态
  + 队列中有元素，但未达到队满状态

#### 循环队列

在想象中将数组弯曲成环形，元素出队时，后继元素不移动，每当队尾达到数组最后一个元素时，便再回到数组开头

#### 实例

```c++
//Queue.h
#ifndef QUEUE_H
#define QUEUE_H
#include <cassert>
//类模板的定义
template <class T, int SIZE = 50>
class Queue {
private:
	int front, rear, count;	//队头指针、队尾指针、元素个数
	T list[SIZE];	//队列元素数组
public:
	Queue();          //构造函数，初始化队头指针、队尾指针、元素个数
	void insert(const T &item);	//新元素入队
	T remove();	//元素出队
	void clear();	//清空队列
	const T &getFront() const;	//访问队首元素
	//测试队列状态
	int getLength() const;//求队列长度
	bool isEmpty() const;//判队队列空否
	bool isFull() const;//判断队列满否
};

```

```c++
//构造函数，初始化队头指针、队尾指针、元素个数
template <class T, int SIZE>
Queue<T, SIZE>::Queue() : front(0), rear(0), count(0) { }

template <class T, int SIZE>
void Queue<T, SIZE>::insert (const T& item) {//向队尾插入元素
	assert(count != SIZE);
	count++;	//元素个数增1
	list[rear] = item;	//向队尾插入元素
	rear = (rear + 1) % SIZE;	//队尾指针增1，用取余运算实现循环队列
}
template <class T, int SIZE> T Queue<T, SIZE>::remove() {	
	assert(count != 0);
	int temp = front;	//记录下原先的队首指针
    count--;			//元素个数自减
    front = (front + 1) % SIZE;//队首指针增1。取余以实现循环队列
    return list[temp];	//返回首元素值
}
template <class T, int SIZE>
const T &Queue<T, SIZE>::getFront() const {	
	return list[front];
}
template <class T, int SIZE>
int Queue<T, SIZE>::getLength() const {	//返回队列元素个数
	return count;
}
template <class T, int SIZE>
bool Queue<T, SIZE>::isEmpty() const {	//测试队空否
	return count == 0;
}
template <class T, int SIZE>
bool Queue<T, SIZE>::isFull() const {	//测试队满否
	return count == SIZE;
}
template <class T, int SIZE>
void Queue<T, SIZE>::clear() {	//清空队列
	count = 0;
	front = 0; 
	rear = 0; 
}
#endif  //QUEUE_H

```

## 群体数据的组织

### 方法

+ 插入排序

+ 选择排序

+ 交换排序

+ 顺序查找

+ 折半查找

### 排序（sorting）

+ 排序是计算机程序设计中的一种重要操作，它的功能是将一个数据元素的任意序列，重新排列成一个按关键字有序的序列。
  + 数据元素：数据的基本单位。在计算机中通常作为一个整体进行考虑。一个数据元素可由若干数据项组成。
  + 关键字：数据元素中某个数据项的值，用它可以标识（识别）一个数据元素。

+ 在排序过程中需要完成两种基本操作：
  + 比较两个数的大小
  + 调整元素在序列中的位置

#### 内部排序与外部排序

+ 内部排序：待排序的数据元素存放在计算机内存中进行的排序过程。

+ 外部排序：待排序的数据元素数量很大，以致内存存中一次不能容纳全部数据，在排序过程中尚需对外存进行访问的排序过程

##### 内部排序方法

+ 插入排序

每一步将一个待排序元素按其关键字值的大小插入到已排序序列的适当位置上，直到待排序元素插入完为止

```c++
template <class T>
void insertionSort(T a[], int n) {
	int i, j;
	T temp;

	for (int i = 1; i < n; i++) {		
		int j = i;
		T temp = a[i];
		while (j > 0 && temp < a[j - 1]) {
			a[j] = a[j - 1];
			j--;
		}
		a[j] = temp;
	}
}

```



+ 选择排序

每次从待排序序列中选择一个关键字最小的元素，（当需要按关键字升序排列时），顺序排在已排序序列的最后，直至全部排完

```c++
template <class T>
void mySwap(T &x, T &y) {
	T temp = x;
	x = y;
	y = temp;
}

template <class T>
void selectionSort(T a[], int n) {
	for (int i = 0; i < n - 1; i++) {
		int leastIndex = i;	
		for (int j = i + 1; j < n; j++)
			if (a[j] < a[leastIndex])
				leastIndex = j;
		mySwap(a[i], a[leastIndex	]);
	}
}

```



+ 交换排序
  + 两两比较待排序序列中的元素，并交换不满足顺序要求的各对元素，直到全部满足顺序
  + 要求为止对具有n个元素的序列按升序进行起泡排序的步骤：
    + 先将第一个元素与第二个元素进行比较，若为逆序，a则将两元素交换。然后比较第二、第三个元素，依次类推，直到第n-1和第n个元素进行了比较和交换。此过程称为第一趟起泡排序。经过第一趟，最大的元素便被交换到第n个位置。
    + 对前n-1个元素进行第二趟起泡排序，将其中最大元素交换到第n-1个位置。

如此继续，直到某一趟排序未发生任何交换时，排序完毕。对n个元素的序列，起泡排序最多需要进行n-1趟

```c++
template <class T>
void mySwap(T &x, T &y) {
	T temp = x;
	x = y;
	y = temp;
}
template <class T>
void bubbleSort(T a[], int n) {
	int i = n – 1;
	while (i > 0) {
	  int lastExchangeIndex = 0;
	  for (int j = 0; j < i; j++)
	    if (a[j + 1] < a[j]) {
         mySwap(a[j], a[j + 1]);
         lastExchangeIndex = j;
	    }
	   i = lastExchangeIndex;
	}
}

```



### 查找

#### 顺序查找

从序列的首元素开始，逐个元素与待查找的关键字进行比较，直到找到相等的。若整个序列中没有与待查找关键字相等的元素，就是查找不成功

```c++
template <class T>
int seqSearch(const T list[], int n, const T &key) {
	for(int i = 0; i < n; i++)
		if (list[i] == key)
			return i;            
	return -1;                 
}

```



#### 折半查找（二分法查找）

对于已按关键字排序的序列，经过一次比较，可将序列分割成两部分，然后只在有可能包含待查元素的一部分中继续查找，并根据试探结果继续分割，逐步缩小查找范围，直至找到或找不到为止

```c++
template <class T>
int binSearch(const T list[], int n, const T &key) {
	int low = 0;
	int high = n - 1;
	while (low <= high) {	
		int mid = (low + high) / 2;
		if (key == list[mid])    
			return mid;	
		else if (key < list[mid])
			high = mid – 1;
		else
			low = mid + 1;
	}
	return -1;
}

```











