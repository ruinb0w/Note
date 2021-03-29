# 基础

## 指针

### 常量指针

> 指针的指向可以修改
>
> 指针指向的值不可以修改

```c++
int a = 10;
int b = 100;

const int * p = &a;
p = &b; // 可以
*p = 200; // 不可以
```

### 指针常量

> 指针的指向不可以修改
>
> 指针指向的值可以修改

```c++
int a = 10;
int b = 100;

int * const p = &a;
p = &b; // 不可以
*p = 200; // 可以
```

### 绝对常量

> 指向和指向的值都不可以改

```c++
int a = 10;
int b = 100;

const int * const p = &a;
p = &b; // 不可以
*p = 200; // 不可以
```

## 结构体

### 创建结构体

```c++
struct People {
    string name;
    int age;
    int score;
}p3; // 方式三

// 方式一
People p1;
p1.name = '小白';
p1.age = 18;
p1.score = 99;

// 方式二
People p2 = {'小黑', 99, 0};
```

### 结构体数组

```c++
People parry[] = {
    {'张三', 1, 2},
    {'李四', 2, 3},
    {'王五', 3, 4}
}
```

### 结构体指针

```c++
People * ptr = &p1;
People * ptr1 = parray;
cout << ptr->name << endl; // 小白
cout << ptr1->name << endl; // 张三
```

## 内存分区模型

### 简述

| 区域   | 描述                     | 管理       |
| ------ | ------------------------ | ---------- |
| 代码区 | 放函数体二进制代码       | 系统管理   |
| 全局区 | 全局变量, 静态变量, 常量 | 系统管理   |
| 栈区   | 函数的参数, 局部变量     | 编译器管理 |
| 堆区   | 手动分配和释放           | 程序员     |

### 代码区&全局区

> 代码区和全局区在程序运行前分配

代码区

* 存放CPU执行的机器指令

* 代码区是共享, 只读的

全局区

* 在程序结束后由操作系统进行释放

### 栈区

不要返回栈区中局部变量的指针

### 堆区

分配内存, 通过new关键字

```c++
int * p = new int; // 不初始化
int * p1 = new int(10); // 初始化
int * pa = new int[10]; //new一个数组
```

清理内存, 通过delete关键字

```c++
delete p; // 清除数字, 字符串, 字符
delete []pa; // 清除数组
```

## 引用

```c++
int a = 10;
int &b = a;  //b引用a
cout << b << endl;
b = 20;
cout << a << endl;
cout << b << endl;
```

### 函数引用传递

```c++
void add(int &a){
    a++;
}

int a = 10;
cout << a << endl; // 10
add(a);
cout << a << endl; // 11
```

## 类

```c++
class Rabbit {
    public: 
    	int name;
    	void eat(){
            cout << name << '在吃东西' << endl;
        }
}

Rabbit r1;
r.name = '兔子1';
r.eat(); // 兔子1在吃东西
```

### 访问权限

| 权限      | 类内访问 | 类外访问 | 继承访问 |
| --------- | -------- | -------- | -------- |
| public    | √        | √        | √        |
| protected | √        | x        | √        |
| private   | √        | x        | x        |

> 默认是private

private/protected 可以控制读写以及检测数据的有效性

### 构造函数&析构函数

>类会自动创建无参构造函数, 析构函数, 拷贝构造函数.
>
>其中构造函数和析构函数都是空函数, 拷贝函数则会自动赋值实例的属性
>
>如果手动添加了构造函数, 则不会创建默认构造函数
>
>如果成员是某个类的实例, 则构造时该成员所属的类的构造函数先执行, 而销毁时后执行该成员所属的类的析构函数

构造函数

* 语法:  `类名(){}`
* 构造函数会在实例创建时执行
* 构造函数可以有参数且可以使用重载

析构函数

* 语法:  `~类名(){}`

* 析构函数会在实例销毁时执行
* 析构函数不可以有参数

```c++
class Person{
	Person(){
        cout << "构造函数调用了" << endl;
    }
    
	~Person(){
        cout << "析构函数调用了" << endl;
    }
}
```

### 类的静态函数

所有的实例都共享类的静态函数

类的静态函数只可以访问类的静态属性

```c++
class Person{
    static void staticFunction(){
        cout << "static function" << endl;
    }
}

// 可以通过实例访问
Person p;
p.staticFunction();

// 也可以直接通过类名访问
Person::staticFunction();
```

### this指针

> this只在成员函数中有, this指向调用成员函数的实例对象
>
> this可以用于解决命名冲突
>
> this可以作为返回值返回

```c++
class Person{
    public:
    int age;
    
    Person(int age){
        this->age = age;
    }
    Person & increaseAge(int n){
        this->age += n;
        return *this;
    }
}
```

### 友元

全局函数做友元, 可以访问私有成员

```c++
class Room{
    friend void frindVisit(); // 将 frindVisit 申明为友元
    
    public:
    string sittingroom = "客厅";
    private:
    string bedroom = "卧室";
};

void frindVisit(){
    Room m;
    cout << 'visiting' << m.sittingroom << endl;
    cout << 'visiting' << m.bedroom << endl;
};

void normalVisit(){
    Room m;
    cout << 'visiting' << m.sittingroom << endl;
    cout << 'visiting' << m.bedroom << endl; //报错
};
```

类做友元

```c++
#include <iostream>
using namespace std;

class Room{
    friend class MyFriends; //将类设置为友元

    public:
    string sittingroom = "客厅";
    private:
    string bedroom = "卧室";
};

class MyFriends{
    public:
    string name = "小白";
    const Room aRoom;
    
    void visitSittingroom(){
        cout << name << "visiting" << aRoom.sittingroom << endl;
    }
    void visitBedroom(){
        cout << name << "visiting" << aRoom.bedroom << endl;
    }
};

class normalPeople{
    public:
    string name = "其他人";
    const Room aRoom;
    
    void visitSittingroom(){
        cout << name << "visiting" << aRoom.sittingroom << endl;
    }
    void visitBedroom(){
        cout << name << "visiting" << aRoom.bedroom << endl; // 报错
    }
};
```

成员函数做友元

```c++
#include <iostream>
using namespace std;

class Room{
    friend void People::friendVisit(); //将People的成员friendVisit设置为友元

    public:
    string sittingroom = "客厅";
    private:
    string bedroom = "卧室";
};

class People{
    public:
    string name = "小白";
    const Room aRoom;
    
    void friendVisit(){
        cout << name << "visiting" << aRoom.sittingroom << endl;
        cout << name << "visiting" << aRoom.bedroom << endl;
    }
    void normalVisit(){
        cout << name << "visiting" << aRoom.sittingroom << endl;
        cout << name << "visiting" << aRoom.bedroom << endl; //报错
    }
};
```

### 类外成员函数

```c++
class People{
    public:
    string name="小白";
    void sayHi();
};

void People::sayHi(){
    cout << name << '打招呼' << endl;
};
```

### 运算符重载

#### +/-运算

成员函数重载

```c++
class Coordinate{
    public:
    int x;
    int y;
    
    Coordinate(int x = 0, int y = 0){
        this->x = x;
        this->y = y;
    }
    
    Coordinate operator+(Coordinate & c){ // 通过operator+来实现重载
        Coordinate temp;
        temp.x = this->x + c.x;
        temp.y = this->y + c.y;
        return temp;
    }
};

int main()
{
  Coordinate c1(10,20);
  Coordinate c2(30,40);
  Coordinate c3 = c1 + c2; // 执行重载后的+运算
  cout << "c3.x = " << c3.x << "c3.y = " << c3.y << endl;
  return 0;
}
```

全局重载

> 左移运算符, 只能用全局重载

```c++
class Coordinate{
  public:
  int x;
  int y;
  
  Coordinate(int x = 0, int y = 0){
    this->x = x;
    this->y = y;
  }
};

Coordinate operator+(Coordinate & c1, Coordinate & c2){ // 通过operator+来实现重载
  Coordinate temp;
  temp.x = c1.x + c2.x;
  temp.y = c1.y + c2.y;
  return temp;
}

int main()
{
  Coordinate c1(10,20);
  Coordinate c2(30,40);
  Coordinate c3 = c1 + c2;
  cout << "c3.x = " << c3.x << "c3.y = " << c3.y << endl;
  return 0;
}
```

#### ++/--运算

```c++
class MyInteger{
    friend Coordinate & operator<<();
    
    public:
    int num = 0;
    
    Coordinate & operator++(){ // 前置递增
        ++ num;
        return num;
    }
    
    Coordinate & operator++(int){ // 后置递增
        num ++;
        return num
    }
};

ostream & operator<<(ostream &cout, MyInteger &myInteger){
    cout << myInteger.num;
    return cout;
}

int main()
{
    MyInteger myinteger;
    cout << myinteger << endl;
    cout << myinteger++ << endl;
    cout << myinteger << endl;
    cout << ++myinteger << endl;
    cout << myinteger << endl;
}
```

#### <<运算

```c++
class Person{
	public:
    	int a = 1;
   		int b = 2;
}

ostream &operator<<(osteam &cout, Person &p){
    cout << p.a+p.b;
    return cout;
}

int main(){
    Person p;
    cout << p << endl;
}
```

#### =运算

```c++
class Person{
  public:
    int * age;

    Person(int age){
      this->age = new int(age);
    }

    ~Person(){
      if (age != NULL) {
        delete age;
        age = NULL;
      }
    }

    Person & operator=(Person & p){
      if (age != NULL) {
        delete age;
        age = NULL;
      }
      age = new int(*p.age);
      return *this;
    }
};

int main()
{
  Person p1(18);
  Person p2(20);
  cout << *p1.age << endl;
  cout << *p2.age << endl;
  p3 = p2 = p1;
  std::cout << *p2.age << std::endl;
  std::cout << *p3.age << std::endl;
  return 0;
}
```

#### ==, != 运算

```c++

```

#### ()运算

> 由于使用起来像函数, 所以也称为**仿函数**

```c++

```

### 继承

语法: `class 子类: 继承方式 父类`

说明:

1. 父类中所有成员都会继承给儿子(私有成员也会继承给儿子, 但儿子无法访问)

3. 构造时先调用父类构造函数, 再调用子类构造函数. 析构时先调用子类的构造函数, 再调用父类的析构函数.

#### 继承方式

<img src="image-20200917105014971.png" alt="image-20200917105014971" style="zoom:80%;" />

#### 同名成员

```c++
class Father {
    public:
    	int age = 99;
}

class Son : Public Father{
    public:
    	int age = 10;
}

int main(){
    class Son s;
    
    // 默认访问的是子类的成员属性
    cout << s.age << endl; // 10
    
    // 可以通过设置作用域来访问父类的成员属性
    cout << s.Father::age << endl; // 99
}
```

#### 多继承(不推荐使用)

```c++
class Animal{}
class Sheep: public Animal{}
class Tuo: public Animal{}
class SheepTuo: public Sheep, public Tuo{} // 这里实现了多继承
```

#### 虚继承

```c++
class Animal{
    public:
    	int age = 10;
}

class Sheep:virtual public Animal{} // 这里实现了虚继承
class Tuo:virtual public Animal{} // 这里实现了虚继承
class SheepTuo: public Sheep, public Tuo{}

int main(){
    SheepTuo st;
    cout << st.age << endl; // 10, 如果不使用虚继承, 这里会发同名成员冲突
}
```

#### 多态

多态分为两类

* 静态多态: 就是 **函数重载** 和 **运算符重载 **, 在编译阶段确定函数地址
* 动态多态: 通过 **派生类** 和 **虚函数** 实现多态, 在运行阶段确定函数地址

动态多态

1. 子类重写父类的方法
2. 父类被重写的方法要设置为虚函数
3. 通过父类引用或指针来调用子类实例

```c++
// 引用的形式
class Animal{
    virtual void shout(){ // 2
        cout << '动物叫' << endl;
    }
}

class Dog: public Animal{
    virtual void shout(){  // 1
        cout << '狗叫' << endl;
    }
}

void animalShout(Animal &animal){ // 3
    animal.shout();
}

int main(){
    Dog d;
    animalShout(d); // 狗叫
}
```

```c++
// 指针的形式
class Animal{
    virtual void shout(){ // 2
        cout << '动物叫' << endl;
    }
}

class Dog: public Animal{
    virtual void shout(){  // 1
        cout << '狗叫' << endl;
    }
}

int main(){
    Dog *d = new Dog;
    d->shout; // 狗叫
}
```

#### 抽象类和纯虚函数

纯虚函数

* 通常父类中的虚函数是无意义的, 当虚函数无意义时可以将虚函数写成纯虚函数.
* 纯虚函数语法: `virtual 返回值类型 函数名 (参数列表) = 0;`

抽象类

* 当类中有纯虚函数, 该类称为抽象类.
* 抽象类无法实例化对象,子类必须重写抽象类中的纯虚函数, 否则子类也是抽象类

#### 虚析狗和纯虚析构

相同

* 都可以解决父类指针释放子类对象
* 都有具体的函数实现

区别

* 如果是纯虚析构该类则变为抽象类

### 函数对象(仿函数)

#### 创建和使用函数对象

```c++
class Add{
    int count = 0;
    int operator(int n1 ,int n2){
        return n1 + n2;
        count ++;
    }
}

Add add;
cout << add(1,2) << endl;
cout << add(10,20) << endl;
cout << add(100,200) << endl;
cout << "count" << add.count << endl;
```

#### 将函数对象作为参数传递

```c++
#include <iostream>
using namespace std;

class Add{
  public:
  int count = 0;
  int operator()(int n1 ,int n2){
    this->count ++;
    return n1 + n2;
  }
};

void loopAdd(Add &add, int *na1, int *na2){
  for (int i = 0; i < 5; i++) {
    cout << add(na1[i], na2[i]) << endl;
  }
  cout << add.count << endl;
}

int main(void)
{
  int na1[] = {1,2,3,4,5};
  int na2[] = {10,20,30,40,50};
  Add add;
  loopAdd(add, na1, na2);
  return 0;
}
```

#### 谓词

定义

* 返回bool类型的函数对象称为谓词
* operator()接收一个参数称为一元谓词
* operator()接收两个参数称为二元谓词

## 模板

### 函数模板

语法

```c++
template<typename T>
函数申明或定义
// template -- 模板申明
// typename -- 申明数据类型
// T -- 通用的数据类型(即数据类型必须一致)
```

示例

```c++
// 定义
template<typename T>
void mySwap(T &a, T &b){
    T tmp = a;
    a = b;
    b = mtp;
}

// 使用
// 1. 自动类型推导
int a = 10;
int b = 20;
mySwap(a, b);
cout << a << "," << b << endl; // 20,10
// 2. 显示指定类型
mySwap<int>(a,b);
cout << a << "," << b << endl; // 10,20
```

#### 函数模板vs普通函数

普通函数调用时, 可以发生自动类型转换

函数模板调用时, 如果通过自动类型推导则不会发生自动类型转换, 如果通过指定则会发生自动类型转换

#### 模板重载

```c++
class Person{
    public:
    	string name;
    	int age;
    
    	Person(string name, int age){
            this->name = name;
            this->age = age;
        }
}

template<> bool myCompare(Person &p1, Person &p2){
	if(p1.name == p2.name && p1.age == p2.age){
        return true;
    }else{
        return false;
    }
}

int main(){
    Person p1("jack", 10);
	Person p2("jack", 10);
    cout << myCompare(p1, p2) << endl;
}
```

### 类模板

语法

```c++
template<class T>
类
// template -- 模板申明
// typename -- 申明数据类型
// T -- 通用的数据类型
```

示例

```c++
// 定义
template<class NameType,class AgeType = int>
class Person{
    public:
   		string name;
    	int age;
    
    	Person(NameType name, ageType age){
            this->name = name;
            this->age = age;
        }
}

int main(){
    Person<string,int>p("jack", 10);
}
```

#### 类模板vs函数模板

1. 类模板没有自动类型推导
2. 类模板的参数类型可以有默认参数

#### 类模板对象做函数参数

```c++
template<class T1, class T2>
class Person(){
    public:
    	Person(T1 name, T2 age){
            this->name = name;
            this->age = age;
        }
    
    	string name;
    	int age;
    	
    	showPerson(){
            cout << this->name << this->age << endl;
        }
}

// 1.指定传入类型(常用)
void test01(Person<string, int>&p){
    p.showPerson();
}

// 2.参数模板化
template<class T1, class T2>
void test02(Person<T1, T2>&p){
   p.showPerson();
}

// 3. 整个类模板化
template<class T>
void test03(T &p){
    p.showPerson();
}

int main(){
    Person<string, int>p("jack", 10);
    test01(p);
    test02(p);
    test03(p);
}
```

#### 类模板继承

1. 继承类模板, 子类需要指出父类中T的类型

   ```c++
   template<class T>
   class Base{
       public:
       	T obj;
   }
   
   class Son:public Base<int>{
   }
   
   int main(){
       Son s;
   }
   ```

2. 如果想灵活指定T, 子类也需要变为类模板

   ```c++
   template<class T>
   class Base{
       public:
       	T n;
   }
   
   template<class T1, class T>
   class Son:public Base<T>{
       public:
       	Ti m;
   }
   
   int main(){
       Son<string, int>s;
   }
   ```

#### 成员函数类外实现

```c++
template<class T1, class T2>
class Person{
    public:
    	T1 name;
    	T2 age;
    	Person(T1 name, T2 age);
    	void showPerson();
};

template<class T1, class T2>
Person<T1, T2>::Person(T1 name, T2 age){
    this->name = name;
    this->age = age;
}

template<class T1, class T2>
void Person<T1, T2>::showPerson(){
    cout << this->name << this->age << endl;
}

int main(){
    Person<string, int>p("jack", 10);
    p.showPerson();
}
```

#### 类模板分文件编写

将类模板和成员函数实现一起写到.hpp文件

#### 类模板与友元

```c++
template Person<class T1, class T2>
class Person{
    
    // 全局友元函数类内实现
    friend void showPerson(Person<T1, T2>&p){
        cout << p.name << p.age << endl;
    }
    
    public:
    	Person(T1 name, T2 age){
            this->name = name;
            this->age = age;
        }
    private:
    	T1 name;
    	T2 age;
}

template<class T1, class T2>
void showPerson1(Person<T1,T2>&p){
    cout << p.name << p.age << endl;
}

int main(){
    Person<string, int>p("jack", 10);
    showPerson(p);
}
```
