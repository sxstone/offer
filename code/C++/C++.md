本文对应的代码在同一文件夹下的"C++程序示例"中。

# C++和C的区别？
C++是面向对象的编程语言，C是面向过程的。

# C++基础语法

## cin、cout对象的多个方法
- cin.ignore()  忽略前n个字符

- cin.getline()

- cin.get()   从缓冲流里面提取一个字符

- cin.peek()  从缓冲流里拿一个字符，然后把它放回去

- cin.gcount()

- cin.read()

- cout.precision()

- cout.width()

## 函数的重载(overloading)  

**所谓函数重载的实质是用同样的名字再定义一个有着不同参数但有着同样用途的函数**。对函数进行重载，可以简化编程工作和提高代码的可读性。
**重载并不是一个面向对象的特征，只是简化编程工作的一种方案。**目的是为了方便对不同数据类型进行同样的处理。

注意重载和覆盖的区别：如果两个函数的函数名、参数和返回值都相同，那么是函数的覆盖。

## 复杂的数据类型（数组、指针和结构）

数组的定义：
```c++
int name[10]; //定义一个长度为10的整形数组
```
例子：见C++程序实例.md中的Example-10

字符串：std::string

string是C++标准库定义的一个对象，其内建功能非常多。
```c++
//先定义三个string变量
string str1 = "hello";
string* str2 = new string("hello");
string str3 = "world";
```
- 获取字符串长度  **int length = str1.length();**

- 提取字符串  
```c++
//获取字符串的第一个字符
string::const_iterator it = str1.begin();
cout << *it << endl;
cout << endl;

//获取字符串的最后一个字符
it = str1.end();//end是指向最后一个字符后面的元素，而且不能输出,所以cout << *it << endl;这样输出会报错
it--;
cout << *it << endl;
cout << endl;
```
- 比较字符串  ****

```c++
if (str1 < str3)
{
	cout << "字符串的比较：" << "str1<str2" << endl;
}
cout << endl;
```
- 添加字符串

- 搜索字符串  **str1.find('a', 2)**,从位置2开始，查找'a'，返回首次匹配的位置，失败则返回-1；**str1.rfind('a', 7)**，从指定位置向前查找，直到串首。

- 倒置字符串  **reverse(str1.begin(), str1.end())**

- 字符串转数组  
```c++
string c = "abc123";
char *d = new char[20];
strcpy(d, c.c_str());//因为这里没有直接赋值，所以指针类型可以不用const char *
```
## 指针
指针是C和C++中最重要的数据类型之一。

想了解指针，必须先了解**地址**，每一个地址对应一个字节（一个字节8位）。

**寻址：**对于变量可以用两种方法来对他进行索引

- 通过变量名

- 通过地址。**一个重要的操作符，“取址”操作符：“&”，它的作用是获取变量的地址**。变量的地址在程序执行期间是不会发生变化的，
这是各个系统一个普遍的要求。不过，同一个程序不同时间加载到内存中，同一个变量的地址是会改变的。
```c++
int var = 123;
std::cout << "Address is:" << &var;
```
**地址是计算机内存中的某个位置，而指针是专门用来存放地址的特殊类型变量。**

一般情况下，我们用下边的方式来声明指针变量。

- type *pointerName;
- int *pointerName1 = &a1;
- 例如
```c++
int *p;
int pp = 123;
p = &pp;
```
- 注意这条语句 int *p1, p2, p3;这里声明的指针变量只有一个：p1，而p2和p3都是整型变量。

- 创建指针时，空格放在哪里都是没关系的，下边的语句都可以接受
	- int *p1;
	- int * p1;
	- int* p1;

- 指针前面的数据类型指的是指针指向的数据类型

允许void类型的指针  void *p;对一个无类型指针进行解引用前，必须先把它转换为一种适当的数据类型。

星号的两种用途：  
- 第一种是用于创建指针：int *myPointer = &myInt;  
- 第二种是对指针进行解引用：*myPointer = 3998; 这句的意思是对myInt赋值3998.

C++允许多个指针有同样的值

## 指针和引用的区别

总体上说，**指针指向一块内存，它的内容是所指内存的地址；而引用则是某块内存的别名，引用不改变指向。**  
```c++
int num = 0;
int* pointer = &num; //pointer是指针
int& reference = num; // reference是引用
cout << *pointer << " " << reference <<endl; // 输出 0 0
```
- 引用不可以为空，但指针可以为空.  
- 引用不可以改变指向，但是指针可以改变指向，而指向其它对象。  
- 引用的大小是所指向的变量的大小，因为引用只是一个别名而已；指针是指针本身的大小，4个字节。  
- 引用比指针使用起来形式上更漂亮，使用引用指向的内容时可以之间用引用变量名，而不像指针一样要使用*；定义引用的时候也不用像指针一样使用&取址。  
- 引用比指针更安全。由于不存在空引用，并且引用一旦被初始化为指向一个对象，它就不能被改变为另一个对象的引用，因此引用很安全。对于指针来说，它可以随时指向别的对象，并且可以不被初始化，或为NULL，所以不安全。const 指针虽然不能改变指向，但仍然存在空指针，并且有可能产生野指针（即多个指针指向一块内存，free掉一个指针之后，别的指针就成了野指针）。  


## 指针和数组

数组在计算机中是以一组连续的内存块保存的。**数组的名字其实也是一个指针，指向数组的基地址，就是第一个元素的地址。**
下面两句话做了同样的事情：  
- int *p1 = &myArray[0];  
- int *p2 = myArray;

已经得到数组的基地址的指针p1，如何访问数组的其他元素？p1++，这个运算并不是将地址值简单+1处理，
它是按照指向的数组的数据类型来递增的，也就是+sizeof(int)。

## 结构

**结构(struct)是一种由程序员定义的、由其他变量类型组合而成的数据类型**。定义一个结构的基本语法是
```
struct name
{
	type varName1;
	type varName2;
}; //注意，这里有个分号！
```
当需要处理一些具有多种属性的数据时，结构往往是很好的选择。C++对于一个结构所能包含的变量的个数是没有限制的，
结构的变量成为成员。用"."对结构成员进行赋值。**在C和C++里，指针是无所不能的，也可以指向结构**。

如何通过指针的解引用指向该结构的各个成员？（或者说是通过指针访问各个成员的值）  
- 创建一个指向该结构的指针：FishOil *pJiayu = &Jiayu;  
- 注意，指针的类型必须与指向的地址的变量类型一致，所以pJiayu指针的类型也是FishOil  
- 指针解引用来访问相应的变量值  (*pJiayu).name = "fahiuf";  
- 另一种方法，pJiayu -> name = "fahiuf";std::cout << pJiayu -> name;  

### C中的struct、C++中的struct和C++中的class的区别
C语言中，struct只是一个聚合数据类型，没有权限设置，也无法添加成员函数，无法实现面向对象编程，且如果没有typedef结构名，声明结构变量必须添加关键字struct。

C++中，class是面向对象编程的核心概念。有权限控制（默认private），可以添加成员函数，有继承（默认private继承）、多态等面向对象编程的功能。

C++中，struct功能大大扩展了，可以有权限设置（默认为public），可以有成员函数，可以继承（默认是public继承），可以实现面向对象编程，允许在声明结构变量时省略关键字struct。



## 传值、传址和传引用

**在默认的情况下，参数只能以值传递的方式给函数。即，被传递到函数的只是变量的值，而不是变量本身**  
**绕开“值传递”的第一种方法是向函数传递变量的地址，也就是说只需要在变量前面加一个“取地址”操作符&就可以了**  
**注意，如果传过去的是地址，在函数中必须要通过“*”对指针进行解引用，除非你有其他用途**
```c++
void changeAge(int age, int newAge) // 传值
{
	age = newAge;
}
int age = 20;
changeAge(age, age+1) // age还是20
```

```c++
void changeAge(int *age, int newAge) // 传址，这里需要把地址解引用
{
	*age = newAge;
}
int age = 20;
changeAge(&age, age+1) // age变为21
```


引用传递和传址的目的是一样的，都是把地址传递给函数，但语法不通更加容易使用了

**例子见Example-12**

## 联合、枚举和类型别名

### 联合（union）
联合和结构有很多相似之处，联合也可以容纳多种不通类型的值，但是它每次只能存储这些值中的某一个。
```c++
//定义联合
union password
{
	unsigned long birthday;
	unsigned short ssn;
	char *per;
}

//创建一个该类型的变量
password pw1;

//赋值
pw1.birthday = 19950101;
pw1.ssn = 12; //当执行这条语句时，上面的birthday会被丢弃。也就是说，它每次只能存储一个值。
```
### 枚举（enum）
**枚举类型用来创建一个可取值列表**

```c++
#include <iostream>
using namespace std;
int main() 
{
	enum weekdays{Monday, Tuesday, Wensday, Thursday, Friday}; //没有引号
	weekdays today;
	today = Monday;
	cout << today << endl; // 0

	today = Tuesday;
	cout << today << endl; // 1 

	switch(today)
	{
		case Monday: break;  
	}
}
```
注意，这里不需要使用引号，因为枚举值不是字符串。编译器会按照各个枚举值在定义时出现的先后顺序把它们与0 ~ n-1的整数
（n是枚举值的总个数）分别关联起来。

使用枚举值类型有两个好处：  
- 它们对变量的可取值加以限制；  
- 它们可以用做switch条件语句的case标号；（因为字符串是不能作为标号用的）  

### 类型别名(typedef)

例如，我们不想用int* 来创建指针，可以向下面这样定义一个类型别名：  
```c++
typedef int* intPointer;
```
之后就可以用下面的方式定义指针了
```c++
intPointer myPointer;
```
## 类和对象

**OOP的三大特征是：封装、继承和多态**

### 基础

**使用对象进行编程是C++的核心，也是C++比C更高级的重要根据之一**

对象的本质是一种新的数据类型。类和结构的区别是结构只有变量，类可以有变量和函数。  
有的程序员喜欢把类的声明和类的函数的定义分别存入两个不同的文件，前者存入.h头文件，后者存入相应的.cpp文件。  
**C++允许在类里声明常量，但是不允许对它进行赋值。**

```c++
class Car
{
	public:
	const float TANKSIZE = 85; // 出错
}
```
绕开这一限制的方法是创建一个静态常量
```c++
class Car 
{
	public:
	static cosnt float FULL_GAS = 85;
}
```
### 构造函数（构造器）

构造器和通用方法的主要区别：  
- 构造器的名字必须和它所在的类的名字一样(大小写保持一致)；  
- 系统在创建某个类的实例时会第一时间自动调用这个类的构造器；  
- 构造器永远不会返回任何值。

创建构造器，需要先把它的声明添加到类里。
```c++
class Car 
{
	Car(void);
}

在结束声明之后开始定义构造器本身：
```c++
Car::Car(void) //不用写void Car::Car(void)
{
	color = "WHITE";
	engine = 'V8";
	wheel = 4;
	gas_tank = FULL_GAS;
}
```
构造对象数组：数组可以是任何一种数据类型，页包括对象。如Car mycar[10];
调用的语法是mycar[x].color;其中x代表数组元素的下标。

**每个类至少有一个构造器，如果没有定义，那么编译器会使用如下语法替你定义一个**
ClassName::ClassName(){}.这是一个空的构造器，除此之外，编译器还会替你创建
一个副本构造器(CopyConstructor)。  

### 析构函数（析构器）

在创建对象时，系统都会自动调用一个特殊的方法，即构造函数；相应的，在销毁一个对象时，系统
也会调用另一个特殊的函数，即析构函数。一般来说，构造器用来完成时限的初始化和准备工作（申请分配内存），
析构器用来完成时候所必须的清理工作（清理内存）。**析构器和构造器有相同的名字，只不过前面多了一个
波浪符"~"前缀**  

```c++
class Car 
{
	Car(void);
	~Car(); //析构器时不带参数的
}
```
在简单的类中，析构器可有可无。在复杂的类中，析构器很重要，没有可能会引起内存泄漏。

### this指针

通过一个例子来认识this指针
```c++
class Human
{
	char fishc;
	Human(char fishc);
}
Human::Human(char fishc)
{
	//fishc = fishc;
	this -> fishc = fishc;
}
注释部分时错误写法，因为编译器不知道哪个是传入的参数fishc，哪个是类的属性fishc。**this指针意思是指向当前类生成的对象**  
这样编译器就知道，赋值符左边是当前对象的属性，右边的是构造器传入来的参数。  

**注意：**  
- 如果代码不存在二义性问题，就不必使用this指针！  

### 类的继承

继承是面对对象编程技术的一个核心概念，它使传统的软件开发模式发生了革命性的变化。
**基类是可以派生出其他类的类，子类是从基类派生出来的类**。  
继承的语法：  
```c++
class SubClass: public SuperClass{}
class Pig : public Animal{}
```

示例见Example-13。
#### 继承机制中的构造函数和析构函数  Example-14
**注意：构造函数先基类后子类，析构函数反之。基类的析构函数将在子类的最后一条语句执行完毕后才被调用**  
```c++
//当构造函数有参数的时候
Animal::Animal(std::string theName)
{
	name = theName;
}
Pig::Pig(std::string theName):Animal(theName)
{}
```
**当调用Pig pig("小猪猪");实际动作发生在Animal()方法里**  


### 访问控制
#### 属性和方法的访问控制
public:可以被任意实体访问  
protected:可以被这个类本身和它的子类访问  
private:只有这个类本身可以访问。使用private的好处是今后修改可以只修改某个类的内部实现，而不必重新修改整个程序。
因为其他代码根本访问不到private保护的内容，所以不会出现“牵一发而动全身”的BUG发生!  	  

在编写你的类定义代码时，应该从public开始，然后是protected，最后是private。  

#### 关于从基类继承来的属性和方法的保护

class Pig:public Animal{}

**C++不仅允许你对在类里定义的方法和属性实施访问控制，还允许你控制子类可以访问基类里的那些属性和方法**  
- public：继承的属性和方法的访问级别不发生任何改变。  
- protected：使得子类外部的代码无法通过子类去访问基类中的public。  
- private：从基类继承来的每一格成员都当成private来对待，这意味着只有这个子类可以使用它从基类继承来的元素。  
一般我们用public既可以。

### 覆盖（重写）方法和重载方法

当我们需要**在基类里提供一个通用的函数，但在它的某个子类里需要修改这个方法的实现**，在C++里覆盖(overriding)就可以做到。
 

**重载机制使你可以定义多个同名的方法，只是它们的输入参数必须不同**。（因为编译器是依靠不同的输入参数来区分不同的方法）。
**继承之后不能重载**。   

### 友元关系

**友元关系是类之间的一种特殊关系，这种关系不仅允许友元访问对方的public方法和属性，还允许友元访问对方的protected和private方法和属性**。

**声明一个友元关系的类：只要在类声明里的某个地方加上一条friend class ** 就可以了**。这条语句可以放在任何地方，放在public、protected和
private的任何段落里都可以。  

### 静态属性和静态方法  Example-15

OOP（面向对象编程）的一个重要特征是用一个对象把数据和对数据处理的方法封装在一起。**使用对象（或者说某个类的实例）来调用方法，每个方法只处理调用它的那个对象所包含的数据，所有的数据都属于同一个对象。**  
C++允许我们把一个或多个成员声明为属于某个类，而不是仅属于该类的对象。**这么做的好处是程序员可以在没有创建任何对象的情况下调用有关的方法**。
**另外一个好处是能够让有关的数据仍在该类的所有对象间共享。**  

创建一个静态属性和静态方法：  
- 只需要在它的声明前加上static保留字即可。  


**静态与非静态的区别：**  
- **静态属性保存在类空间，非静态属性保存在对象空间**   
- **静态属性的访问，通过类访问（::），非静态属性的访问通过对象(->)**  
- 静态方法的访问，通过类访问(::)  
- 如果一个方法内部不操作属于对象空间的属性，那么将其封装成静态方法，通过类来调用，这样效率会快很多  
- 静态方法中不能出现this指针。**因为静态方法不是属于某个特定的对象，而是由全体对象共享的。**     

注意：  
- 静态数据成员不能在类中初始化，实际上类定义只是在描述对象的蓝图，在其中指定初值是不允许的。也不能在类的构造函数中初始化该成员，因为静态数据成员为类的各个对象共享，否则每次创建一个类的对象则静态数据成员都要被重新初始化。静态成员的值对所有的对象是一样的。**静态成员可以被初始化，但只能在类体外进行初始化**（通常在实现文件中进行初始化）。  
- 静态成员函数在类外实现时候无须加static关键字，否则是错误的。  
- 静态成员仍然遵循public，private，protected访问准则。   
- 静态成员函数没有this指针，它不能返回非静态成员，因为除了对象会调用它外，类本身也可以调用。静态成员函数可以直接访问该类的静态数据和函数成员，而访问非静态数据成员必须通过参数传递的方式得到一个对象名，然后通过对象名来访问。  
- **静态成员之间可以相互访问**，包括静态成员函数访问静态数据成员和访问静态成员函数；**非静态成员函数可以任意地访问静态成员函数和静态数据成员；静态成员函数不能访问非静态成员函数和非静态数据成员**；调用静态成员函数，可以用成员访问操作符(.)和(->)为一个类的对象或指向类对象的指针调用静态成员函数;静态成员变量只能被静态成员函数调用，静态成员函数也是由同一类中的所有对象共用，只能调用静态成员变量和静态成员函数。  
- 在使用静态属性时，千万不要忘记为它们分配内存。具体做法是在类声明的外部对静态属性做出声明（就像声明一个变量那样）。  
- 静态方法也可以使用一个普通方法的调用语法来调用，但建议不要这么做，那会让代码变得糟糕，因为不方便和普通方法区分开来。**要使用ClassName::methodName(); 不要使用objectName.methodName();**  

### 虚方法（virtual method）

#### new和delete保留字

在C和C++中，可以在没有创建变量的情况下为有关数据分配内存。也就是直接创建一个指针并让它指向新分配的内存块：  
```c++
int *pointer = new int;
*pointer = 110;
std::cout << *pointer;
delete pointer;
```
最后一步非常必要和关键，因为**C++不会自动释放内存，程序中的每一格new操作都必须有一个与之对应的delete操作**。  

#### 虚方法
声明一个虚方法的语法非常简单，只要在其原型前面加上virtual保留字即可。  
- virtual void play();  

虚方法是继承的，一旦在基类里把某个方法声明为虚方法，在子类里就不可能再把它声明为一个非虚方法了。  
**虚方法和非虚方法的区别：非虚方法不能被重写，只能被重定义。**
#### 技巧
- 如果拿不准要不要把某个方法声明为虚方法，那么就把它声明为虚方法好了。  
- 在基类里把所有的方法都声明为虚方法会让最终生成的可执行代码的速度变得稍微慢一些，但好处是可以一劳永逸地确保程序的行为符合你的预期。  
- 在实现一个多层次的类继承关系时，最顶级的基类应该只有虚方法。  
- 析构器都是虚方法！从编译的角度看，它们只是普通的方法。如果它们不是虚方法，编译器就会根据它们在编译时的类型而调用那个在基类里定义的
版本（构造器），那样往往会导致内存泄漏。  

### C++的多态


#### 重载、重写、重定义的的区别

##### 1. 重载

​	函数重载是指在同一作用域内（**在同一个类中**），**函数名相同，参数列表不同**的一组函数，这组函数被称为重载函数。重载函数通常用来命名一组功能相似的函数，这样做减少了函数名的数量，避免了名字空间的污染，对于程序的可读性有很大的好处。比如说四则运算中的+函数，可以根据参数不同定义参数为int、str时的加法。被重载的函数不需要有virtual关键字，它们的返回值也有所不同。但调用函数时，会根据参数的类型选择执行哪一个函数。

##### 2. 重写（覆盖）

重写就是override，是指**派生类中定义基类中的虚函数，为多态服务**。特征是**重写的函数与基函数不在一个作用域中（基类和派生类），它们的函数名、函数参数类型、返回值类型都必须相同，但它们的访问修饰符可以不同（private、public、protected），且基类必须是虚函数或纯虚函数**。举个例子，父亲要看电影、儿子也要看电影，但他们看完电影的反应是不一样的（但都得是一种类型的反应，比如说某句话，或者做某件事），他们的函数输入也必须都是电影。父亲看完后print 好看，儿子看完后print 难看，这就是一种虚函数的重写。在函数重写时，往往会加上override关键字声明，以防和重定义混淆。

##### 3. 重定义

重定义也叫隐藏，**重定义是指在不同作用域中，派生类定义了一个和基类函数名字相同、返回值可以不同、参数不同重定义函数**。

- 当基类函数是虚函数时，若子类函数的参数与基类函数相同，那么它叫重写，若参数不同，那么它叫重定义。当基函数和子函数参数不同，并且子函数还用override关键字声明时，编译就会报错。
- 当基类函数不是虚函数时，无论参数是否相同，子类函数都算重定义。

#### 虚函数、纯虚函数、静态联编、动态联编

##### 1. 虚函数、静态联编、动态联编

- 静态联编是指在函数编译时就已确定要调用函数的哪个实现，而动态联编是指在函数执行时才确定调用函数的哪个实现，有些类似tf和pytorch的静态图和动态图。静态联编效率高，动态联编更灵活，**C语言中全都是静态联编**，这也可以说明C中没有对象的概念，也不存在灵活的多态。动态联编还需要和虚函数一起讲。

- 虚函数时为了满足多态的特性，在基类中定义的一种函数。当一个基类类型的指针指向一个派生类的对象时，会优先调用派生类对象中定义的虚函数，而不是基类中的虚函数。比如

```c++
class Cfather
{
public:
virtual void Eat(){cout<<"Im your father"<<endl;}
void Move(){cout<<"father can move, kid cant do it";}
private:
};
class CChild : public Cfather
{
public:
virtual void Eat(){cout<<"Im your kid"<<endl;}
private:
};
Cfather m_father;
CChild m_child;
Cfather *p ;  // 注意，此时指针类型是父类
p = &m_father ; //指向基类对象的父类类型指针
p->Eat();    //输出"Im your father"
p = &m_child;
p->Eat();    // 输出"Im your kid"
//如果子类没有重写此函数时，则还是调用父类中的
p->Move(); //输出 "father can move, kid cant do it"
```

在这里，指向子类对象的指针调用Eat函数时就是动态联编，直到运行时才根据对象m_child的类型确定调用哪个函数实现。

##### 2. 纯虚函数

纯虚函数比较简单，类似于Java中的接口函数。它在基类中不允许被定义，但要求它的派生类必须实现纯虚函数，有纯虚函数的类也叫做**抽象类**（抽象类不能生成对象）。纯虚函数的意义在于它代表着一种抽象的对象，比如生物，生物可以由人、老虎等继承，但是它本身缺少实际的意义，所以生物会作为一个抽象类。要定义纯虚函数，只需要在虚函数的函数体后加一个“=0”即可，比如

```c++
class Creature{
      public:
          virtual void speak() = 0;//纯虚函数, print生物叫声，但“生物”本身是没有叫声的
}
class Dog{
  		public:
  				virtual void speak(){cout<<"汪汪汪！"<<endl;}
}
class Cat{
  		public:
  				virtual void speak(){cout<<"喵喵喵！"<<endl;}
}
```

### 抽象方法（abstract method，纯虚函数）
把某个方法声明为一个抽象方法等于告诉编译器**这个方法必不可少，但是在这个基类里还不能为它提供一个实现**  
纯虚函数的定义：在声明一个虚函数的基础上，在原型的末尾加上“=0”。告诉编译器不用浪费时间在这个类里寻找这个方法的实现。  

### 多态性  
**多态性是OOP的重要特征之一**  
**多态性是指用一个名字定义不同的函数，调用同一个名字的函数，却执行不同的操作，从而实现“一个结构，多种方法”**。  
**多态的三大特征：重写，继承和子类指向父类**

重载和多态无关。
 
多态是如何实现绑定的？  
- 编译的实时性：通过重载实现；  
- 运行时的多态性：通过虚函数实现；  
编译时的多态性特点是运行速度快，运行时的多态性是高度灵活和抽象。  


**成员函数的重载、覆盖和隐藏的区别：**  
- 成员函数重载的特征：
  - 相同的范围（在同一个类中）；  
  - 函数名字相同；  
  - 参数不同；   
  - virtual关键字可有可无。  
- 重写（覆盖）是指派生类的函数覆盖基类函数，特征：  
  - 不同的范围（分别位于派生类和基类）；  
  - 函数名字相同；  
  - 参数相同；  
  - 基类函数必须有virtual关键字。  
- 重定义  
  - 不同的范围（分别位于派生类和基类）；  
  - 函数名字相同；  
  - 如果被重定义的函数是非虚函数，参数是否一致无所谓；如果被重定义的函数是虚函数，那么参数必须不一致。  



析构函数都是虚方法：  
- 析构函数是为了释放内存资源的，如果析构函数不被调用会造成内存泄漏。  
- **析构函数都是虚方法是为了当一个基类的指针删除一个派生类的对象时，派生类的析构函数可以被正确调用。**  
- 当类里面有虚函数时，编译器会给类添加一个虚函数表，里边存放着虚函数指针。**为了节省资源，只有当一个类被用来作为基类的时候，我们才把析构函数写成虚函数**。 （因为继承虚函数的函数会自动变为虚函数，所以只需要把基类的析构函数写成虚函数） 
  
### 运算符重载
**运算符重载的方法是定义一个重载运算符的函数，在需要执行被重载的运算符时，系统就自动调用该函数，以实现相应的运算**。也就是说运算符重载是通过定义函数实现的，运算符重载实质上是函数的重载。

重载运算符的函数一般格式如下：
```c++
函数类型 operator 运算符名称（形参）
{
	对运算符的重载处理
}

int operator+(int a, int b)
{
	return (a-b);
}
```
- C++不允许用户自己定义新的运算符，只能对已有的C++运算符进行重载。下面五个运算符不允许重载：    
	- .（成员访问运算符）  
	- .*（成员指针访问运算符）  
	- ::（域运算符）  
	- sizeof（尺寸运算符）  
	- ?:（条件运算符）  
- 重载不能改变运算符运算对象个数；  
- 重载不能改变运算符的优先级别；  
- 重载不能改变运算符的结合性；  
- 重载运算符的函数不能有默认的参数；  
- 重载运算符必须和用户自定义类型的对象一起使用，其参数至少应该有一个是类对象或类对象的引用。也就是说，参数不能全部都是C++的标准类型，这样约定是为了防止用户修改用于标准类型结构的运算符的性质。  

运算符重载除了可以作为累的成员函数外，还可以是非成员函数：放在类外，做Complex类（举个例子，复数类）的友元函数存在。为什么要把运算符函数作为友元函数呢？因为运算符函数要访问Complex类对象的成员，如果运算符函数不是Complex类的友元函数，而是一个普通函数，它是没有权限访问Complex类的私有成员的。由于友元的使用会破坏类的封装，因此从原则上说，要尽量将运算符函数作为成员函数。  

注意：  
- 只在必要的时候才重载运算符；  
- 重载运算符时，千万不要让它们失去原始的意义，你完全重载+然后对它进行减法操作，有这种做法的员工在公司是要被开除的。  

### 多继承（multiple inheritance）

可能是OOP技术中最惹人争议的功能，可能引起一些难以预料的后果。因此Java和C#等面向对象语言大都只支持多继承的最简单版本。  

**什么时候需要用多继承？**  
- 只要遇到的问题无法只用一个“是一个”关系来描述的时候，就可以用多继承；  
- 例子：老师和学生都是人，也就是说Teacher类和Student类都继承Person类，但是有些学生同时是助教（即他既是学生又是老师），那么可以写一个
TeachingStudent类让他同时继承Teacher类和Student类。这里就是多继承。    
- 基本语法：
```c++
class TeachingStudent: public Student, public Teacher
{

}
```

### 虚继承

上面的TeachingStudent类继承自Teacher和Student两个类，因而继承了两组Person类的属性。这在某些时候没问题，比如classes属性，他学习的班级和教的班级是不一样的，但是也有可能不合理，如name属性，因为他作为老师和作为学生的名字应该一样。  为了解决这个问题，可以使用**虚继承**。 通过虚继承某个基类，就是在告诉编译器：**当前这个类派生出来的子类只能拥有那个基类的一个实例。**  
虚继承的语法：
```c++
class Teacher:virtual public Person
{}
```
让Student和Teacher类都虚继承自Person类，编译器将确保从Student和Teacher类再派生出来的子类只能拥有一份Person类的属性。  


## 错误处理和调试  

### 调试技巧
程序出错分为两大类：编译时出错(complile-time error)和运行时出错(run-time error)。相比之下，编译时出错是比较好应对的，因为它会告诉你哪一行出错以及什么错误。  

**预防或应对编译时错误的好经验**：   
- 培养并保持一种编程风格！  
- 认真对待编译器给出的错误/警告信息。  
- 三思而后行。  
	- 开始写代码前先想好具体的思路。  
	- 编译错误不要立刻修改源代码，应该先完整地审阅一遍源代码，再开始纠正错误。否则可能错误越改越多。   
- 注意检查最基本的语法  
- 把可能有问题的代码改为注释   
	- 不要轻易整行整行地删除代码，把可能有问题的代码先改为注释，看错误是否还在。排除法。。。
- 换一个环境或开发工具试试。  
- 检查自己是否已经把所有必要的头文件全部include进来。比如只有#include <iostream>才能使用cout.  
- 留意变量的作用域和命名空间。  
- 休息一下再调试。  
- 多使用调试工具。  
- 把调试好的代码另外保存起来并不要改动它，然后把代码划分为各个模块，用它们来搭建新的应用程序，会减少很多开发和调试的时间。  


**预防或应对运行时错误的好经验**：  
- 培养并保持一种良好的编程风格！杂乱无章是程序员的大敌。  
- 多用注释，用好注释。  
- 注意操作符的优先级。比如b = a--,是先把a赋值给b，然后a减去1。另外，不确定就用括号括起来。    
- 不要忘记对用户输入和文件输入进行合法检查。  
- 不要做任何的假设。最大熵原理。  
- 把程序划分为比较小的单元模块来测试。写程序的时候也要注意模块化。  

### 让函数返回错误代码

让程序处理潜在错误，即异常处理。  

C和C++都有一个专门为调试准备的工具，就是**assert()**函数。在C语言中是assert.h库文件里定义，在C++里是cassert  

**assert()函数需要有一个参数，它将测试这个输入参数的真or假，如果为真，什么都不做；如果为假，做一些操作**  

```c++
#include<cassert>
int main()
{
	int i = 20;
	assert(i == 65);
	return 0; 
}

使用cout输出变量值。  

### 捕获异常

异常（exception）就是与预期不相符合的反常现象。  
基本思路：  
1. 安排一个C++代码（try语句）去尝试做某些事——尤其是那些可能会失败的事情。  
2. 如果发生问题，就会抛出一个异常（throw语句）。  
3. 再安排一些代码（catch语句）去捕获这个异常并进行相应的处理。  

捕获异常的基本语法如下：

```c++
try
{
	// Do something.
	// Throw an exception on error.
}

catch
{
	// Do whatever.
}
```
**注意：**  
- 每条try语句至少有一条配对的catch语句。必须定义catch语句以便让它接收一个特定类型的参数。  
- C++还允许我们定义多条catch语句，让每条catch语句分别对应着一种可能的异常类型：  
  - catch (int e) {...}  
  - catch (bool e) {...}  
  - catch (...) {...}
- 最后一条catch语句可以捕获任何类型的异常  
- 可以用throw保留字来抛出一个异常：throw 1;  
- 在某个try语句块里执行过throw语句，它后面的所有语句（截止到这个try语句块末尾）将永远不会被执行。  


如何让函数抛出异常：在定义函数时明确地表明你想让它抛出一个异常，为了表明你想让它抛出哪种类型的异常，可以使用
如下所示的语法：  
- type functionName(arguments) throw(type);  
如果没有使用这种语法来定义函数，就意味着函数可以抛出任意类型的异常。  

一条原则，在构造器和析构器里不应该使用异常。  
如果try语句块无法找到一个与之匹配的catch语句块，它抛出的异常将终止程序的执行。  
在C++标准库里有一个名为exception的文件，该文件声明了一个exception的基类。可以用这个基类来创建个人的子类以管理异常。
如果你打算使用对象作为异常，记住一个原则：**以值传递的方式抛出异常，以引用传递的方式捕获对象**。  

## 动态内存管理  

固定不变的内存空间其实是在编写程序时就可以确定的（一半以变量的形式）。这些程序都不能在程序运行期间动态增加或减少内存空间。  

**静态内存**：变量（包括指针变量）、固定长度的数组、某给定类的对象。我们可以在程序代码里通过它们的名字或者地址来访问和使用它们。  
使用静态内存最大弊端是，不得不在编写程序时为有关变量分配一块尽可能大的内存（以防止不够存放数据）。一旦程序开始运行，不管实际情况如何，
那个变量都将占用那么多的内存，没有任何办法能改变静态内存的大小。  

**动态内存**由一些没有名字、只有地址的内存块构成，那些内存块是在程序运行期间动态分配的。它们来自一个由C++标准库替你管理的“内存池”。  
从内存池申请一些内存需要用new语句，它将根据你提供的数据类型分配一块大小适当的内存。不必担心内存块的尺寸问题，编译器能够记住每一种数据类型的单位长度并迅速计算需要分配多少字节。  
如果有足够可用内存能满足你的申请，new语句将返回新分配地址快的起始地址。如果没有足够的内存空间，那么new语句将抛出std::bad_alloc异常。  
**注意在用完内存块之后，应该用delete语句把它还给内存池。**另外作为一种附加的保险措施，在释放了内存块之后还应该把与之关联的指针设置为NULL。  

**NULL指针**：有一个特殊的地址值叫做NULL指针。当把一个指针的变量设置为NULL时，它的含义是那个指针将不再指向任何东西。  int *x; x = NULL;//
这时x啥都不指向  
所以在用delete释放内存后，指针会保留一个毫无意义的地址，我们要将指针变量赋值为NULL。  

**注意：**  
- 静态内存和C++保留字static没有任何关系。静态内存指内存在编译时被设定为一个固定的值，这个值在程序运行时是无法改变的。  
- new语句返回的内存块很可能充满“垃圾”数据。所以我们通常先往里面写一些东西覆盖，再访问它们，或者在类直接写一个构造器来初始化。  
- 

为对象分配内存和为各种基本数据类型分配内存的做法完全一样：  
- 用new想内存池申请内存；  
- 用delete来释放内存。  
  
注意：  
- 在重新使用某个指针之前千万不要忘记调用delete语句，如果不这么做，那个指针将得到一个新的内存块的地址，而程序将永远无法释放
原先那个内存块，因为它的地址已经被覆盖掉了。  
- delete语句只释放给定指针变量正指向的内存块，不影响这个指针。在执行完delete语句后，那个内存块被释放了，但指针变量还依然在。
（所以要给指针变量赋值NULL）。  

## 动态数组  

用new给基本类型和对象在运行时分配内存，但它们的尺寸在编译时就已经确定了——因为我们申请内存的数据类型在程序里有明确的定义，有
明确的单位长度。  
有些时候，必须要等到程序运行时才确定需要申请多少内存，甚至还需要根据程序运行的情况追加申请更多的内存。在某种意义上讲，这样的内存
管理才是真正的动态。  



例子：写一个程序，能够在程序运行时让用户输入一个值自行定义数组的长度。  **Example-16**  
由于数组的长度在编写程序时是未知的，意味着无法在定义数组时在方括号里给出一个准确的数字。  
**数组名和下标操作符的组合可以被替换成一个指向该数组基地址的指针和对应的指针运算**  
- int a[2];//a代表基地址，2代表偏移2 * sizeof(int)位。int是四个字节。  
- int *x = a; 
- 指针变量x指向数组a的地址，a[0]和*x都代表数组的第一个元素。根据指针运算原则，a[1]等价于*(x+1)，以此类推。  

把一个数组声明传递给new语句将使它返回一个该数组基类型的指针。  
把数组下标操作符和该指针变量的名字搭配使用就可以向对待一个数组那样使用new语句为这个数组分配的内存块了。  
例如：  
- int *x = new int[10];  
- 可以向对待一个数组那样使用指针变量x:  
  - x[1] = 45;  
  - x[2] = 1;  
- 当然，也可以用一个变量来保存该数组的元素个数。**下面即是动态数组的声明**：  
  - int count = 10;  
  - int *x = new int[count];

删除一个动态数组要比删除其他动态数据类型稍微复杂一些。**因为用来保存数组地址的变量只是一个简单的指针，所以需要明确地告诉编译器它应该删除一个数组**。
具体的做法是**在delete保留字的后面加上对括号：delete [] x;**  

## 从函数或方法返回内存  Example-17 

动态内存的一个常见用途是**让函数申请并返回一个指向内存块的指针**。掌握这个技巧很重要，尤其是在你打算使用由别人编写的库文件时。  

基本思路：**在函数里面调用new语句为某种对象或某种数据类型分配一块内存，再把那块内存的地址返回给程序的主代码，主代码将使用那块内存并
在完成有关操作后立刻释放。**  

### 为什么不应该让函数返回一个指向局部变量的指针

变量作用域的概念：函数或方法有它们自己的变量，这些变量只能在这个函数内部使用，这些变量我们成为局部变量（local variable）  
传址调用的概念：利用指针在某个函数内部改变另一个函数的局部变量的值。  

**任何一个函数不应该把它的局部变量的指针作为它的返回值！因为局部变量在栈里，函数结束会自动释放。**那么在主函数里使用就会出问题。  

**如果想让一个函数在不会留下任何隐患的情况下返回一个指针，那它只能是一个动态分配的内存块的基地址。**  

## 函数指针和指针函数  
函数指针：  **Example-18**
- 指向函数首地址的指针变量成为函数指针。  

指针函数：**Example-17**     
- 一个函数可以反回一个整型数据的值，字符类型值和实型类型的值，还可以**反回指针类型的数据，使其指向某个地址单元**。  

### 副本构造器

我们可以把一个对象赋值给一个类型与之相同的变量。编译器将生成必要的代码把“源”对象各属性的值分别赋值给“目标”对象的对应成员。这种
赋值行为称之为逐位复制(bitwise copy)。这种行为在绝大多数场合都没问题，但如果某些成员变量是指针的话，问题就来了：对象成员进行
逐位复制的结果是你将拥有两个一模一样的实例，而这两个副本里的同名指针会指向相同的地址。当删除其中一个对象时，它包含的指针也将被删除，但万一此时另一个副本（对象）还在引用这个指针，就会出问题。  

例子：  
```c++
MyClass obj1;
MyClass obj2;
obj2 =obj1;
```
第三行代码把obj1的值赋值给obj2,如果里面有指针就可能出问题。  
一个解决方法：重载"="操作符，在其中对指针进行处理。  
```c++
MyClass &operator = (const MyClass &rhs); // rhs是right hand side的缩写
```
上面的语句告诉我们这个方法所预期的输入参数应该是一个MyClass类型的、不可改变的引用。  
- 因为这里使用的参数是一个引用，所以编译器在传递输入参数时就不会再为它创建另一个副本（否则可能导致无限递归）  
- 又因为这里只需要读取这个输入参数，而不需要改变它的值，所以我们用const把那个引用声明为一个常量，确保万无一失。  

**只对赋值操作符进行重载还不能完美地解决问题**

副本构造器：  
MyClass(const MyClass &rhs);

## 强制类型转换
### 静态对象强制类型转换  

### 动态对象强制类型转换  

## 避免内存泄露

分配了一个内存块但忘记释放它，这是一种严重的错误。这样的内存块将等到程序执行结束时才会被释放掉。如果程序运行很长时间（例如在服务器上，注意
不是所有的系统都像Windows一样经常重启）并且在不停地申请内存块，忘记释放那些已经不再有用的老内存块将迟早把内存消耗完，直接导致后边的new操作无法执行甚至是崩溃。  **这样的编程漏洞称之为内存泄露（memory leak）**。  

new语句所返回的地址是访问这个内存块的唯一线索，同时也是delete语句用来把这个内存块归还给内存的唯一线索。下面代码中如果这个地址值（保存在x里）
丢失了，就会发生内存泄露。  

```c++
int *x; 
x = new int[100];
delete[] x;
x = NULL;
```
地址值会因为很多原因丢失，比如因为一个指针变量被无意中改写，例如：
```c++
int *x; 
x = new int[100];
x = new int[200]; //上一句申请的内存块地址就丢失了
delete[] x;
x = NULL;
```
会导致内存泄露的另一种情况是用来保存内存块地址的指针变量作用域问题，例如：
```c++
void foo()
{
	Myclass *x;
	x = new MyClass();
}
当退出这个函数的时候，这个函数对应的栈空间就会被自动收回，因为栈空间是由系统分配和系统收回的。所以申请的内存块的地址就不见了。所以在函数
返回之前加入一条delete x;语句或者让函数把内存块的地址返回，即return x;  

### 内存作用域
变量都有一个作用域：规定了它们可以在程序的哪些部分使用。  
**动态内存不存在作用域的问题，一旦被分配，内存块就可以在程序的任何地方使用。一旦new出来了，只有delete可以把它删除。**
所以必须由程序员来跟踪它们的使用情况，并在不需要用到它们的时候把它们及时归还给系统。  
**这里需要特别注意的是，虽然动态分配的内存块没有作用域，但用来保存其地址的指针变量是受作用域影响的。**  

## 命名空间和模块化编程
### 命名空间
创建命名空间的方法（注意最末尾不要加分号，和类与结构体不一样）：  
```c++
namespace myNamespace
{
	// 全部东西
}
```
命名空间可以让你使用同一个标识符而不会导致冲突。  
```c++
namespace author
{
	std::string person;
}
namespace programmer
{
	std::string person;
}
```
使用命名空间：  
- std::cout << "fsadfa\n";  
- using namespace std;  //把std命名空间作为全局作用域，不提倡，和命名空间的初衷不一致    
- 用一个using指令只把你需要的特定命名从命名空间提取到全局作用域

如果把所有的函数声明放到前面，它将拥有全局性；如果把它放到某个函数里，那么它将只在这个函数里可以使用。  


### 模块化编程
模块化（modulation）：  
- 把程序划分为多个组成部分（即所谓的“模块”）；  
- 这是通过把程序代码分散到多个文件里，等编译程序时再把那些文件重新组合在一起实现的。  

命名空间（namespace）  
- 相比C语言是C++新增的东西。  

头文件：  
- 只用一个源代码文件来保存程序的全部代码是可行的，但那会给编辑修改工作带来诸多不便。  
- 可以借助C++预编译器和编译器的能力把一个复杂的应用程序划分成多个不同的文件，而仍保持它在内容和功能上的完整。  
- C++预处理器的#include指令提供了一种能够让编译器在编译主程序时把其他文件的内容包括进来的机制。  
- 头文件的基本用途是提供必要的函数声明和类声明。  
- 头文件可以分为**系统文件**和**自定义头文件**。  
- 系统头文件的一个重要作用是保证C++代码的可移植性，确保同样的C++代码在不同的操作系统上做同样的事情。比如Windows的cout和Mac的cout的内部实现不一定一样。    
- 在#include指令里，**系统头文件的文件名要放在尖括号里**，这告诉编译器应该到标准路径寻找这个文件；**自定义头文件的文件名要放到双引号里**。
- 可以用头文件来保存程序的任何一段代码，如类和函数的声明，但一定不要用头文件来保存它们的实现！  
- 与标准的C++源代码相比，在头文件里应该使用更多的注释。至少把它的用途和用法描述清楚。  
- 应该在注释里说明的内容包括
  - 创建日期、文件用途、创建者姓名、最后一次修改日期、有什么限制和前提条件等等。  
  - 头文件里每个类和函数都有一个说明。  
- 自定义的头文件如果没有给出路径名，编译器将到当前子目录以及当前开发环境中的其他逻辑子目录中寻找头文件。  
- 导入自己的头文件可以使用相对路径，比如#include "./utils.h"。  
- 务必注意，Windows通常使用反斜杠作为路径名的分隔符。反斜杠是转义符，所以使用双反斜杠"\\"。  

创建实现文件：  
- 头文件一般只包含类的声明，不包含类的实现代码。  
- 把接口（函数的原型）和实现（函数体的定义）分开是对代码进行模块化的基本原则之一。  

利用C++预处理器，我们可以让头文件只在这个类还没被声明的情况下才声明它。  
建议用预处理的方式注释很多段代码，比起/**/要效果好(因为注释不能嵌套（好像是）)，比如：  
```c++
#if 0
    //
	//
#endif
```

下面这段代码表示，如果UTILS没有定义则定义。 
```c++
#ifndef UTILS 
#define UTILS  
#endif
``` 

## 链接和作用域  
### 作用域
变量的作用域就是你可以在什么范围内访问这个变量。当一个项目有多个文件时，变量的作用域也会受到影响。  

与作用域有关的另一个概念是链接，当你同时编译多个文件时：  
- g++ -o test main.cpp rational.cpp  
 
每个原文件都被称为一个翻译单元，在某个翻译单元里定义的东西在另一个翻译单元里使用正是链接发挥作用的地方。  

**存储类**：每个变量都有一个存储类，它决定着程序将把变量的值存储在计算机的什么地方、如何存储、以及变量有着怎样的作用域。  
- 默认的存储类是auto（自动）。自动变量存储在stack的临时内存里并有着最小的作用域，当程序执行到语句或函数末尾的右花括号时，它们将被系统回收（栈回收）。    
- 与auto不同的是static，static变量在程序的声明周期内将一直保有它的值而不会消亡，因为它们存储在静态存储区。一个static变量可以有external或internal链接。     
- 第三种存储类是extern。它在有多个翻译单元时非常重要。这个关键字用来把另一个翻译单元里的某个变量声明为本单元里的一个同名全局变量。  
- 还要一个存储类是register，它要求编译器把一个变量存储在CPU的寄存器里，但有着与自动变量相同的作用域。这种存储速度最快，但有些编译器可能不允许使用这类变量。  

### 链接
在使用编译器编译程序时，实际上由3个步骤构成：  
1. 执行预处理指令；  
2. 把.cpp文件编译成.o文件；  
3. 把.o文件链接成一个可执行文件。  
   
## 函数模板

C++程序设计范型：  
- 按照面向过程式范型把程序划分成不同的函数；  
- 按照面向对象式范型把代码和数据组织成各种各样的类并建立类之间的继承关系；  
- 泛型编程。支持程序员创建函数和类的蓝图（即模板，template），而不是具体的函数和类。  
	- 这些模板可以没有任何类型：它们可以处理的数据并不仅限于某种特定的数据类型。  
	- 当程序需要用到这些函数中的某一个时，编译器将根据模板即时生成一个能够对特定数据类型进行处理的代码版本。  
	- 泛型编程技术可以让程序员用一个解决方案解决多个问题。  
	- 标准模板库（Standard Template Library，STL）非常重要！它包含了很多有用的数据类型和算法。

**如果某个函数对所有数据类型都进行同样的处理，就应该把它编写为一个模板；如果某个函数对不同的数据类型进行不同的处理，就应该对它进行重载。**
```c++
template <class T>
void swap(T &a, T &b)
{
	T temp = a;
	a = b;
	b = temp;
}
```


## 类模板

类模板与函数模板非常相似：同样是先编写一个类的模板，再由编译器在程序第一次使用这个模板时生成实际代码。  

```c++
template <class T>
class MyClass
{
	MyClass();
	void swap(T &1, T &b);
}
```

## 内联函数
内联（inline）函数从源代码看，有函数的结构，而在编译后，却不具备函数的性质。编译时，类似宏替换，使用函数体替换调用处的函数名。
一般在代码中用inline修饰，但是否形成内联函数，需要看编译器对该函数定义的具体处理。  

```c++
inline int add(int x, int y, int z)
{
	return x+y+z;
}
```
在程序中，调用其函数时，该函数在编译时被替代，而不像一般函数那样是在运行时被调用。  

## 容器和算法

在C++标准库里有许多现成的容器。  

