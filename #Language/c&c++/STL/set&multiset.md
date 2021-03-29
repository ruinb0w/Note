# set

## 概念

### 特点

元素在插入时会被自动排序

### 本质

set&multiset 属于关联式容器, 底层是二插树

### set和multiset的区别

* set 中元素是唯一的
* multiset 中元素可以不唯一

## 构造函数

```c++
set<T> set_obj; // 默认构造函数
set(set<T> set_obj) // 拷贝构造函数
```

## 运算符重载

#### =

说明: 赋值

## 方法

### C

#### insert

语法: `set_obj.insert(元素)`

* 说明: 返回pair类型的对象, 通过 `pair_obj.second` 可以查看是否成功

### R

#### begin

语法: `set_obj.begin()`

* 说明: 获取容器起始迭代器

#### end

语法: `set_obj.end()`

* 说明: 获取容器结束迭代器

#### size

语法: `set_obj.size()`

* 说明: 获取元素个数

#### empty

语法: `set_obj.empty()`

* 说明: 元素为空返回true

#### find

语法: `set_obj.find(元素)`

* 说明: 找到则返回指向元素的迭代器, 不存在返回 `set_obj.end()`

#### count

语法: `set_obj.count(元素)`

* 说明: 统计元素在容器中的个数(set中只有0或1)

### U

#### swap

语法: `set_obj1.swap(set_obj2)`

* 说明: 容器元素互换

### D

#### clear

语法: `set_obj.clear()`

* 说明: 清空元素

#### erase

语法: `set_obj.erase(迭代器)`

* 说明: 移除迭代器指向的元素

语法: `set_obj.erase(开始迭代器, 结束迭代器)`

* 说明: 移除开始到结束的元素

语法: `set_obj.erase(元素)`

* 说明: 移除指定元素

### O

#### 设置set排序

内置数据类型

```c++
class MyCompare{
    public:
    	bool operator()(int v1, int v2){
            return v1 > v2;
        }
}

set<int, MyCompare> s; // 这样s就是从大到小排序
```

自定义数据类型

```c++
#include <iostream>
#include <set>
using namespace std;

class Person{
  public:
  string name;
  int age;
  Person(string name, int age){
    this->name = name;
    this->age = age;
  }
};

class ComparePerson{
  public:
  bool operator()(const Person &v1, const Person &v2){
    return v1.age > v2.age;
  }
};

int main(void)
{
  set<Person, ComparePerson> s; // 这样s就是从大到小排序
  Person p1("xiaobai", 10);
  Person p2("xiaohei", 20);
  Person p3("xiaohong", 30);

  s.insert(p1);
  s.insert(p2);
  s.insert(p3);

  for (set<Person,ComparePerson>::iterator it = s.begin(); it != s.end() ; it++) {
    cout << "name: " << it->name << ",age: " << it->age << endl;
  }
  return 0;
}
```