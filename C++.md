# c++基础

## 1.C++基础知识

### 1.1注释

```c++
/*长注释*/
//短注释
```

### 1.2变量

```c++
//变量创建的语法：数据类型 变量名 =变量初始值
int a =10;
```

### 1.3常量

```c++
//常量定义的两种方式
//1。宏常量
#define  常量名 常量值
#define Day 7 
//2.const 修饰的变量
const 数据类型 变量名 =变量值//不可修改
    const int month =12;
```

### 1.4关键字

**作用：**关键字是C++中预先保留的单词（标识符）

* **在定义变量或者常量时候，不要用关键字**



C++关键字如下：

| asm        | do           | if               | return      | typedef  |
| ---------- | ------------ | ---------------- | ----------- | -------- |
| auto       | double       | inline           | short       | typeid   |
| bool       | dynamic_cast | int              | signed      | typename |
| break      | else         | long             | sizeof      | union    |
| case       | enum         | mutable          | static      | unsigned |
| catch      | explicit     | namespace        | static_cast | using    |
| char       | export       | new              | struct      | virtual  |
| class      | extern       | operator         | switch      | void     |
| const      | false        | private          | template    | volatile |
| const_cast | float        | protected        | this        | wchar_t  |
| continue   | for          | public           | throw       | while    |
| default    | friend       | register         | true        |          |
| delete     | goto         | reinterpret_cast | try         |          |

`提示：在给变量或者常量起名称时候，不要用C++得关键字，否则会产生歧义。`

### 1.5变量命名规则

C++规定给标识符（变量、常量）命名时，有一套自己的规则

* 标识符不能是关键字
* 标识符只能由字母、数字、下划线组成
* 第一个字符必须为字母或下划线
* 标识符中字母区分大小写

> 建议：给标识符命名时，争取做到见名知意的效果，方便自己和他人的阅读

## 2.数据类型

### 2.1整型

**作用**：整型变量表示的是==整数类型==的数据

C++中能够表示整型的类型有以下几种方式，**区别在于所占内存空间不同**：

| **数据类型**        | **占用空间**                                    | 取值范围         |
| ------------------- | ----------------------------------------------- | ---------------- |
| short(短整型)       | 2字节                                           | (-2^15 ~ 2^15-1) |
| int(整型)           | 4字节                                           | (-2^31 ~ 2^31-1) |
| long(长整形)        | Windows为4字节，Linux为4字节(32位)，8字节(64位) | (-2^31 ~ 2^31-1) |
| long long(长长整形) | 8字节                                           | (-2^63 ~ 2^63-1) |

==有一位为符号位==





#### c++在处理终端，文件I/O上的区别

终端操作差别不大

在文件I/O上，差别还是挺大的

```c++
//文件打开形式
ios::in//--打开一个可读文件
ios::out//--打开一个可写入文件
ios::binary//--以二进制形式打开一个文件
ios::app//--写入的所有数据被追加到文件的末尾
ios::trunk//--删除文件原来已有的内容
ios::nocreate//--如果打开的文件并不存在，那么以此参数调用open函数将无法进行
ios::noreplece//--如果要打开的文件已存在，试图用open函数打开将返回一个错误
```

```c++
//对输入数据进行合法性检查
//解决这些问题的办法之一是对cin调用的结果不做任何假设
//cin对象有几个专门用来报告其工作情况的成员函数，它将返回一个真假值来表明cin的状态；
-eof()//如果到达文件（或输入）末尾，返回true;
-fail()//如果cin无法工作，返回ture;
-bad()//如果cin因为比较严重的原因（列如内存不足）而无法工作，返回ture;
-good()//如果以上情况都没有发生，返回ture;
```

#### 函数的重载-overloading



#### 复杂的数据类型

##### 数组

数组需要声明为某一特定的类型：float,char,int;

type name[x];

在c语言里，字符串被实际存储在一个字符数组中；

在c++里我们提供了更好的方法std::string

##### 指针

对于变量我们可以用两种方法来对它进行索引

-通过变量名称

-另一种通过地址

取址操作符&，它的作用就是获得变量的地址；

```c++
int var =123;
std::cout<<"address is :"<<&var;
```

扩展知识：

- 对齐在计算机底层世界处处皆是，内存对齐，文件对齐。（程序在编译连接后被分成一个一个的区块，而区块在文件和文件在内存中要按一定的规律对齐）
  - 一般32位操作系统内存对齐值是：1000H == 4kb
  - 一般64位操作系统内存对齐值是：2000H == 8kb
- 文件的对齐值是：200H
- 变量地址在程序执行期间不会发生变化

指针是用来存放地址的特殊类型变量，一般我们用下面的形式来声明指针变量

——type*pointerName;

```
int *p;
int pp =123;
p =&pp;
int *p1,*p2,*p3;
//另外允许void类型的指针变量
void *p//单纯用来存放一个地址，没有指定指针指向的类型是什么
      //针对一个无类型指针进行解引前，必须先将它转化为一个适当的数据类型（后期详解）



//对指针进行解引号用*好号，即为取出该指针指向的值
std::cout<<*p;
```

数组名对应第一个地址指针

##### 结构

结构对象的基础

定义一个结构的基本语法：

```c++
struct name
{
	type varName1;
	type varName2;
	....

};//别忘记分号
```

指针可以指向任何变量，当然可包括指向结构

指针怎么指向结构的成员呢？

```c++
struct student
{
	std::string name;
	std::string id;
	char sex;
};
student Jiayu={"小甲鱼","fishc_0000", 'M'}
student *pJiayu = &Jiasyu;
//第一可以通过指针进行解引来访问相应的变量值
(*pJiayu).name = "黑夜";
//第二种方法
i.e. ... ... ... ...//(一般在书籍里表示也就是的意思)
pJiayu -> name = "黑夜";
PJiayu -> id = "fishc_00001";
```

#### 函数的传值、传址、传引用

引用（Reference）是 C++ 相对于C语言的又一个扩充。**引用可以看做是数据的一个别名**，通过这个别名和原来的名字都能够找到这份数据。引用类似于 Windows 中的快捷方式，一个可执行程序可以有多个快捷方式，通过这些快捷方式和可执行程序本身都能够运行程序；引用还类似于人的绰号（笔名），使用绰号（笔名）和本名都能表示一个人

引用的定义方式类似于指针，只是用`&`取代了`*`，语法格式为：

```c++
type &name = data
```

type 是被引用的数据的类型，name 是引用的名称，data 是被引用的数据。引用必须在定义的同时初始化，并且以后也要从一而终，不能再引用其它数据，这有点类似于常量（const 变量）

下面是一个演示引用的实例

```c++
#include <iostream>
using namespace std;
int main() {
    int a = 99;
    int &r = a;
    cout << a << ", " << r << endl;
    cout << &a << ", " << &r << endl;
    return 0;
}
```

运行结果：
99, 99
0x28ff44, 0x28ff4

本例中，变量 r 就是变量 a 的引用，它们用来指代同一份数据；也可以说变量 r 是变量 a 的另一个名字。从输出结果可以看出，a 和 r 的地址一样，都是`0x28ff44`；或者说地址为`0x28ff44`的内存有两个名字，a 和 r，想要访问该内存上的数据时，使用哪个名字都行。

注意，引用在定义时需要添加`&`，在使用时不能添加`&`，使用时添加`&`表示取地址。如上面代码所示，第 6 行中的`&`表示引用，第 8 行中的`&`表示取地址。除了这两种用法，`&`还可以表示位运算中的与运算。

由于引用 r 和原始变量 a 都是指向同一地址，所以通过引用也可以修改原始变量中所存储的数据，请看下面的例子：

```c++
#include <iostream>
using namespace std;
int main() {
    int a = 99;
    int &r = a;
    r = 47;
    cout << a << ", " << r << endl;
    return 0;
}
```

运行结果：
47, 47

最终程序输出两个 47，可见原始变量 a 的值已经被引用变量 r 所修改。

如果读者不希望通过引用来修改原始的数据，那么可以在定义时添加 const 限制，形式为：

```c++
const type &name = value;
//也可以是：
type const &name = value
```

##### C++引用作为函数参数

```c++
#include <iostream>
using namespace std;
void swap1(int a, int b);
void swap2(int *p1, int *p2);
void swap3(int &r1, int &r2);
int main() {
    int num1, num2;
    cout << "Input two integers: ";
    cin >> num1 >> num2;
    swap1(num1, num2);
    cout << num1 << " " << num2 << endl;
    cout << "Input two integers: ";
    cin >> num1 >> num2;
    swap2(&num1, &num2);
    cout << num1 << " " << num2 << endl;
    cout << "Input two integers: ";
    cin >> num1 >> num2;
    swap3(num1, num2);
    cout << num1 << " " << num2 << endl;
    return 0;
}
//直接传递参数内容
void swap1(int a, int b) {
    int temp = a;
    a = b;
    b = temp;
}
//传递指针
void swap2(int *p1, int *p2) {
    int temp = *p1;
    *p1 = *p2;
    *p2 = temp;
}
//按引用传参
void swap3(int &r1, int &r2) {
    int temp = r1;
    r1 = r2;
    r2 = temp;
}
```



```c++
//传址
#include <iostream>

void swap(int *x, int *y);//调用时为swap(&x,&y),可以与下面的传引用对比来看
int main()
{
    int x,y;
    std::cout<<"请输入两个不同的值：";
    std::cin>> x >> y;
    
    swap(&x,&y);
    std::cout<<"调换后输出："<< x <<''<< y <<"\n\n";
   return 0; 
}

void swap(int *x, int *y)
{
#if 0//此处用宏用，永远不执行，不用/*   */   #if 1 永远执行
    int temp;
    temp = *x;
    *x = *y;
    *y = temp;
#endif
    *x^ = *y;
    *y^ = *x;
    *x^ = *Y;  
}
```

```c++
//传引用
#include <iostream>

void swap(int &x,int &y);//传引用，当调用此函数时swap(x, y)会自动将x和y的地址传送给函数，而不是值
int main()
{
    int x,y;
    std::cout<<"请输入两个不同的值：";
    std::cin>> x >> y;
    
    swap(x,y);
    std::cout<<"调换后输出："<< x <<''<< y <<"\n\n";
   return 0; 
}

void swap(int &x, int &y)
{
#if 0//此处用宏用，永远不执行，不用/*   */   #if 1 永远执行
    int temp;
    temp = *x;
    *x = *y;
    *y = temp;
#endif
    *x^ = *y;
    *y^ = *x;
    *x^ = *Y;  
}
```

##### C++引用作为函数返回值

```c++
#include <iostream>
using namespace std;
int &plus10(int &r) {
    r += 10;
    return r;
}
int main() {
    int num1 = 10;
    int num2 = plus10(num1);
    cout << num1 << " " << num2 << endl;
    return 0;
}
```

运行结果：
20 20

在将引用作为函数返回值时应该注意一个小问题，就是不能返回局部数据（例如局部变量、局部对象、局部数组等）的引用，因为当函数调用完成后局部数据就会被销毁，有可能在下次使用时数据就不存在了，C++ 编译器检测到该行为时也会给出警告。

更改上面的例子，让 plus10() 返回一个局部数据的引用

```c++
#include <iostream>
using namespace std;
int &plus10(int &r) {
    int m = r + 10;
    return m;  //返回局部数据的引用
}
int main() {
    int num1 = 10;
    int num2 = plus10(num1);
    cout << num2 << endl;
    int &num3 = plus10(num1);
    int &num4 = plus10(num3);
    cout << num3 << " " << num4 << endl;
    return 0;
}
```



#### 联合、枚举和类别名

##### 联合union

```c++
union mima
{
	unsigned long brithday;
	unsigned short ssn;
	char* pet;

};
mima mima_1;//像这样创建一个该类型变量
```

我们可以像对结构成员进行赋值那样对联合里的成员进行赋值，使用同样的语法；

```
mima_1.brithday = 19881301;
```

如果我们再执行下面的语句

```
mima_1.pet = "chaozai";
```

将会把联合里chaozai存入mima_1联合的pet成员，并丢弃birthday成员里的值；

##### 枚举enum

可以用作switch条件语句的case标号——因为字符串是不能作为小标号用的，小技巧

```c++
//例如
int main()
{
	emu weekdays{Monday, Tuesday, Wednesday, Thursday, Friday };
	weekdays today;
	
	today = Mondady;
	std::cout<<today<<"\n";//0
	
	today = Tuesday;
	std::cout<<today<<"\n"//1
	
	switch(today)
	{
	case Monday:
	}

}
```

##### 类型别名 Typedef

```
//我们不喜欢使用int*创建指针，可以像下面这样定义一个类型别名
typedef int* intPointer;
intPointer myPointer;//此之后我们就可以像下面这样来定义整型指针
```

### c++对象

类名第一个字母习惯大写，末尾分号；

类中变量成为属性，函数成为方法；

```
class  Car
{
public:
	std::string color;//声名属性
	std::string engine;
	float gas_tank;
	unsigned int wheel;
	
	void fill_tank(foat liter);//声名方法

};

void Car::fiil_tank(float liter)//作用域解析符，告诉编译器从属何类
{
	gas_tank  += liter;
}
```

c++中不允许对变量进行赋值

绕开这一限制的方法是创建静态常量；

```
class Car
{
	public:
		static const float FuLL_GAS = 85;//一般也不那么做

};
```

类似使用结构的情况，可以在声名某个类的同时，创建一些该类的对象：

```
class Car
{
	....
}car1,car2;//但一般不那么做，不是一个良好的编程习惯
```

#### 构造器和析构器

##### 构造器

类里的一种特殊方法；

- 构造器和通常方法的主要区别：
  - 构造器的名字和它所属类的名字一样
  - 系统在创建某个类的实例时会第一时间调用这个类的构造器
  - 构造器永远不会返回任何值
- 创建构造器，需要先把它的声明添加到类里：

```
class Car
{
	Car(void);

};

Car::Car(void)//声明结束后开始定义构造器本身；
{
	color = "WHITE";
	engine = "V8";
	wheel = 4;
	gas_tank = Full_GAS;
}
```

每个类至少有一个构造器，如果没有在类里定义一个构造器的话，编译器就会使用如下语法代替你定义一个：

```
ClassName::ClassName(){};
```

构造器（构造函数的三种写法）

无参构造函数

```c++
//无参构造函数
#include <iostream>
using namespace std;

class Student {
public:
    int m_age;
    int m_score;

    // 1. 无参构造函数
    Student() {
        m_age = 18;
        m_score = 99;
        cout << "1. 无参构造函数" << endl;
    }
};
```

一般构造函数有两种写法

- 初始化列表：以一个冒号开始，接着是以逗号分隔的数据成员列表，每个数据成员后面跟一个放在括号的初始化值。
- 内部赋值：正常函数赋值

C++规定，对象的成员变量的初始化动作发生在进入构造函数本体之前。也就是说采用初始化列表的话，构造函数本体实际上不需要有任何操作，因此效率更高

```c++
//一般构造函数
#include <iostream>
using namespace std;

class Student {
public:
    int m_age;
    int m_score;

    // 2. 一般构造函数
    // 初始化列表方式
    Student(int age, int score) :
        m_age(age),
        m_score(score)
        {}

    // 内部赋值方式
    Student(int age, int score) {
        m_age = age;
        m_score = score;
    }
};
//一般构造函数可以有多种参数形式，即一个类可以有多个一般构造函数，前提是参数的个数或者类型不同（C++的函数重载机制)
```

复制构造函数

复制构造函数参数为类对象本身的引用，根据一个已存在的对象复制出一个新的对象，一般在函数中会将已存在对象的数据成员的值复制一份到新创建的对象中

```c++
#include <iostream>
using namespace std;

class Student {
public:
    int m_age;
    int m_score;

    // 3. 复制构造函数
    Student(Student& s) {
        m_age = s.m_age;
        m_score = s.m_score;
        cout << "3.  复制构造函数" << endl;
    }
};
```

注意：若没有显示定义复制构造函数，则系统会默认创建一个复制构造函数，当类中有指针成员时，由系统默认创建的复制构造函数会存在“浅拷贝”的风险，因此必须显示定义复制构造函数。

- 浅拷贝指的是在对对象复制时，只对对象中的数据成员进行简单的赋值，若存在动态成员，就是增加一个指针，指向原来已经存在的内存。这样就造成两个指针指向了堆里的同一个空间。当这两个对象生命周期结束时，析构函数会被调用两次，同一个空间被两次free，造成野指针。
- 深拷贝就是对于对象中的动态成员，不是简单的赋值，而是重新分配空间



##### 析构器

在创建对象时，系统都会自动调用一个特殊的方法，即构造器；

相应的，在销毁一个对象时，系统也应该会调用另一个特殊的方法达到对应效果——析构器

一般来说，构造器用来完成事先的初始化和准备工作（申请分配内存），析构器用来完成事后所必须得清理工作（清理内存）

```
class Car
{
	Car(void);//构造器
	~Car();//析构器
}
```

析构器不带参数，所以析构器的声明永远是如下格式：~ClassName();在一些复杂的程序中，析构器往往至关重要可能引起内存的泄露；

##### 构造对象数组，

数组可以是任何一种数据类型，当然包

```
Car mycar[10];
//调用语法依旧是
mycar[x].running;//x为数组下标
```

this指针

一个例子：

```
class Human
{
	char fishc;
	Human(char fishc);
};
Human::Human(char fishc)
{
	fishc = fishc;
}
```

上述代码可能会出现一个问题，是构造器不知道哪个是参数，哪个是属性；

这时候可以用this指针

```c++
this ->fishc = fishc;
```

左侧为当前对象的fishc属性，右侧为构造器传入的fishc参数；

如果代码不存在隐患就不用使用；

this指针还有一些更复杂的应用，在此不再详述，详情请看书；

#### 类的继承

基类和子类

现在编写一个Animal类作为Turtle类和Pig类的基类；

- 基类：
  - 基类是可以派生出其他的类，也成为父类或者超类；比如这里的Animal类就是基类；
- 子类：
  - 子类是从基类里派生出来的类，比如这里的Turtle类和Pig类都是子类；

![image-20220818220143038](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220818220143038.png)

![image-20220818220242782](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220818220242782.png)

```
#include <iostream>
#include <string>

class Animal
{
public:
	std::string mouth;
	
	void eat();
	void sleep();
	void drool();
	
};

class Pig:public Animal
{
public:
	void climb();
};


class Turtle:public Animal
{
public:
	void swim();
};
void Anima::eat()
{
	std::cout<<"I am eating!"<<endl;
}

void Animal::sleep()
{
	std::cout<<"I am sleeping Don't bother me"<<endl;
}

void 
```

##### 继承机制中的构造器和解析器







```
#include <iostream>
#include <string>


class BaseClass
{

public:
	BaseClass();
	~BaseClass();

	void doSomething();

};

class Subclass : public BaseClass
{
public:
	Subclass();
	~Subclass();
};


BaseClass::BaseClass()
{

	std::cout << "进入基类构造器。。。\n";
	std::cout << "我在基类构造器里。。。\n";
}


BaseClass::~BaseClass()
{

	std::cout << "进入基类析构器。。。\n";
	std::cout << "退出基类析构器。。。\n";
}

void BaseClass::doSomething()
{
	std::cout << "我干了某些事情\n";

}


Subclass::Subclass()
{
	std::cout << "进入子类构造器。。。\n";
	std::cout << "我在子类构造器里做了某些事情。。。\n";

}

Subclass::~Subclass()
{
	std::cout << "进入子类析构器。。。\n";
	std::cout << "我在子类析构器里做了某些事情。。。\n";

}
int main()
{
	Subclass subclass;
	subclass.doSomething();
	std::cout << "完事收工\n";

	return 0;

}
```



新手要注意的地方

类之间的继承原则是，自然而然的例如：

人在human类里有一个swim（）方法，当在设计一条鱼时，也想要swim（）方法，但你不应该用human去派生，虽然这在语法逻辑上说得过去；

构造器的设计越简明越好，应该只用它来初始化有关属性；

##### 访问控制

访问级别

|   级别    |     允许谁来访问     |
| :-------: | :------------------: |
|  public   |       任何代码       |
| protected | 这个类本身和它的子类 |
|  private  |    只有这个类本身    |

编写代码时先从public: 开始然后是protected: 最后是private： 

对于从基类继承来的方法和属性保护

```c++
class Pig:public Animal{...}
```

- public是告诉编译器：继承的方法和属性的访问级别不发生任何改变—即public仍然可以被所有代码访问，protected 只能由基类的子类访问就，privat则只能由基类本身访问。
- protected 把基类访问级别改为protected.如果原来是public的话。这将使得这个子类外部代码无法通过子类访问基类中的public
- private则是告诉每一个成员从基类继承来的都当做private来对待

。。。。一般情况下只用public而已！

##### 覆盖方法

只需要在子类里再次声明就好，然后进行子类函数的重新定义

下面的例子说明覆盖eat()的方法；

```c++
#include <iostream>
#include <string>

class Animal
{
public:
	std::string mouth;
	
	void eat();
	void sleep();
	void drool();
	
};

class Pig:public Animal
{
public:
	void climb();
	void eat();//重新声明
};


class Turtle:public Animal
{
public:
	void swim();
};

void Anima::eat()//父类eat()方法
{
	std::cout<<"I am eating!"<<endl;
}

void Animal::sleep()
{
	std::cout<<"I am sleeping Don't bother me"<<endl;
}

void Pig::eat()
{
    Animal::eat();//不一定非要定义一个类后才可以调用类的方法；我们在此调用
    std::cout<<"正在吃鱼\n\n";
}
```

重载方法可以定义多个同名的方法（函数），只是他们的输入参数必须不同。因为编译器是依靠不同的输入参数来区分不同的方法。

注意：

- 对方法（函数）进行重载一定要有放矢，重载的方法（函数）越多，程序就越不容易看懂。
- 对方法进行覆盖（注意区分覆盖和重载）时一定要看仔细，因为只要输入的参数和返回值与原来的不一致，你编写出来的程序就将是一个重载方法不是覆盖方法。这种错误一般很难发现；
- 对于基类继承来的方法进行重载，程序永远不会像你预期的那样工作！

##### 友元关系

由于想要在某些应用场合，一个完全无关的类由于某些特殊原因需要访问到某个protected成员，甚至某个privated成员，那这样引出了一种特殊的需求，友元关系因此诞生；

友元关系是类之间的一种特殊关系，这种关系不仅允许友元类访问对方的public方法和属性，还允许友元访问对方的protected和private方法和属性。

- 使用方法
  - 只需要在类声明里的某个地方加上一条friend class **就行了。这条语句可以放在任何地方；

```
class Lovers
{

public:
	Lovers(std::string theName);
	void kiss(Lovers*lover);
	void ask(LOvers *lover, std::string something);

protected:
	std::string name;
	
	friend calss Others;//关联友元，这样Others类可以访问到 protected属性

}
```

##### 静态属性和静态方法

c++允许我们把一个或多个成员声明为属于某个类，而不是是属于该类的对象

好处优点：

- 程序员可以在没有创建任何对象的情况下拥有相关的方法

- 还能够让有关的数据仍然在该类的所有空间对象共享
- 创建一个静态属性和静态方法：
  - 只需要在它的声明前加上static保留字即可

举例:
比如现在需要统计一下有多少只活的动物,那么我们需要一个计数器数量：每诞生一只宠物,就给宠物计数器加上1,每死掉一只,就减去1,此时我们首先想到的是创建一个全局变量来充当这个计数器,但这么做的后果是程序中的任何代码都可以修改这个计数器,稍不小心就会在程序里留下一个难以查堵的漏洞

所以坚决不建议在非必要的时候声明全局变量,我们真正需要的是一个只有在创建或删除对象时候才允许访问的计数器

这个问题必须使用C++的静态属性和静态函数才能完美地得到解决，C++允许我们把一个或多个成员声明为属于某个类，而不是仅属于该类实例化出的某个对象这么做的好处在于程序员可以在没有创建任何对象的情况下调用有关的方法 而且 有关数据仍能在该类的所有对象（静态和非静态皆可）之间共享
原文链接：https://blog.csdn.net/Chroniccandy/article/details/108621102

```c++
calss Pet
{
public:
	pet(std::string theName);
	~pet();
	
	static int getCount();
	
protected:
	std::string name;
private:
	static int count;
	
};

class Dog : public Pet
{
public:
	Dog(std::string theName);
	
};

class Cat:public Pet
{
public:
	Cat(std::string theName);
	
};
int Pet::cout = 0;  //这一句做了两件事，1让编译器分配内存，2是让变量初始化为0


Pet::Pet(std::string theName)
{
    name = theName;
    count++;
    
    std::cout<<"一只宠物出生了，他的名字叫："<<name<<"\n";
    
}
Pet::~Pet()
{
    count--;
    std::cout<<name<<"挂掉了\n";
} 

int Pet::getCount()
{
    return count;
    
}
    
Dog::Dog(std::string theName):Pet(theName)
{
    
}
    
Cat::Cat(std::string theName):Pet(theName)
{
    
}
int main（）
{
    Dog dog("Tom");
    Cat cat("Jerry");
    
    std::cout<<"\n已经诞生了"<<Pet::getCount()<<"只宠物！\n\n";
    {
        Dog dog_2("Tom_2");
        Cat cat_2("Jerry_2");
        
        std::cout<<"现在呢已经诞生了"<<pet::getCount()<<"只宠物\n\n";
        
    }
     std::cout<<"现在呢已经诞生了"<<pet::getCount()<<"只宠物\n\n";
    
    return 0;
}
```

静态方法的使用一般使用：ClassName::methodName();不要使用：objectName.methodName();因为这样会让你很容易产生混淆；

##### 虚方法

认识两个新的c++保留字new和delete

```
int *pointer=new int;//创建一个整型名字叫pointer的指针，用new方法给它分配一块int型的内存（4个字节的空间）
*pointer = 110;
std::cout<<*pointer;
delete pointer;
//最后一步非常关键的必要，因为程序不会自动释放内存，程序中每一个new操作都必须有一个与之对应的delete操作
```

```c++
int main()
{

    Pet*cat = new Cat("加菲");
    Pet*dog = new Dog("欧迪");
    
    cat->sleep();
    cat->eat();
    cat->paly();
    
    dog->sleep();
    dog->eat();
    dog->paly();
    
    delete cat;
    delete dog;
    
    return 0;
}

```

//C++允许我们定义一个基类的指针指向子类的数据空间,但当子类中存在覆盖基类的方法时，我们想用指针调用子类的方法，就会出现问题，结果是调用了基类的方法,在编译的时候，编译器会为认为这里是一个BaseClass型的指针，因此也就认为指针中的test方法是基类的方法。

为了解决上述问题——使用虚方法

声名一个虚方法就是在方法的原型上前面加virtual保留字即可

```c++
virtual void play();
```

如果方法是通过引用或指针（而不是对象）调用的， 如果没有关键字 virtual， 程序根据**引用或指针的类型**选择方法； 如果使用了关键字 virtual， 程序根据引用或指针指向的**对象类型**选择方法。举例

```c++
#include <iostream>
using namespace std;

class Base
{
    public:
        Base(int _x):x(_x)
        {

        }
        virtual int get()//
        {
            cout<<"Base的get"<<endl;
            return x;   
        }   
    private:
        int x;
};

class Derived:public Base
{
    public:
        Derived(int _y):Base(_y),y(_y)
        {

        }
        int get()
        {
            cout<<"Derived的get"<<endl;
            return y;
        }
    private:
        int y;
};

int main()
{
    Base *a=new Derived(5);
    cout<<a->get()<<endl;
    return 0;
}
//若基类没有virtual声明，其结果为
//Base的get
//5
//若基类中含有virtual声明，其结果为
//Derived的get
//5
```



另外虚方法是继承的，一旦在基类里把某个方法声名为虚方法，在子类里就不可能再把它声名为一个非虚方法了

虚方法只会把程序变慢一点点，没有其他什么坏处

tips one

- 如果拿不准要不要把某个方法声名为虚方法，那么就把它声名为虚方法

tips two

- 在基类里把所有的方法都声名为虚方法会让程序变得慢一点，但好处是可以让程序符合你的行为预期

tips three

- 在实现一个多层次类的继承关系时，最顶级的基类应该只有虚方法

tips four

- 析构器是虚方法



**抽象方法**

抽象方法（abstract method,也可以成为**纯虚函数**）是面向对象编程技术的另一核心概念，在设计一个多层次的类继承关系时常会用到

**抽象方法的应用场景：**

把某个方法声名为一个抽象方法**就是告诉编译器这个方法必不可少，但我现在在这个基类里还不能为它提供一个实现！**

抽象方法的语法：

```c++
//在声名一个虚方法的基础上，在原型的末尾加上“=0”告诉编译器不用浪费时间在这个类里寻找这个方法的实现！
```

```c++
class Pet
{
public:
    Pet(std::string theName);
    
    virtual void eat();
    virtual void sleep();
    virtual void play()=0;
    
protected:
    std::string name;
}
```

##### 多态性

c++如何实现多太性的呢？

- 编译时的多态性：通过重载实现
- 运行时的多态性：通过虚函数实现

动态多态发生在继承关系的类中，通过***\*虚函数表\****实现

静态多态是发生在编译时期的，通过**模板和函数重载**实现，相比动态多态不需派生关系

编译时的多态性特点是运行速度快，运行时的特点是高度灵活和抽象

**延申拓展：显示接口和隐士接口**

显示接口就是指能够明确来源的接口，比如在动态多态的范例中，当调用getMax时，我们能够知道这个getMax到底是CBase的还是CChild的

隐式接口就是指那些无法确定的来源的接口，如对于函数重载和模板，我们也不知道调用的是哪个实现。

具体可参考CSDN文章：
原文链接：https://blog.csdn.net/weixin_43935710/article/details/103871715



##### 运算符的重载



运算符重载的函数格式：

```
函数类型 operator 运算符名称（形参列表）
{
	对运算符的重载处理
}

//例如对加号实现重载
int operator +(int a, int b)
{
	return(a-b);
}
```

c++不允许用户自己定义新的运算符，只有对已有的c++运算符进行重载

除了以下5个运算符号不允许重载，其他运算符允许重载：

- .成员访问运算符号
- *成员指针运算符
- ::域运算符
- sizeof 尺寸运算符
- ?:条件运算符

tips:

千万不要因为你会这么做而这么做，一定是迫不得已的时候才那么做，进行操作符的重载；

重载操作符，是为了让代码更容易阅读；

在重载操作符时，千万不要让它失去原始的意义，例如：你完全重载加号让它变成减号这无非是被开除

***重载的话把这个例子看明白了就明白了***

```c++
#include <iostream>
#include <string>
#include <stdlib.h>

class Rational
{
public:
	Rational(int num, int denom);//num =分子，denom =分母

	Rational operator+(Rational rhs);// rhs = right hand side
	Rational operator-(Rational rhs);
	Rational operator *(Rational rhs);
	Rational operator /(Rational rhs);

	void print();

private:
	void normalize();//负责对分数进行化简处理

	int numerator;//分子
	int denominator;//分母
	//类名&  为c++中的类引用操作
	friend std::ostream& operator<<(std::ostream& os, Rational f);
	//第一个参数os是指向将要向它写的那个流，以引用传递的方式进行
	//第二个参数是打算写到数据流中的数据
	//运用友元进行操作，因为重载的不属于Rational 但要对rational中的pirvate属性
};

Rational::Rational(int num, int denom)
{
	numerator = num;
	denominator = denom;

	normalize();

}

//noramlize()对分数进行简化操作
//只允许分子为负数，如果分母为负数则把负数挪到分子部分如1/-2=-1/2
//允许欧几里得算法（辗转求余原理）将分数进行简化；2/10=1/5


void Rational::normalize()
{
	//确保分母为正
	if (denominator < 0)
	{
		numerator = -numerator;
		denominator = -denominator;

	}

	//欧几里得算法（辗转求余原理）
	int a = abs(numerator);
	int b = abs(denominator);

	while(b>0)
	{
		int t = a % b;// 4%16 1.t=4,a=b=16,b=t=4;b>0  -->;
		              //16%4  2.t=0,a=b=4,b=t=0
		a = b;
		b = t;
	}
	//分子、分母分别处以最大公约数得到最简化分数

	numerator /= a;
	denominator /= a;
}



Rational Rational::operator+(Rational rhs)
{
	int a = numerator;
	int b = denominator;
	int c = rhs.numerator;
	int d = rhs.denominator;

	int e = a * d + c * b;
	int f = b * d;

	return Rational(e, f);

}

//减去一个数等于加上这个数的相反数
Rational Rational::operator-(Rational rhs)
{
	rhs.numerator = -rhs.numerator;

	return operator+(rhs);

}

Rational Rational::operator*(Rational rhs)
{
	int a = numerator;
	int b = denominator;
	int c = rhs.numerator;
	int d = rhs.denominator;

	int e = a * c;
	int f = b * d;

	return Rational(e, f);




}


//除一个数等于乘它的倒数
Rational Rational::operator/(Rational rhs)
{
	int t = rhs.numerator;
	rhs.numerator = rhs.denominator;
	rhs.denominator = t;

	return operator*(rhs);

}

void Rational::print()
{
	if (numerator % denominator == 0)
		std::cout << numerator / denominator;
	else
		std::cout << numerator << "/" << denominator;

}

std::ostream& operator<<(std::ostream& os, Rational f);

int main()
{
	Rational f1(2, 16);
	Rational f2(2, 8);

	/*Rational res = f1 + f2;
	f1.print();
	std::cout << "+";
	f2.print();
	std::cout << "=";
	res.print();
	std::cout << "\n";*/

	//重载了左移操作符号就不再需要使用类里的print()函数

	
	std::cout << f1 << "+" << f2 << "==" << (f1 + f2) << "\n";
	std::cout << f1 << "-" << f2 << "==" << (f1 - f2) << "\n";
	std::cout << f1 << "*" << f2 << "==" << (f1 * f2) << "\n";
	std::cout << f1 << "/" << f2 << "==" << (f1 / f2) << "\n";

	return 0;

}


std::ostream& operator<<(std::ostream& os, Rational f)
{
	os << f.numerator << "/" << f.denominator;
	return os;

}
```

##### 多继承

multiple inheritance 可能是面向对象编程技术中最另人争议的功能

什么时候要用到多继承？

---

- 是要你遇到问题无法只用“是一个”关系来表达的时候，就是多继承出场地时候

- 例如：学生和老师都是人，这时可以创建一个person类和teacher类和student类，teacher和student继承person类

- 但如果出现了一个助教，同时存在两个“是一个”关系，这时我们需要写一个TeachingStudent类让它同时继承Teacher类和Student类,即使用多继承

  基本语法：

  

  ```c++
  calss TeachingStudent:public Student,public Teacher
  {
  	...
  }
  ```

写析构器时可以这么写 

```c++
TeachingStudent::TeachingStudent(std::string theName,std::string classTeaching,std::string classAttending):Teacher(theName, calssTeaching),Student(theName,classAttending)//此处的用法为，多继承助教老师，析构器直接调用继承的Teacher类和Student类的析构器实现的
```

##### 虚继承

多继承的派生类继承了所有父类的成员。尽管概念上非常简单，但是多个基类的相互交织可能会带来错综复杂的设计问题，命名冲突就是不可回避的一个

![image-20220904194705552](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220904194705552.png)

在一个派生类中保留间接基类的多份同名成员，虽然可以在不同的成员变量中分别存放不同的数据，但大多数情况下这是多余的：因为保留多份成员变量不仅占用较多的存储空间，还容易产生命名冲突。假如类 A 有一个成员变量 a，那么在类 D 中直接访问 a 就会产生歧义，编译器不知道它究竟来自 A -->B-->D 这条路径，还是来自 A-->C-->D 这条路径。

```c++
//间接基类A
class A{
protected:
    int m_a;
};
//直接基类B
class B: public A{
protected:
    int m_b;
};
//直接基类C
class C: public A{
protected:
    int m_c;
};
//派生类D
class D: public B, public C{
public:
    void seta(int a){ m_a = a; }  //命名冲突
    void setb(int b){ m_b = b; }  //正确
    void setc(int c){ m_c = c; }  //正确
    void setd(int d){ m_d = d; }  //正确
private:
    int m_d;
};
int main(){
    D d;
    return 0;
}
//这段代码实现了上图所示的菱形继承，第 25 行代码试图直接访问成员变量 m_a，结果发生了错误，因为类 B 和类 C 中都有成员变量 m_a（从 A 类继承而来），编译器不知道选用哪一个，所以产生了歧义
```

为了消除歧义，我们可以在 m_a 的前面指明它具体来自哪个类：

```c++
void seta(int a)
{
    B::m_a=a;
}
//或者
void seta(int a)
{
    C::m_a=a;
}
```

为了解决多继承时的命名冲突和冗余数据问题，[C++](http://c.biancheng.net/cplus/) 提出了虚继承，使得在派生类中只保留一份间接基类的成员。在继承方式前面加上 virtual 关键字就是虚继承，请看下面的例子:

```c++
//间接基类A
class A{
protected:
    int m_a;
};
//直接基类B
class B: virtual public A{  //虚继承
protected:
    int m_b;
};
//直接基类C
class C: virtual public A{  //虚继承
protected:
    int m_c;
};
//派生类D
class D: public B, public C{
public:
    void seta(int a){ m_a = a; }  //正确
    void setb(int b){ m_b = b; }  //正确
    void setc(int c){ m_c = c; }  //正确
    void setd(int d){ m_d = d; }  //正确
private:
    int m_d;
};
int main(){
    D d;
    return 0;
}
```

这段代码使用虚继承重新实现了上图所示的菱形继承，这样在派生类 D 中就只保留了一份成员变量 m_a，直接访问就不会再有歧义了。

虚继承的目的是让某个类做出声明，承诺愿意共享它的基类。其中，这个被共享的基类就称为虚基类（Virtual Base Class），本例中的 A 就是一个虚基类。在这种机制下，不论虚基类在继承体系中出现了多少次，在派生类中都只包含一份虚基类的成员

##### 错误处理和调试

有些错误问题例如：计算阶乘超出了计算机所能表达的最大整数（在你的电脑上）

对于这类问题我们可以使用climits头文件

- climits头文件？
  - 这个头文件是从c的limits.h头文件引用过来的，主要列出了各种数据类型在给定操作系统上的取值范围，并且把每种数据类型的最大可能和最小可能取值分别定为为一个常量供我们比较。
  - 比如，SHORT_MAX代表短整数类型在给定系统上的最大可能取值，SHORT_MIN代表短整数类型在给定操作系统上的最小可能取值。USHORT_MAX代表无符号整数的最大可能取值
- 如下代码

```c++
#include<iostream>
#include<climits>

class Factorial
{
public:
	Factorial(unsigned short num);
	unsigned long getFactorial();
	bool inRange();
private:
	unsigned short num; 

	
};

Factorial::Factorial(unsigned short num)
{
	this->num = num;//左为类num属性，右为num形参
}

 unsigned long Factorial::getFactorial()
{
	unsigned long sum = 1;
	
	for (int i = 1; i <= num; i++)
	{
		sum *= i;
	}
	return sum;
}

bool Factorial::inRange()
{
	unsigned long max = ULONG_MAX;
	for (int i=num; i >= 1; i--)
	{
		max /= i;
	}
	if (max < 1)
		return false;
	else
		return true;


}

int main()
{
	unsigned short num = 0;

	std::cout << "请输入一个整数";
	std::cin >> num;

	Factorial fac(num);

	if (fac.inRange())
	{
		std::cout << num << "的阶乘是" << fac.getFactorial() << "\n";

	}
	else
	{
		std::cout << "您所输入的值太大！\n";
	}

	return 0;
	
	
	return 0;

}
```

- 有些程序员喜欢使用异常而不是return语句
- 上述例子中return语句的使用其实是不好的，因为把各种错误代码进行语言处理的语句混杂在程序主干部分既不利于模块化编程，又容易干扰正常思考；

##### assert（）函数

c++和c都有一个专门为调试准备的工具函数，就是assert()函数

这个函数是在c语言的assert.h库文件里定义的，所以包含到c++里我们用以下语句#include<cassert>

assert()函数需要一个参数，它将测试这个输入参数的真or假状态，如果为真，do nothing为假就do something

##### 捕获异常

异常（exception)就是与预期不想符合的反常现象

基本使用思路:

C++ 通过 throw 语句和 try...catch 语句实现对异常的处理。throw 语句的语法如下

```c++
throw  表达式
```

该语句拋出一个异常。异常是一个表达式，其值的类型可以是**基本类型**，也可以是类。

try...catch 语句的语法如下：

```c++
try {
    语句组
}
catch(异常类型) {
    异常处理代码
}
...
catch(异常类型) {
    异常处理代码
}
```

catch 可以有多个，但至少要有一个。

不妨把 try 和其后`{}`中的内容称作“try块”，把 catch 和其后`{}`中的内容称作“catch块”。

try...catch 语句的执行过程是：

- 执行 try 块中的语句，如果执行的过程中没有异常拋出，那么执行完后就执行最后一个 catch 块后面的语句，所有 catch 块中的语句都不会被执行；
- 如果 try 块执行的过程中拋出了异常，那么拋出异常后立即跳转到第一个“异常类型”和拋出的异常类型匹配的 catch 块中执行（称作异常被该 catch 块“捕获”），执行完后再跳转到最后一个 catch 块后面继续执行。

```c++
#include <iostream>
using namespace std;
int main()
{
    double m ,n;
    cin >> m >> n;
    try {
        cout << "before dividing." << endl;
        if( n == 0)
            throw -1; //抛出int类型异常
        else
            cout << m / n << endl;
        cout << "after dividing." << endl;
    }
    catch(double d) {
        cout << "catch(double) " << d <<  endl;
    }
    catch(int e) {
        cout << "catch(int) " << e << endl;
    }
    cout << "finished" << endl;
    return 0;
}

```

//程序的运行结果如下：
//9 6↙
//before dividing.
//1.5
//after dividing.
//finished

说明当 n 不为 0 时，try 块中不会拋出异常。因此程序在 try 块正常执行完后，越过所有的 catch 块继续执行，catch 块一个也不会执行。

程序的运行结果也可能如下：
9 0回车
before dividing.
catch\(int) -1
finished说明当 n 不为 0 时，try 块中不会拋出异常。因此程序在 try 块正常执行完后，越过所有的 catch 块继续执行，catch 块一个也不会执行。

程序的运行结果也可能如下：
9 0回车
before dividing.
catch\(int) -1
finished

当 n 为 0 时，try 块中会拋出一个整型异常。拋出异常后，try 块立即停止执行。该整型异常会被类型匹配的第一个 catch 块捕获，即进入`catch(int e)`块执行，该 catch 块执行完毕后，程序继续往后执行，直到正常结束。

如果拋出的异常没有被 catch 块捕获，例如，将`catch(int e)`，改为`catch(char e)`，当输入的 n 为 0 时，拋出的整型异常就没有 catch 块能捕获，这个异常也就得不到处理，那么程序就会立即中止，try...catch 后面的内容都不会被执行

#### 能够捕获任何异常的 catch 语句

如果希望不论拋出哪种类型的异常都能捕获，可以编写如下 catch 块

```c++
catch(...) {
    ...
}
```

这样的 catch 块能够捕获任何还没有被捕获的异常。例如下面的程序

```c++
#include <iostream>
using namespace std;
int main()
{
    double m, n;
    cin >> m >> n;
    try {
        cout << "before dividing." << endl;
        if (n == 0)
            throw - 1;  //抛出整型异常
        else if (m == 0)
            throw - 1.0;  //拋出 double 型异常
        else
            cout << m / n << endl;
        cout << "after dividing." << endl;
    }
    catch (double d) {
        cout << "catch (double)" << d << endl;
    }
    catch (...) {
        cout << "catch (...)" << endl;
    }
    cout << "finished" << endl;
    return 0;
}
```

程序的运行结果如下：
9 0↙
before dividing.
catch (...)
finished

当 n 为 0 时，拋出的整型异常被`catchy(...)`捕获。

程序的运行结果也可能如下：
0 6↙
before dividing.
catch (double) -1
finished

当 m 为 0 时，拋出一个 double 类型的异常。虽然`catch (double)`和`catch(...)`都能匹配该异常，但是`catch(double)`是第一个能匹配的 catch 块，因此会执行它，而不会执行`catch(...)`块。

由于`catch(...)`能匹配任何类型的异常，它后面的 catch 块实际上就不起作用，因此不要将它写在其他 catch 块前面。

#### 函数的异常声明列表

为了增强程序的可读性和可维护性，使程序员在使用一个函数时就能看出这个函数可能会拋出哪些异常，C++ 允许在函数声明和定义时，加上它所能拋出的异常的列表，具体写法如下：

```c++
void func() throw (int, double, A, B, C);
```

或

```c++
void func() throw (int, double, A, B, C){...}
```



上面的写法表明 func 可能拋出 int 型、double 型以及 A、B、C 三种类型的异常。异常声明列表可以在函数声明时写，也可以在函数定义时写。如果两处都写，则两处应一致。

如果异常声明列表如下编写：

```c++
void func() throw ();
```

则说明 func 函数不会拋出任何异常。

一个函数如果不交待能拋出哪些类型的异常，就可以拋出任何类型的异常。

函数如果拋出了其异常声明列表中没有的异常，在编译时不会引发错误，但在运行时， Dev C++ 编译出来的程序会出错；用 Visual Studio 2010 编译出来的程序则不会出错，异常声明列表不起实际作用。

稍微一点复杂程序

```c++
#include<iostream>
#include<climits>

unsigned long returnFactorial(unsigned short num)throw(const char*);

int main()
{
	unsigned short num = 0;
	std::cout << "请输入一个整数：";
	while (!(std::cin >> num) || (num < 1))
	{
		std::cin.clear();
		std::cin.ignore(100, '\n');
		std::cout << "请输入一个整数：";
	}
	std::cin.ignore(100, '\n');

	try
	{
		unsigned long factorial = returnFactorial(num);
		std::cout << num << "的阶乘是：" << factorial;

	}
	catch (const char*e)
	{
		std::cout << e;
	}

	return 0;
}

unsigned long returnFactorial(unsigned short num)throw(const char*)
{
	unsigned long sum = 1;
	unsigned long max = ULONG_MAX;

	for (int i = 1; i <= num; i++)
	{
		sum *= i;
		max /= i;

	}
	if (max < 1)
	{
		throw"悲催。。。该基数太大，无法在该计算机求出阶乘值\n";
	}
	else
	{
		return sum;
	}

}
```

#### 动态内存管理

- **静态内存**就是平时一直使用的东西，变量（包括指针变量）、固定长度数组、某给定类的对象。在程序中，我们可以使用他们的名字或地址来访问使用他们。
- 使用静态内存的最大弊端是，你不得不在程序编写时为有关变量分配一块尽可能大的内存（防止不够存放数据）一旦程序开始运行，不管实际情况如何，变量所占内存无法改变。
- **动态内存**只由地址的内存块构成，没有名字，在程序运行期间动态分配。它是由标准c++库替你管理——内存池用new语句，如果没有足够的内存空间可用申请，new语句将抛出std::bad_alloc异常！
- 在用完内存块后，应该用delete语句把它还给内存池。另外作为一种附加的保险措施，在释放内存块后还应该把与之关联的指针设置为NULL；

```c++
int *i = new int;
```

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220907213125947.png" alt="image-20220907213125947" style="zoom:50%;" />

```c++
delete i;
```

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220907212917779.png" alt="image-20220907212917779" style="zoom:50%;" />

```C++
i = NULL;
```

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220907213018494.png" alt="image-20220907213018494" style="zoom:50%;" />

有一个特殊的地址叫做NULL指针。当把一个指针变量设置为NULL时，它的含义是那个指针不再指向任何东西

```c++
int* x;
x =NULL;//这时候啥都不指向
```

在使用delete释放内存后，指针会保留一个毫无意义的地址，我们要将指针变量赋值为NULL;

- 注意，最重要的原则之一是每一条new语句都必须有一条与之配对的delete语句，没有配的delete语句或有两个配对delete语句都属于编程漏洞。可能导致内存泄露；

```c++
#include<iostream>
#include<string>

class Company
{
public:
	Company(std::string theName);
	virtual void printInfor();

protected:
	std::string name;

};


class TechCompany :public Company
{
public:
	TechCompany(std::string theName, std::string product);
	virtual void printInfor();

private:
	std::string product;
};


Company::Company(std::string theName)
{
	name = theName;
}

void Company::printInfor()
{
	std::cout << "这个公司的名字叫做：" << name << "。\n";

}

TechCompany::TechCompany(std::string theName, std::string product) :Company(theName)
{
	this->product = product;
}
void TechCompany::printInfor()
{
	std::cout << name << "公司大量生产了：" << product << "这款产品\n";

}

int main()
{

	Company *company = new Company("APPLE");
	company->printInfor();

	delete company;
	company = NULL;

	company = new TechCompany("APLLE", "iphone");
	company->printInfor();

	delete company;
	company = NULL;
	return 0;
}

```

#### 动态数组

 **数组**是一种顺序存储的数据结构，在定义数组时，首先要确定数组的大小。静态数组在编译时就需要确定数组的大小，所以，为了防止内存溢出，我们尽量将数组定义的大一些，但是这样太过浪费内存。

 **动态数组则**不同，它不需要在编译时就确定大小，它的大小在程序运行过程中确定，所以可以根据程序需要而灵活的分配数组的大小，相比静态数组，它更“灵活”、“自由”。但是动态数组需要进行显式的内存释放

- **动态数组内存分配**
  -    动态数组进行内存分配的格式为new T[size]，size可以不是常量表达式；如下面的例子所示：

```c++
int size =10;
int *Dynamic_Arr2 = new int[size];//为初始化
```

可以看出，虽然我们分配了一个动态数组，其实返回的是一个T类型的指针，指针指向的是数组的第一个元素，从这个角度来说，动态数组更像是指针。也是由于这种性质，导致了动态数组中size可以取0，即返回一个空指针，即分配一个空动态数组是合法的。同样的道理，返回的是一个指针，那么就不能使用begin或者end迭代器进行遍历

- **动态数组初始化**
  -  上面的例子中，Dynamic_Arr2并未进行初始化，若想进行默认初始化，需要在数组后面加上一个小括号。

```c++
int *Dynamic_Arr3 = new int [size]();//默认初始化
```

此时数组中的十个值都为0；也可以利用花括弧进行显式的初始化，例子如下

```c++
string *dynamci_Arr4 = new string[size]{"aa","bb","cc","dd",string(2,'e')};
```

***\*注意：显式地初始化时，元素数目不能大于数组大小。其次，显式初始化可能会因为编译器版本原因报错，笔者在VS2013与VS2017下进行测试，VS2013下在释放内存时出现内存错误。\****

- 动态数组释放
  - 释放动态数组时，使用delete[]arr_name;即在数组名前面加一个中括弧；例如、

```c++
delete[] Dynamic_Arr4;
```

 释放一个动态数组时，或者说是指向数组的指针时，空括号是必须的。它告诉编译器，指针指向一个数组的第一个元素。delete释放数组是逆序进行的，最后一个元素被最先释放，第一个元素最后一个被释放。

- **动态多维数组的内存申请**

```c++
int MAX_NUM = 10;
	int COL_NUM = 5, ROW_NUM = 3;
	double ***Arr3D = new double **[MAX_NUM];
 
	for (int i = 0; i < MAX_NUM; i++)
	{
		Arr3D[i] = new double *[ROW_NUM];
 
		for (int j = 0; j < ROW_NUM; j++)
		{
			Arr3D[i][j] = new double[COL_NUM];
		}
	}

```

从上面可以看出，多维数组的申请与多维vector的定义类似，是一层一层的申请内存的，返回的是指向指针数组的指针。先依次声明维度的大小，然后从最低维度开始申请内存。先申请ROW_NUM个大小为COL_NUM的数组，将指向这些数组的首地址的指针传递到大小为ROW_NUM的数组中，构成一个新的数组，以此类推，完成内存申请。 上面的例子中得到的是一个10层，3行，5列的数组

- 多维动态数组内存释放
  -    多维动态数组的释放是从最低维度开始的。先释放掉最低维度的一维数组，然后依次释放内存，直到释放掉最高维度。就跟一层一层的拆房子一样

```c++

for (int i = 0; i < MAX_NUM; i++)
	{
		for (int j = 0; j < ROW_NUM; j++)
		{
			delete[] Arr3D[i][j];
		}
		delete[] Arr3D[i];
	}
	delete[] Arr3D;
```

#### 从函数或方法返回内存

```c++
#include  <iostream>
void swap(int*x,int*y);
int main()
{
    int a,b;
    a =3;
    b =5;
    
    swap(&a,&b);
    std::cout<<"a="<<a<<"\n";
    std::cout<<"b="<<b<<"\n";
    
    return 0;
}

void swap(int*x,int*y)
{
#if 0//此处用宏用，永远不执行，不用/*   */   #if 1 永远执行
    itn temp;
    temp =*x;
    *x=*y;
    *y= temp;
#endif
    *x^=*y;
    *y^=*x;
    *x^=*Y;   
}
```

函数指针和指针函数

1.指针函数：是指函数返回值是某一类型的指针，本质是一个`函数`。

指针函数的定义为： `类型标识符 *函数名(参数表)`， 例如： `int *f(x，y);`

```c++
int *fun();
int *p;
p = fun(a);
```



2.函数指针：是指向函数的指针变量，即本质是一个`指针变量`。

函数指针的定义为：`类型说明符 (*函数名) (参数)`，例如：`int (*P) (int x);`

```c++
int (*P) (int x); //声明一个函数指针

//把函数的地址赋值给函数指针，可以采用下面两种形式：
p = func; //将func函数的首地址赋给指针p
p = &func; //取地址运算符&不是必需的，因为单单一个函数标识符就标号表示了它的地址

//可以采用如下两种方式来通过指针调用函数
x = (*p)();
x = p(); //这两种格式看上去和函数调用无异。但是有些程序员倾向于使用第一种格式，因为它明确指出是通过指针而非函数名来调用函数的。

```

#### 副本构造器

对象赋值中的指针变量成员
逐位复制(bitwise copy) :
众所周知,我们可以把 一个对象实例赋值给一个类型与之相同的对象(例如 MyClass a=MyClass b),在赋值过程中编译器将生成必要的代码把"源"对象各属性的值分别赋值给"目标"对象的对应成员,这种赋值行为被称为逐位复制(bitwise copy)。

逐位复制下的普通变量与指针变量 :
逐位赋值在绝大多数场合都是没有问题的,但如果某些成员变量是指针的话,问题就来了：对象成员进行逐位复制的结果是你将拥有两个一模一样的实例,这两个实例的普通变量虽然名字一样,但是都有不同的地址。而这两个副本实例的同名指针变量却会指向相同的一个地址…

漏洞:
如果两个实例的同名指针变量指向着同一个地址,当删除其中一个对象,它包含的指针也将被删除,但万一此时另一个副本(对象)还在引用这个指针,便会出现问题！

```c++
class Myclass
{
public:
	int test; //普通成员变量test
	int* testp;  //指针成员变量testp
};
int main()
{
	Myclass a(new int(1));//1.进入主构造器 开始构造对象a  | 2.构造完毕离开主构造器
	Myclass b(new int(2));//1.进入主构造器 开始构造对象b  | 2.构造完毕离开主构造器
	a = b;//1.进入赋值语句重载函数  | 2.离开赋值语句重载函数 
	

	int* aTestpointer = &a.test;
	int* bTestpointer = &b.test;

	int* aTestPpointer = a.testp;
	int* bTestPpointer = b.testp;
	//为了便于阅读,省略了打印地址的代码
	***
	打印指针地址...
}

```

在主函数中建立同属于Myclass类的两个对象实例a和b,并将b对象赋值给对象a,然后分别打印a和b对象内的非指针变量成员和指针变量成员的地址：

![img](https://img-blog.csdnimg.cn/20201019221516775.png#pic_center)

从运行结果我们可以看出,两个同类副本对象中的指针变量testp指向的确实是同一个地址,这导致如果我们删除其中一个对象,另一个对象便不能引用这个Testp指针,为了解决这个隐患,能不能在调用另一个副本对象的同时删除这个被第一个对象删除的指针,避免第二个副本对象引用一个不存在的指针呢？

虽然这么做在逻辑上没有问题,但从实际情况上来看是不可能的,因为CPU本身就是逐条指令执行的,逐条执行有先后顺序,当试图第二次释放同一块内存,程序肯定会崩溃。

解决方案:
那么怎么才能解决这个问题, 让程序员能在进行对象“复制”的时候能够精确的表明应该复制什么内容和如何进行赋值,接下来我们暂时先**利用重载赋值操作符解决这个问题**。

## 重载操作符

现在我们有两个Myclass类的副本对象a和b,我们再将a对象的值赋值给对象b：

```c++
MyClass a;
MyClass b;
a=b;
```

第三行对象赋值操作语句中,将a对象的值赋值给对象b,这里就可能因为赋值时对象中有指针变量成员而埋下祸根,那么,怎样才能在发生错误前截获这个赋值操作并告诉它应该如何处理那些埋下祸根的指针变量呢。

重载赋值操作符：
几乎所有C++的操作符都可以重载,而赋值操作符 " = " 恰好是其中的一个,我们将重载这个 " = "操作符,在其中对对象赋值时的指针变量进行处理：

```c++
Myclass &operator=(const Myclass &rhs);

该函数返回一个引用,该引用指向一个Myclass类的对象

```

上述语句告诉我们这个方法所预期的输入参数应该是一个Myclass类型的,不可被改变的引用
因为这里使用的输入参数是一个引用,所以编译器在传递输入参数的时候就不会再为它创建另一个副本(否则会导致无限递归),用引用做参数也方便我们把一组赋值语句串联起来，如a = b = c；

又因为这里只需要读取这个输入参数,而不用改变它的值,所以我们用const把那个引用声明为一个常量(const),确保万无一失。

只对赋值操作符 " = " 进行重载,解决指针变量在对象赋值对象时的问题

```c++
class Myclass
{
public:
	Myclass(int* p);
	~Myclass();

	Myclass& operator=(const Myclass& rhs);//todo重载赋值号函数

	void print();

private:
	int *ptr;
};

Myclass::Myclass(int* p)
{
	ptr = p;
}

Myclass::~Myclass()
{
	delete ptr;
}

Myclass& Myclass::operator=(const Myclass& rhs)
{	
	//条件一 ： 对象赋值 赋值号两边为不同的对象    a=b; (a为本对象,b为传入的对象)
	if (this != &rhs)//判断重载函数右操作数传入的对象的引用是否和本类对象的地址一致
	{
		//todo如果地址不一致(不是同一个对象)
		delete ptr; //释放删除 a (本对象)的指针  先把a对象的指针空间清理出来
		ptr = new int; //动态分配内存给ptr这个指针
	   *ptr = *rhs.ptr;//将ptr这个指针值赋值为传入的对象的指针的值。
		
		🔥以上操作在两个同类对象赋值时(a=b)：
		1.先进行判断，判断两个对象是否为同一个对象(a和b不是同一个对象)
		2.若不是同一个对象,将逐位赋值时的a对象的名为ptr的指针(逐位赋值时直接被赋值为对象b的ptr指针地址)释放,再给a对象的名为			   
		ptr的指针动态分配一个与对象b的ptr指针完全不同的地址(此时我们便保证了副本对象a和b中的同名指针变量ptr地址是不同的)
		3.让a和b的ptr指针指向不同地址后,此时a的ptr指针虽然有不同的地址,但这个地址不指向任何一个值(0000000),但是b对象的指针	       	 
		变量ptr指向了一个整型数值，所以我们一定要将b对象的ptr指向的值赋值给a对象的ptr指针
		
	}
	//条件二：对象赋值 赋值号两边为同一个对象    a=a; 
	else
	{
		cout << "赋值号两边为同个对象,不做处理!\n";
	}
	return *this;//🔥返回一个引用
}

void Myclass::print()//打印两个副本对象同名指针ptr的值
{	
	cout << *ptr << endl;
}


int main()
{
	Myclass a(new int(1));//创建一个int型数，并且用()括号中的数据进行初始化
	Myclass b(new int(2));

	a.print();
	b.print();

	a = b;
	cout << endl;

	a.print();
	b.print();
}

```

运行结果

```
1
2

2
2
```

虽然对赋值操作符进行重载完成了程序的要求,但是还不够完美,所以我们还需要运用副本构造器对代码进行改良:

**赋值操作符重载和副本构造器这两种解决方案的区别：**

重载赋值操作符： 先创建两个同类的实例a和b,再把b实例赋值给实例a。

```c++
Myclass a;
Myclass b;
b=a;
```

副本构造器： 先创建一个实例a,然后在创建另一个同类实例b的同时用实例a的值对实例b进行初始化

```c++
Myclass a;
Myclass b=a;//此时编译器将在Myclass这个类中寻找一个副本构造器(copy constructor),如果找不到这个副本构造器,它会自行创建一个副本构造器
```

虽然这两种方案看起来区别不大,但编译器却会生成完全不同的程序代码 ：这是因为如果编译器在对实例对象声明的同时进行初始化(方案二)的时候,编译器将在Myclass这个类中寻找一个副本构造器(copy constructor),如果找不到这个副本构造器,它会自行创建一个副本构造器。

为什么需要副本构造器：
赋值操作符重载的这个方案的缺陷在于：即使我们对赋值操作符进行了重载,但是由编译器自行创建的副本构造器仍会以"逐位复制"的方法把 对象b复制给对象a,这仍是一个隐患。想要避免这个隐患,我们需要 亲自定义一个副本构造器,而不是让编译器帮我们自动生成。

**副本构造器的作用**： 让程序员能在进行对象“复制”的时候能够精确的表明应该复制什么内容和如何进行赋值

**副本构造器的声明：**

```c++
Myclass(const Myclass &rhs);
```

这个构造器需要一个固定不变(const)的Myclass类的引用作为输入参数,就像赋值操作符那样,因为它是一个构造器,所以不需要返回类型,只需要相应的类名和参数列表。

我们需要使用副本构造器继续改善代码…

```c++
#include <iostream>
#include <string>

using namespace std;

class Myclass
{
public:
	Myclass(int* p);//todo声明主构造器
	Myclass(const Myclass& rhs);🔥 声明副本构造器
	~Myclass();//todo声明主析构器
	int test;
	int* testp;
	Myclass& operator=(const Myclass& rhs);//todo重载赋值号函数

	void print();

private:
	int *ptr;
};

Myclass::Myclass(int* p)
{
	cout << "进入主构造器" << endl;
	ptr = p;
	cout << "离开主构造器" << endl;
}

Myclass::Myclass(const Myclass& rhs)🔥 定义副本构造器
{
	cout << "进入副本构造器" << endl;
	*this = rhs;//🔥调用赋值符重载函数
	cout << "离开副本构造器" << endl;
}

Myclass::~Myclass()
{
	cout << "进入主析构器" << endl;
	delete ptr;
	cout << "离开主析构器" << endl;
}

Myclass& Myclass::operator=(const Myclass& rhs)
{	
	//条件一 ： 对象赋值 赋值号两边为不同的对象    a=b; (a为本对象,b为传入的对象)
	if (this != &rhs)//判断重载函数右操作数传入的对象的引用是否和本类对象的地址一致
	{
		//todo如果地址不一致(不是同一个对象)
		delete ptr; //释放删除 a (本对象)的指针  先把a对象的指针空间清理出来
		ptr = new int; //动态分配内存给ptr这个指针
	   *ptr = *rhs.ptr;//将ptr这个指针值赋值为传入的对象的指针的值。
		
		🔥以上操作在两个同类对象赋值时(a=b)：
		1.先进行判断，判断两个对象是否为同一个对象(a和b不是同一个对象)
		2.若不是同一个对象,将逐位赋值时的a对象的名为ptr的指针(逐位赋值时直接被赋值为对象b的ptr指针地址)释放,再给a对象的名为			   
		ptr的指针动态分配一个与对象b的ptr指针完全不同的地址(此时我们便保证了副本对象a和b中的同名指针变量ptr地址是不同的)
		3.让a和b的ptr指针指向不同地址后,此时a的ptr指针虽然有不同的地址,但这个地址不指向任何一个值(0000000),但是b对象的指针	       	 
		变量ptr指向了一个整型数值，所以我们一定要将b对象的ptr指向的值赋值给a对象的ptr指针
		
	}
	//条件二：对象赋值 赋值号两边为同一个对象    a=a; 
	else
	{
		cout << "赋值号两边为同个对象,不做处理!\n";
	}
	return *this;//🔥返回一个引用
}


void Myclass::print()
{	
	cout << *ptr << endl;
}


int main()
{

	cout << "\n-------不同的两个对象在进行对象赋值操作时\n(声明完对象后再对此对象进行赋值操作 ：不调用副本构造器 仅进行赋值语句重载函数)：\n" << endl;

	//todonew int(1)声明整型的空间 里面存放整型量
	Myclass a(new int(1));//1.进入主构造器 开始构造对象a  | 2.构造完毕离开主构造器
	Myclass b(new int(2));//1.进入主构造器 开始构造对象b  | 2.构造完毕离开主构造器
	a = b;//1.进入赋值语句重载函数  | 2.离开赋值语句重载函数 
	

	cout << "对象赋值后 未启用副本构造器的情况下: \n"


	a.print();//对象a调用类中的打印函数
	b.print();//对象b调用类中的打印函数
	//todo运行结果为 2 2


	cout << "\n-------不同的两个对象在进行对象赋值操作时\n(声明对象的时候同时进行对此对象进行赋值操作 ：调用副本构造器中的赋值语句重载函数)：\n" << endl;

	Myclass c(new int(3));//1.进入主构造器 开始构造对象c |  2.构造完毕离开主构造器
	Myclass d = c;//1.进入副本构造器 开始构造对象d  |  2.进入赋值语句重载函数  | 3.离开赋值语句重载函数   |  4.构造完毕离开副本构造器 
	c.print();
	d.print();
	//todo运行结果为 3 3

	cout << "\n-------相同的两个对象在进行对象赋值操作时：\n" << endl;
	
	Myclass e(new int(4));//1.进入主构造器 开始构造对象e |  2.构造完毕离开主构造器
	e = e;//1.进入赋值语句重载函数  | “赋值号两边为同个对象,不做处理!” | 2.离开赋值语句重载函数 
	e.print();
	//todo运行结果为4
	return 0;*/
}

```

![img](https://img-blog.csdnimg.cn/20201020144901719.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0Nocm9uaWNjYW5keQ==,size_16,color_FFFFFF,t_70#pic_center)

![img](https://img-blog.csdnimg.cn/20201020145006978.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0Nocm9uaWNjYW5keQ==,size_16,color_FFFFFF,t_70#pic_center)
http://www.bubuko.com/infodetail-262935.html
https://blog.csdn.net/joan11_3/article/details/51628095

#### 高级强制类型转换

 什么情况下会用到强制类型转换呢，例如如下情况：

```c++
int main()
{
    Company * company = new TechCompany("APPLE","Iphone");
    TechCompany *teCompany = (TechCompany*)company;//此处使用c语言强制类型转换
    teCompany->printInfo();
    
    delete company;//注意不能即删除company,又删除techCompany
    company = NULL;
    techCompany = NULL;
    
    return 0;
    
}
```

注意不能即删除company,又删除techCompany，因为强制类型转换操作不会创建一个副本拷贝，它只是告诉编译器把有关1变量解释为另一种类型组合形式，所以他们指向的是同一地址。

虽然上述例子看起来很好看，但是它仍然有一个问题没有解决：

- 如果被强制转换的类型和目标类型结构完全不同该怎么办呢？

例如：

```c++
//如果将上诉例子改为如下，前提，company 和TechCompany结构不同，就会报错出现问题
int main()
{
    Company * company = new Company("APPLE","Iphone");//此处new对象本身就位Company类
    TechCompany *teCompany = (TechCompany*)company;//此处使用c语言强制类型转换
    teCompany->printInfo();
    
    delete company;//注意不能即删除company,又删除techCompany
    company = NULL;
    techCompany = NULL;
    
    return 0;
    
}
```

c++提供了一些强制类型转换

| 语法                          | 说明                                                         |
| :---------------------------- | ------------------------------------------------------------ |
| const_cast<MyClass*>(value)   | 用来改变value的“常量性”                                      |
| dynamic_cast<MyClass*>(value) | 用来把一种类型的对象指针安全的强制转换为另一种类型的对象指针。注：如果valu的类型不是一个MyClass类（或MyClass的子类）的指针，这个操作符将返回NULL; |
| reinterpret_cast<T>(value)    | 在不进行任何实质性的转换的情况下，把一种类型的指针解释为另一种类型的指针或者把一种整数解释为另一种整数 |
| static_cast<T>(value)         | 用来进行强制类型转换而不做任何运行时检查，老式强制类型转换操作的替代品 |

- 如果你喜欢，你仍然可以在c++里继续使用c的强制转换操作符
- 但表格中的操作符还能够进行必要的类型检查，可以改善程序的可靠性
- 动态强制类型转换的语法更像一个函数调用：

```c++
Company *company = new Company("APPLE","Iphone");
TechCompany*tecCompany = dynamic_cast<TechCompany*>(company);//返回一个NULL
```

上述例子可以优化为：

```c++
//如果将上诉例子改为如下，前提，company 和TechCompany结构不同，就会报错出现问题
int main()
{
    Company * company = new Company("APPLE","Iphone");//此处new对象本身就位Company类
    TechCompany *teCompany = <TechCompany*>(company);//此处使用c++ dynamic_cast强制类型转换
    
    if(techCompany != NULL)
    {
        std::cout<<"成功！\n";
        teCompany->printInfo();
    }
    else
    {
        std::cout<<"悲催！\n";
    }
    
    delete company;//注意不能即删除company,又删除techCompany
    company = NULL;
    techCompany = NULL;
    
    return 0;
    
}
```



#### 避免内存泄露

```c++
int * x
x = new int[3000];
x = new int[4000];
delete[]x;
x = NUll;
```

这可能内存泄露的情况之一

会导致内存泄露的另一种情况是用来保存内存块地址的指针变量作用域问题；

```c++
void foo()
{
    My Class *x;
    x = new MyClass();
}
```

当foo()函数结束时，指针变量x将超出它的作用域，这意味着它将不复存在，它的值当然就会丢失。

有两种方法可以用来堵住这种漏洞：

- 第一个方法是在return语句之前的某个地方插入一条delete x 语句：

```c++
void foo()
{
    MyClass *x;
    x = new MyClass();
    delete x;
    x = NULL;
    return;
}
```

- 第二个方法是让函数把内存的地址返回给它的调用者：

```c++
MyClass *foo()
{
    MyClass *x;
    x = new Myclass();
    
    return x;
}
```

动态内不存在作用域的问题，一旦被分配，内存块就可以在程序的任何地方使用。

因为动态内存没有作用域，所以必须由程序员来跟踪他们的使用情况，并在不需要用到他们的时候把它们及时归还给系统。

这里需要特别注意的是，虽然动态分配的内存块没有作用域，但用来保存其地址的指针变量是受作用域影响。

#### 模块化编程与命名空间

- 第一个概念模块化（modularization）
  - 把程序划分为多个组成部分（模块）
  - 通过程序代码分散到多个文件里，等编译程序时再把那些文件重新组合到一起实现
- 第二个就是命名空间（namespace）
  - 这个概念是c++相比c新增加的东西，编写的程序越多、程序越复杂，就越需要使用命名空间

**头文件：**

c++预处理器#include指令提供让编译器在编译主程序时把其他文件包括进来的机制

- 头文件的基本用途是提供必要的函数声明，和类声明。可分为系统头文件和自定义头文件
  - 系统头文件定义的是系统级功能，有了他们c++代码才可以在某种特定的系统上运行，比如mac系统和windows系统上的cout指令，实现机制肯定是不同的。系统头文件的另一个重要作用是保证c++代码的可移植性，确保同样的c++代码在不同的操作系统上做同样的事情。。。。。。在include指令里，系统头文件的文件名要放在尖括号里，这是告诉编译器：应该到“标准的“地址寻找这个文件：include<stdio.h>
  - 自定义头文件，在linclude指令里，要放在双引号里给出：#include"fishc.h"
- 头文件是一些以.h作为扩展名的标准文件，在一般情况下，都应该把自定义头文件和其余文件放在同一个子目录里，或者在主程序目录下专门创建一个子文件夹来集中存放他们
- 你可以在头文件里来保存任何一段代码，如函数或类的声明，但不要用来保存他们的实现！
- 在头文件里应该多添加注释，将它的用途和用法描述清楚
  - 包括：文件用途、创建者名称，最后一次修改时间，用什么限制和前提条件等等
  - 头文件里每一个类和函数也应该说明
- 头文件一般用来保存函数声明、用户定义典型数据（结构和类）、模板和全局常量。

**使用头文件**(linux./windows.\\)windows下一个反斜杠代表转义字符

- 如果没有给出路径名，编译器将到当前子目录以及当前开发环境中其他逻辑子目录去寻找头文件
- 导入自己的头文件可以使用相对路径，如果头文件与主程序文件在同一个子目录里，则可以这么写：
  - ——#include"./fishc.h"   点斜杠表示当前目录
- 如果头文件位于某个下级子目录里，可以以下级子目录名字开头：
  - ——#include"includes/fishc.h"    
- 如果头文件位于与当子目录平行的“兄弟”子目录里，则需要这么写：
  - ——#include"../includes/fishc.h"
- 作为一个通用原则，把声明放在一个头文件里，把实现代码放在一个.cpp文件里

例子：

一个源程序为如下，现将该程序拆分开来，分为rational.h和rational.cpp

```c++
#include <iostream>
#include <string>
#include <stdlib.h>

class Rational
{
public:
	Rational(int num, int denom);//num =分子，denom =分母

	Rational operator+(Rational rhs);// rhs = right hand side
	Rational operator-(Rational rhs);
	Rational operator *(Rational rhs);
	Rational operator /(Rational rhs);

	void print();

private:
	void normalize();//负责对分数进行化简处理

	int numerator;//分子
	int denominator;//分母
	//类名&  为c++中的类引用操作
	friend std::ostream& operator<<(std::ostream& os, Rational f);
	//第一个参数os是指向将要向它写的那个流，以引用传递的方式进行
	//第二个参数是打算写到数据流中的数据
	//运用友元进行操作，因为重载的不属于Rational 但要对rational中的pirvate属性
};

Rational::Rational(int num, int denom)
{
	numerator = num;
	denominator = denom;

	normalize();

}

//noramlize()对分数进行简化操作
//只允许分子为负数，如果分母为负数则把负数挪到分子部分如1/-2=-1/2
//允许欧几里得算法（辗转求余原理）将分数进行简化；2/10=1/5


void Rational::normalize()
{
	//确保分母为正
	if (denominator < 0)
	{
		numerator = -numerator;
		denominator = -denominator;

	}

	//欧几里得算法（辗转求余原理）
	int a = abs(numerator);
	int b = abs(denominator);

	while(b>0)
	{
		int t = a % b;// 4%16 1.t=4,a=b=16,b=t=4;b>0  -->;
		              //16%4  2.t=0,a=b=4,b=t=0
		a = b;
		b = t;
	}
	//分子、分母分别处以最大公约数得到最简化分数

	numerator /= a;
	denominator /= a;
}



Rational Rational::operator+(Rational rhs)
{
	int a = numerator;
	int b = denominator;
	int c = rhs.numerator;
	int d = rhs.denominator;

	int e = a * d + c * b;
	int f = b * d;

	return Rational(e, f);

}

//减去一个数等于加上这个数的相反数
Rational Rational::operator-(Rational rhs)
{
	rhs.numerator = -rhs.numerator;

	return operator+(rhs);

}

Rational Rational::operator*(Rational rhs)
{
	int a = numerator;
	int b = denominator;
	int c = rhs.numerator;
	int d = rhs.denominator;

	int e = a * c;
	int f = b * d;

	return Rational(e, f);


}


//除一个数等于乘它的倒数
Rational Rational::operator/(Rational rhs)
{
	int t = rhs.numerator;
	rhs.numerator = rhs.denominator;
	rhs.denominator = t;

	return operator*(rhs);

}

void Rational::print()
{
	if (numerator % denominator == 0)
		std::cout << numerator / denominator;
	else
		std::cout << numerator << "/" << denominator;

}

std::ostream& operator<<(std::ostream& os, Rational f);

int main()
{
	Rational f1(2, 16);
	Rational f2(2, 8);

	/*Rational res = f1 + f2;
	f1.print();
	std::cout << "+";
	f2.print();
	std::cout << "=";
	res.print();
	std::cout << "\n";*/

	//重载了左移操作符号就不再需要使用类里的print()函数


	std::cout << f1 << "+" << f2 << "==" << (f1 + f2) << "\n";
	std::cout << f1 << "-" << f2 << "==" << (f1 - f2) << "\n";
	std::cout << f1 << "*" << f2 << "==" << (f1 * f2) << "\n";
	std::cout << f1 << "/" << f2 << "==" << (f1 / f2) << "\n";

	return 0;

}

std::ostream& operator<<(std::ostream& os, Rational f)
{
	os << f.numerator << "/" << f.denominator;
	return os;

}

```

在rational.h头文件里程序为，类声明

```c++
//rational.h
//creat by dez
//这个头文件声明了有理数（rational class）
//类里对四则运算进行了重载，实现分数运算

#include<iostream>

class Rational
{
public:
	Rational(int num, int denom);//num =分子，denom =分母

	Rational operator+(Rational rhs);// rhs = right hand side
	Rational operator-(Rational rhs);
	Rational operator *(Rational rhs);
	Rational operator /(Rational rhs);

	void print();

private:
	void normalize();//负责对分数进行化简处理

	int numerator;//分子
	int denominator;//分母
	//类名&  为c++中的类引用操作
	friend std::ostream& operator<<(std::ostream& os, Rational f);
	//第一个参数os是指向将要向它写的那个流，以引用传递的方式进行
	//第二个参数是打算写到数据流中的数据
	//运用友元进行操作，因为重载的不属于Rational 但要对rational中的pirvate属性
};
```

rational.cpp文件为,函数的实现

```c++
#include <iostream>
#include <string>
#include <stdlib.h>
#include"rational.h"


Rational::Rational(int num, int denom)
{
	numerator = num;
	denominator = denom;

	normalize();

}

//noramlize()对分数进行简化操作
//只允许分子为负数，如果分母为负数则把负数挪到分子部分如1/-2=-1/2
//允许欧几里得算法（辗转求余原理）将分数进行简化；2/10=1/5


void Rational::normalize()
{
	//确保分母为正
	if (denominator < 0)
	{
		numerator = -numerator;
		denominator = -denominator;

	}

	//欧几里得算法（辗转求余原理）
	int a = abs(numerator);
	int b = abs(denominator);

	while(b>0)
	{
		int t = a % b;// 4%16 1.t=4,a=b=16,b=t=4;b>0  -->;
		              //16%4  2.t=0,a=b=4,b=t=0
		a = b;
		b = t;
	}
	//分子、分母分别处以最大公约数得到最简化分数

	numerator /= a;
	denominator /= a;
}



Rational Rational::operator+(Rational rhs)
{
	int a = numerator;
	int b = denominator;
	int c = rhs.numerator;
	int d = rhs.denominator;

	int e = a * d + c * b;
	int f = b * d;

	return Rational(e, f);

}

//减去一个数等于加上这个数的相反数
Rational Rational::operator-(Rational rhs)
{
	rhs.numerator = -rhs.numerator;

	return operator+(rhs);

}

Rational Rational::operator*(Rational rhs)
{
	int a = numerator;
	int b = denominator;
	int c = rhs.numerator;
	int d = rhs.denominator;

	int e = a * c;
	int f = b * d;

	return Rational(e, f
}


//除一个数等于乘它的倒数
Rational Rational::operator/(Rational rhs)
{
	int t = rhs.numerator;
	rhs.numerator = rhs.denominator;
	rhs.denominator = t;

	return operator*(rhs);

}

void Rational::print()
{
	if (numerator % denominator == 0)
		std::cout << numerator / denominator;
	else
		std::cout << numerator << "/" << denominator;

}

std::ostream& operator<<(std::ostream& os, Rational f);

std::ostream& operator<<(std::ostream& os, Rational f)
{
	os << f.numerator << "/" << f.denominator;
	return os;

}
```



#### c预处理器

上个例子中rational.h类被声明了两次，这显然没有必要（如果它是一个结构，声名两次还会导致编译报错）

解决方案，利用c++预处理器，我们可以让头文件只在这个类还没有被声明过的情况下，才声明它。

| 指令   | 说明                                   |
| ------ | -------------------------------------- |
| #if    | 如果表达式为真，执行代码               |
| #else  | 如果前面的#if表达式为假，执行代码      |
| #elif  | 相当于“elseif”                         |
| #endif | 用来标志一个指令的结束                 |
| #ifdef | 如果本指令所引用的定义已存在，执行代码 |
| #ifdef | 如果本指令所引用的定义不存在，执行代码 |

只需要将上述头文件这样改

```c++
//rational.h
//creat by dez
//这个头文件声明了有理数（rational class）
//类里对四则运算进行了重载，实现分数运算

#ifndef RATIONAL_H
#define RATIOANL_H

#include<iostream>

class Rational
{
public:
	Rational(int num, int denom);//num =分子，denom =分母

	Rational operator+(Rational rhs);// rhs = right hand side
	Rational operator-(Rational rhs);
	Rational operator *(Rational rhs);
	Rational operator /(Rational rhs);

	void print();

private:
	void normalize();//负责对分数进行化简处理

	int numerator;//分子
	int denominator;//分母
	//类名&  为c++中的类引用操作
	friend std::ostream& operator<<(std::ostream& os, Rational f);
	//第一个参数os是指向将要向它写的那个流，以引用传递的方式进行
	//第二个参数是打算写到数据流中的数据
	//运用友元进行操作，因为重载的不属于Rational 但要对rational中的pirvate属性
};

#endif
```

#### 命名空间

命名空间就是由用户定义的范围，同一个命名空间里的东西只要在这个命名空间独一无二的名字就可以了

创建命名空间的方法很简单，先写出关键字namespace,再写出这个命名空间的名字，然后把这个命名空间里的东西全部包括在一对花括号里就可以了

```
namespace myNamespace
{
//全部东西
}
```

现在把我们上述创建的Rational类的定义放到它自己的命名空间中，这样不用担心有其他的也加Rational的东西与我们所写起冲突了

```c++
//rational.h中的改动
#ifndef RATIONAL_H
#define RATIOANL_H

#include<iostream>

namespace myMath
{
	class Rational
	{...};
}
#endif
//rational.cpp内容全部用命名空间括起来
namespace myMath
{
//全部内容
}
//main函数中
使用using namespace myMath;
或者在使用rational的地方使用myMath::Rational f1(2,16);这种操作
```

访问命名空间有是三种方式

- std::cout
- using namespace std;//一般不要这么做
- using std::cout;——cout<<"...."//只把你要的特定命名空间提取到作用域。



#### 链接和作用域

每个源文件都被称为一个翻译单元（translation unit）,在某一个翻译单元里定义的东西在另一个翻译单元里使用正是链接发挥作用的地方。作用域、链接和存储是相互关联的概念。

**存储类**

每一个变量都有一个存储类，它决定这程序将把变量存储在计算机什么地方、如何存储，以及变量应该有着怎样的作用域。

1. 默认的存储类是auto（自动）的，，自动变量存储在成为（stack）的临时内存里，并有着最小的作用域，当程序执行到语句块或函数末尾的花括号时，将被系统自动回收。

2. 与atuo不同的是static，static变量在程序的生命期内将一直保有它的值而不会消亡，因为他们是存储在静存储区，生命周期和全局变量一样。static 变量可以有external或internal链接。

3. 第三个存储类是extern，它在有多个翻译单元时非常重要。这个关键字用来把另一个翻译单元里某个变量申明为本翻译单元里一个同名变量。

- 编译器不会为extern变量分配内存，因为在其他地方已经为它分配过内存。

4. 还有一个存储类是register，它要求编译器把一个变量存储在CPU的寄存器里，但是他与自动变量有相同的作用域。

- register变量存储速度最快，但是有些编译器可能不允许使用这类变量。

**变量的链接和作用域**

链接是一个比较深奥的概念，本文尽可能用浅显的文字来对他描述

- 在使用编译器建议程序时，它实际由3个步骤构成，
  1. 执行预处理器指令；
  2. 把.cpp文件编译成.o文件；
  3. 把.o文件链接成一个可执行文件；



链接有三种情况，凡是有名称的东西（函数、类、常量、变量、模板、命名空间，等等）必然属于其中之一：**外链接（external），内连接（internal），无连接（none）**。

- **外连接（external）**：每个翻译单元都可以访问这个东西，前提是你知道有这个东西存在
  - 普通函数、变量、模板和命名空间都可以有外连接
- **内连接（internal）**:在某个翻译单元里定义的东西只能在翻译单元里使用，在任何函数以外的静态变量都有内连接；
- **无连接（none）**：在函数里定义的变量只存在于该函数的内部，无任何连接（none）；

![image-20220920102601057](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220920102601057.png)

#### 基本语法模板

1. 面向过程式范型——把程序划分为不同的函数

2. 面向对象式范型——把代码和数据组成各种各样的类型并建立类之间的继承关系

3. 这里介绍另一种范型：泛型编程；

   - 在泛型编程技术里，我们仍然需要编写自己的函数和类，但不必限定它们所使用的数据类型

   - 只需要使用一个占位符号（通常用字母T来表示），然后用这个占位符号来编写函数

   - 当程序需要这段代码时，你提供数据类型，编译器将根据你的模板及时生成实用代码

   - 以下代码定义了一个名为foo（）的函数模板：

     ```
     template <class T>
     void foo(T param)
     {
     	//do something
     }
     ```

举个列子：交换两个变量的值是一种几乎所有的程序都需要用到的基本基本操作。

```c++
#include <iostream>
#include <string>

template<class T>//不要把函数模板分成原型和实现两个部分，放在一起
void swap(T&a,T&b)
{
    T tmp = a;
    a = b;
    b = tmp;
}

int main()
{
    int i1 = 100;
    int i2 = 200;
    
    std::cout<<"交换前，i1="<< i1 <<", i2 ="<< i2 <<"\n";
    swap(i1,i2);
    std::cout<<"交换后， i1="<< i1 <<", i2 ="<< i2 <<"\n";
    
    std::string s1 = "小甲鱼";
    std::string s2 = "xioayouyu";
    
    
	std::cout << "交换前，s1=" << s1 << ", s2 = " << s2 << "\n";
	swap(s1, s2);
	std::cout << "交换前，s1=" << s1 << ", s2 = " << s2 << "\n";
    
    return 0;
}
```

#### 类模板

类模板与函数模板相似，同样是先由你编写一个类的模板，再由编译器在你第一次使用这个模板时生成实际代码

```c++
template <class T>
 class MyClass
 {
     MyClass();
     void swap(T&a,T&b);
 }
//构造器的实现将是下面这样的
MyClass<T>::MyClass()
{
    //初始化操作
}
```

- 因为MyClass是一个类模板，所以不能只给出MyClass::MyClass(),编译器需要你在这里给出一种与MyClass()配合使用到的数据类型，必须在尖括号里提供它。因为没有确定的数据类型可以提供，所以使用一个T作为占位符即可。
-  

```c++
#include <iostream>
#include <string>

template <class T>
 class Stack
 {
public:
     Stack(unsigned int size = 100);
     ~Stack();
     void push(T value);
     T pop();
private:
     unsigned int size;
     unsigned int sp;
     T *data;
 };

template <class T>
Stack<T>::Stack(unsigned int size)
{
    this -> size = size;
    date = new  T(size)
    sp = 0;
}

Stack<T>::~Stack()
{
    delete []data;
}

template <class T>
void Stack<T>::push(T value)
{
    data[sp++] = value;
}

template <class T>
 T Stack<T>::pop()
 {
    return data[--sp]; 
 }


int main()
{
    Stack<int> intStack(100);
    intStack.push(1);
    intStack.push(2);
    intStack.push(3);
    
    std::cout << intStack.pop() << "\n";
    std::cout << intStack.pop() << "\n";
    std::cout << intStack.pop() << "\n";
    
    return 0;

}
```

#### 内联函数

内联函数的引入是为了解决程序中函数调用的效率问题

内联函数从源代码层面看，有函数的结构，而在编译后，却不具备函的数形式性质。编译时类似宏替换，使函数体替换调用处的函数名。

一般在代码中用inline修饰，但能否能形成内联函数，需要看编译器对该函数定义的具体处理

```c++
inline int add(int x ,int y, int z)
{
    return x+y+z;
}
//在程序中，调用其函数时，该函数在编译时被替代，而不像一般函数那样是在程序运行时被调用
```

函数是一个可以重复使用的代码块，CPU 会一条一条地挨着执行其中的代码。CPU 在执行主调函数代码时如果遇到了被调函数，主调函数就会暂停，CPU 转而执行被调函数的代码；被调函数执行完毕后再返回到主调函数，主调函数根据刚才的状态继续往下执行。

一个 C/[C++](http://c.biancheng.net/cplus/) 程序的执行过程可以认为是多个函数之间的相互调用过程，它们形成了一个或简单或复杂的调用链条，这个链条的起点是 main()，终点也是 main()。当 main() 调用完了所有的函数，它会返回一个值（例如`return 0;`）来结束自己的生命，从而结束整个程序。

函数调用是有时间和空间开销的。程序在执行一个函数之前需要做一些准备工作，要将实参、局部变量、返回地址以及若干寄存器都压入栈中，然后才能执行函数体中的代码；函数体中的代码执行完毕后还要清理现场，将之前压入栈中的数据都出栈，才能接着执行函数调用位置以后的代码。

如果函数体代码比较多，需要较长的执行时间，那么函数调用机制占用的时间可以忽略；如果函数只有一两条语句，那么大部分的时间都会花费在函数调用机制上，这种时间开销就就不容忽视。

为了消除函数调用的时空开销，C++ 提供一种提高效率的方法，即在编译时将函数调用处用函数体替换，类似于C语言中的宏展开。这种在函数调用处直接嵌入函数体的函数称为内联函数（Inline Function），又称内嵌函数或者内置函数。

```c++
#include <iostream>
using namespace std;
//内联函数，交换两个数的值
inline void swap(int *a, int *b){
    int temp;
    temp = *a;
    *a = *b;
    *b = temp;
}
int main(){
    int m, n;
    cin>>m>>n;
    cout<<m<<", "<<n<<endl;
    swap(&m, &n);
    cout<<m<<", "<<n<<endl;
    return 0;
}
```

注意，要在函数定义处添加 inline 关键字，在函数声明处添加 inline 关键字虽然没有错，但这种做法是无效的，编译器会忽略函数声明处的 inline 关键字。

当编译器遇到函数调用`swap(&m, &n)`时，会用 swap() 函数的代码替换`swap(&m, &n)`，同时用实参代替形参。这样，程序第 16 行就被置换成：

```c++
int temp;
temp = *(&m);
*(&m) = *(&n);
*(&n) = temp;
```

当函数比较复杂时，函数调用的时空开销可以忽略，大部分的 CPU 时间都会花费在执行函数体代码上，所以我们一般是将非常短小的函数声明为内联函数。

指定内联函数的方法很简单，只需要在函数定义处增加 inline 关键字。请看下面的例子：c++并没有限制只能使用一个类型的占位符，如果类模板需要一种以上的类型，根据具体情况多使用几个占位符号即可。

```c++
template <class T , class U>
class MyClass
{
    //.....
}

//实例化时，我们只需要这么做：
MyClass<int, float> myClass;
```

#### 容器和算法

能够容纳两个或更多个值的数据结构通常我们称为容器

数据结构与算法这本书可以详细的去参考

c++库里有许多现成的容器可以直接拿来用，找到合适的容器只是编程工作的一部分，还需要适当的函数和算法来处理这个容器里的数据1才能实现最优效率

数组这种数据结构的最大先天不足在于它受限于一个固定的长度

c++提供的向量（vector）类型从根本上解决了数组先天不足的问题，像创建各种不同类型的数组一样，我们也可以创建各种不同的类型的向量。

- 不用对一个向量能容纳多少元素做出限定，因为向量可以动态的随着你往里面添加元素而增大
- 可以通过size()方法查询长度
- 通过push_back()方法往里面添加东西
- 可以通过访问数组元素语法来访问某给定的向量里的各种元素

```c++
std::vector <type> vectorName;
```

使用举例：

```c++
#include <iostream>
#include <string>
#include <vector>

int main()
{
    std::vector<std::string> names;
    names.push_back("乌龟");
    names.push_back("猫头鹰");
    name.push_back("加菲猫");
    
    for(int i  0; i <names.size(); i++)
    {
        std::cout<< names[i] << "\n";
        
    }

    return 0;
}
```

##### 迭代器

对容器里的各种元素进行一遍遍历，是一种常见的任务，所以应该有一种标准的方式来做这件事，c++提供的各种迭代器（iteratror）

- 迭代器是一种功能非常有限却非常实用的函数，提供一些基本操作符：*、++、==、！=、=
- 迭代器是所谓的智能指针，具有遍历复杂数据结构的功能



修改上述程序，使用迭代器

```c++
#include <iostream>
#include <string>
#include <vector>

int main()
{
    std::vector<std::string> names;
    names.push_back("乌龟");
    names.push_back("猫头鹰");
    name.push_back("加菲猫");
    
    std::vector<std::string>::iterator iter = names.begin();//iter 迭代器指向，names的开始位置
    while(iter != names.end())
    {
        std::cout<< *iter <<"\n";
        ++iter;
    }
    return 0;
}
```







