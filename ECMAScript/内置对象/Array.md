# 属性

### array.length

说明: 保存了数组的长度

# 静态方法

### Array.isArray()

说明: 判断内容是数组,则返回true

语法: `Array.isArray(content)`

* **return** boolean

### Array.from()

说明: 复制数组

语法: `Array.from(sourceArray[,filter]) `

* **sourceArray** 原数组
* **return** 新的数组

# 实例方法

### indexOf()

说明: 根据值来获取索引位置

语法: `arr.indexOf(value)`

* **return** number 没有返回-1

### slice()

说明: 截取数组, 如果参数为空则复制数组

语法: `arr.slice([start][, end])`

### concat()

说明: 拼接数组

语法: `arr.concat(array1,...arrayN)`

* **return** 拼接后的数组

### join()

说明: 将数组项合并为字符串

语法: `arr.join([symbol])`

* **symbol** string 分隔符, 默认为`,`

* **return** string

### reverse()

说明: 反转数组

语法: `array.reverse()`

* **return** array

### sort()

说明: 数组排序, 默认按照ASCII排序

语法: `array.sort([callback])`

* **callback(a,b)**
  1. **a** 数组的第i项
  2. **b** 数组的第i+1项
  3. 返回>0则将a排到b前面, 返回<0则将b排到a前面, 返回0则不动
* **return** array

### splice()

说明: 删除, 插入, 替换数组项

语法: `arr.splice(index, length[, content])`

* **index** 操作的位置
* **length** 删除的长度
* **content** 插入的内容

### array.fill()

说明: 填充数组(替换数组项)

语法: `array.fill(content[,start[, end]])`

* **content** 填充(替换)内容
* **start** 开始填充位置
* **end** 结束位置

### array.copyWithin()

说明: 复制并覆盖数组项

语法: `array.copyWithin(index, start[, end])`

* **index** 覆盖的索引位置
* **start** 复制的起始位置
* **end** 复制的结束位置

## 遍历数组

### forEach()

说明: 

语法: `arr.forEach(callback)`

* **callback**
  1. 数组项
  2. 项的索引
  3. 原数组

### every()

说明: 遍历数据中的元素, 如果回调函数都返回true则该方法返回true

语法: `array.every(callback[, thisArg])`

* **callback** 回调函数
  1. 元素的值
  2. 索引值
  3. 调用该方法的array对象
* **thisArg** 回调函数`this`指向的对象
* **return** boolean

### filter()

说明: 遍历数组, 将callback返回true的数组项组成新数组

语法: `arr.filter(callback)`

* **callback**
  1. 元素的值
* **return** array

### map()

说明: 遍历数组, 将callback的返回值组成一个新的数组

语法: `array.map(callback)`

* **callback** 
  1. 数组中正在处理的当前元素
  2. 数组中正在处理的当前元素的索引, 可选
  3. `map` 方法被调用的数组, 可选
  4. 执行 `callback` 函数时使用的`this` 值, 可选

### reduce()

说明: 返回回调函数的最终累计值

语法: `array.reduce(callback)`

* ### callback(previous, current, index, array)

  * **previous** 如果是第一次循环则previous为数组第0项, 从第二次开始为回调函数则返回值
  * **current** 从数组的第1项开始

示例:

```js
numbers.reduce(function(previous, current, index){
	return previous + current;
});
```

### some()

说明: 遍历数组, 如果callback返回true则**终止**遍历

语法: `arr.some(callback)`

* **callback(currentValue[, index[, array[, thisArg]]])**
  * **currentValue** 数组中正在处理的元素
  * **index** 数组中正在处理的元素的索引值
  * **array** 被调用的数组
  * **thisArg** 执行 `callback` 时使用的 `this` 值
  * **return** boolean

### findIndex()

说明: 遍历数组, 当callback返回true时**终止**并**返回索引**

语法: `arr.findIndex(callback[, thisArg])`

* **callback(currentValue[, index[, array]])**
  * **currentValue** 数组中正在处理的元素
  * **index** 数组中正在处理的元素的索引值
  * **array** 被调用的数组
* **thisArg** 执行 `callback` 时使用的 `this` 值
* **return** number

## 堆栈操作

### push()

说明: 在数组的最后添加若干项

语法: `arr.push(item1,...,itemN)`

* **return** number 数组的长度

### pop()

说明: 弹出数组最后的项

语法: `array.pop()`

* **return** 弹出的项

### shift()

说明: 弹出数组最前面的项

语法: `array.shift()`

* **return** 弹出的项

### unshift()

说明: 在数组的最后添加若干项

语法: `array.unshift(item1,...,itemN)`

* **return** 返回数组长度

# 迭代(@@iterator)

### array\[Symbol.iterator]()

说明: 该方法会返回包含值的`@@iterator`

* `iterator.next()`返回`{ value: 1, done: false }`

### array.entries()

说明: 该方法会返回包含键值对的`@@iterator`

* `iterator.next()`返回`{ value: [ 0, 1 ], done: false }`

### array.values()

说明: 该方法会返回包含值的`@@iterator`

* `iterator.next()`返回`{ value: 1, done: false }`

### array.keys()

说明: 该方法会返回包含键的`@@iterator`

- `iterator.next()`返回`{ value: 0, done: false }`