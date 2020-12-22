# stack

> 需要引入 stack 头文件

<img src="image-20201014143041321.png" alt="image-20201014143041321" style="zoom:80%;" />

## 构造函数

```c++
stack<T> stk;
stack<T> stk(const stk &stk);
```

## 运算符重构

### =

## 方法

### 存取数据

#### push()

说明: 向栈内放入元素

#### pop()

说明: 从站内拿出元素

#### top()

说明: 返回栈中顶部元素

### 获取容器信息

#### empty()

说明: 返回元素是否为空(为空返回true)

#### size()

说明: 返回栈内元素个数