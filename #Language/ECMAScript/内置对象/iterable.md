# iterable

Array, Map, Set 都属于iterable类型

可以使用`for-of`结构语句和`forEach()`方法

```js
a.forEach(function (element, index, array) {
    // element: 指向当前元素的值
    // index: 指向当前索引
    // array: 指向Array对象本身
    console.log(element + ', index = ' + index);
});
```

### map和reduce

* map和reduce都是array的方法
* map和reduce都接受一个callback函数作为参数

map

* 语法: `arr.map(function(x){return value})`
* map接受一个函数作为参数, 并将函数返回值映射为一个数组

reduce

* 语法: `arr.reduce(function(first_or_last_return,second_or_next_item){return value})`
* reduce接受两个参数, 它会遍历整个数组
* 如果array只有一项则直接返回该项
* 第一次遍历x,y的值为数组的第一和第二个
* 之后的遍历则是上一次的返回值和下一个数组元素

filter() 过滤数组

* 语法: `arr.filter(function(element[, index, self]){})`
* * element 数组的项
  * index 该项的序号
  * self 数组自身
* 遍历数组, 根据回调函数的返回值`true|false`来决定是否留下该项
* filter可以用来过滤数组中的重复项

sort() 排序

* 语法: `arr.sort(function(arg1, arg2){return 1|-1|0})`
* 返回1则将前一个升序
* 返回-1则将前一个降序
* 返回0则不变

## Map和Set

### Map

`Map`是一组键值对的结构，具有极快的查找速度

```js
var m = new Map([['Michael', 95], ['Bob', 75], ['Tracy', 85]]);
```

`Map`具有以下方法

`m.set(key, value)`

`m.get(key)` 返回value

`m.has(key)` 返回true|false

`m.delete(key)` 删除键值对

### Set

`Set`是键的集合

```js
var s2 = new Set([1, 2, 3]);
```

`Set` 具有以下方法

`s.add(key)`

`delete(key)`

