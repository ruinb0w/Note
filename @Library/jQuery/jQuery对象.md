jQuery对象有五种主要的使用方式

1. **传入一个函数** 则该函数会作为入口函数, 当DOM加载完毕后执行该函数
2. **传入一个DOM对象** 则将该DOM对象封装为jQuery实例对象
3. **传入一个标签字符串** 可以创建DOM并封装为jQuery对象, 并返回
4. **传入一个选择表达式** 可以获得选中的元素封装的jQuery实例对象
5. 直接使用jQuery对象提供的静态方法

# 1.入口函数

```js
$(document).ready(function(){
    //sentences
});
// 等同于
$(function(){
    //sentences
});
```

jq的入口函数执行的比js早一点, 不会等图片加载

# 2.包装DOM对象

```js
let jqObj = $(domObj);
```

# 3.创建对象

```js
let jqObj = $("<h1>hello</h1>");
```

# 4.选择器

### 4.1 基本选择器

| 选择器                  | 说明     |
| ----------------------- | -------- |
| #id                     | id       |
| .class                  | 类选择器 |
| tagname                 | 标签     |
| *                       | 选择所有 |
| selector1, selector2... | 选择并级 |
| selector1selector2...   | 选择交集 |

### 4.2 层次选择器

| 选择器             | 说明                                     |
| ------------------ | ---------------------------------------- |
| ancestor decendant | 后代选择器                               |
| father \> son      | 子代选择器                               |
| pre + next         | 兄弟选择器, 选择pre的下一个next          |
| pre ~ sibling      | 兄弟姊妹选择器, 选择pre之后的所有sibling |

### 4.3 属性选择器

| 语法               | 说明                |
| ------------------ | ------------------- |
| [attribute]        | 存在属性            |
| [attribute=value]  | 属性的值为value     |
| [attribute!=value] | 属性的值不为value   |
| [attribute^=value] | 属性的值以value开头 |
| [attribute$=value] | 属性的值以value结尾 |
| [attribute*=value] | 属性的值包含value   |

### 4.4 过滤选择器

| 过滤               | 说明                |
| ------------------ | ------------------- |
| :first             | 选中第一个          |
| :last              | 选中最后一个        |
| :not(selector)     | 反选                |
| :even              | 偶数                |
| :odd               | 奇数                |
| :eq(index)         | 等于index           |
| :gt(index)         | 大于index           |
| :lt(index)         | 小于index           |
| :contains(content) | 包含文本内容content |
| :hidden()          | 隐藏的              |
| :visible()         | 可见的              |

> 多个过滤是依次执行

### 4.5 表单选择器

| 语法      | 选择器                                  |
| --------- | --------------------------------------- |
| :input    | 匹配所有input, textarea, select, button |
| :text     | type为text                              |
| :checkbox | type为checkbox                          |
| :radio    | type为radio                             |
| :checked  | 表单为选中的                            |

# 5.静态方法

## 类型判断

### $.type()

说明: 类型判断, 可以判断出数组

### $.isFunction()

### $.isNumeric()

### $.isArray()

### isWindow()

### isEmptyObject()

### isPlainObject()

### parseJSON()

说明: 将JSON字符串解析为对象

### parseHTML()

说明: 将字符串解析为DOM对象

### parseXML()

说明: 将字符串解析为XML对象

### isXMLDoc()

说明: 如果对象是XML对象则返回true

## DOM节点操作

### $.unique()

说明: DOM节点去重

## 数组操作

### $.merge()

说明: 合并数组

### $.map()

说明: 遍历数组, 将回调函数的返回值组成新的数组

语法: `$.map(array, callback)`

* **callback** function(value, index)

### $.each()

说明: 遍历数组或对象

语法: `$.each(array, callback)`

* **callback** function(index|key, value)

### $.grep()

说明: 遍历数组, 将回调函数返回true的value组成新数组

语法: `$.grep(array, callback)`

* **callback** function(value, index)

## 字符串操作

### $.makeArray()

说明: 将字符串转为数组

### $.trim()

说明: 去除字符串前后空格

## 队列操作

### $.queue()

说明: 将函数加入队列

语法: `$.queue(element, queueName, function)`

### $.dequeue()

说明: 将函数从队列中去除并执行

语法: `$.dequeue(element, queueName)`

## 其他

### extend()

说明: 复制

语法: `$.extend([deepCopy, ]target, source[, source]*)`

- **deepCopy** bool 默认为false表示浅拷贝

### proxy()

说明: 修改this指向, 仅仅是修改, 并不会执行

语法: `$.proxy(function, object[, arg]*)`

- **return** 返回一个修改指向后的function, 调用该function时可以进行传参

### each()

说明: 遍历jQuery实例

语法: `$.each(jqObj, callback);`

- **callback(key, value)**

### $.noConflict()

说明: 防止冲突用一个变量代替jQuery变量和$变量

语法: `let yourVariable = $.noConflict()`

