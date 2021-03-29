## 概念

简介

1. map中所有元素都是pair
2. pair的第一个元素是key, 第二个元素是value
3. map中元素根据键值自动排序

实质

* map/multimap 属于关联式容器, 底层是二叉树

优点

* 可以快速通过key找到value

map和multimap的区别

* map不允许key重复, multimap允许

## 使用

### C

#### map<T1, T2>map_obj;

#### map(const map &map_obj);

### R

#### size

#### empty

#### find

语法: `map_obj.find(key)`

* 说明: 查找key, 如果存在则返回该元素的迭代器, 如果不存在返回 `map_obj.end()`

#### count

语法: `map_obj.count(key)`

* 说明: 统计某个key的个数, 用于multimap

### U

#### insert

语法: `map_obj.insert(pair<T1, T2>(key,value))`

#### swap

#### =

语法: `map<T1, T2> map_obj2 = map_obj1;`

* 说明: 赋值

#### [ ]

语法: `map_obj[key]=value`

* 说明: 通过重载[]来添加数据
* 不建议用[ ] 来访问, 因为访问到没有的key会自动创建一个value为0的元素

#### erase

语法: `map_obj.erase(key)`

* 说明: 将key对应的元素删除

#### clear

### O

#### 排序

```c++
class Compare{
    public:
    operator(const int v1, const int v2)const{
        return v1 > v2;
    }
}

map<int,string, Compare> m; // 从大到小排
m[10] = "xiaobai";
m[5] = "xiaohei";
m[15] = "xiaohong";
```

