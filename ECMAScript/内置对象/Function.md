# Function

Function 在js中也是一个对象

需要注意的是js只有函数作用域, 并且function是可以嵌套的,即内部函数可以访问外部函数.

## 函数申明

函数申明有两种方式

1. 普通申明方式

   ````js
   function functionName(){}
   ````

2. 匿名函数

   ```js
   var functionName = function(){};
   ```

## Function所拥有的特殊属性

### arguments

在函数中可以使用arguments对象, 它类似数组, 但不是数组

arguments保存了function的所有参数

### rest

arguments保存了所有参数, rest则是保存了剩余参数

```js
function(arg1, arg2, ...rest){
    //这里的rest就保存了除了第一和第一个参数外的所有参数
    //参数名可以不是rest但需要注意要用...来标志出rest, 例如...hello也是可以的.
    console.log(rest);
}
```

### this

this指向调用这个函数的对象

可以通过两个方法来指定this指向的对象

`func.apply(obj, [arguments])`

`func.call(obj, argument, ... , argument)`

> 可以看到两者的区别是, apply通过**数组**打包了需要传给函数的参数而call则是需要一个一个的来

## 高阶函数

将一个函数作为参数传递给另一个函数

```js
function add(x, y, f) {
    return f(x) + f(y);
}
add(-5, 6, Math.abs);
```

## 箭头函数

箭头函数与普通函数的最主要区别是this指向是根据上下文的.

## generator

generator看上去像一个函数，但可以返回多次

```js
//这里通过 function* 申明了一个generator类型的结构
function* foo(x) {
    yield x + 1;
    yield x + 2;
    return x + 3;
}
//这里得到的是一个generator对象,并不是直接执行函数
var g = foo(10);
```

执行generator 有两种方式

**方式一**

`g.next()` 这个方法会返回一个对象`{value: 0, done: false}`

* value为yield或者return返回的值
* done为true则表示generator执行完毕

**方式二**

```js
//通过for-of遍历generator对象
for(var setp of g){
	console.log(setp.value);
}
```

