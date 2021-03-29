# 简介

既然js是基于对象的,那么就应该有一个源头. 在浏览器中这个源头就是window对象

window对象不仅是充当了全局作用域还代表了浏览器窗口

`window`有一个别名`top`

# 属性

### window.innerWidth

### window.outerWidth

### window.innerHeight

### window.outerHeight

# 方法

### alert()

警告框

语法: `alert(内容)`

### prompt()

输入框

语法: `prompt(提示内容)`

返回值: 输入内容

### localStorage()

The following snippet accesses the current domain's local [`Storage`](https://developer.mozilla.org/en-US/docs/Web/API/Storage) object and adds a data item to it using [`Storage.setItem()`](https://developer.mozilla.org/en-US/docs/Web/API/Storage/setItem).

```js
localStorage.setItem('myCat', 'Tom');
```

The syntax for reading the localStorage item is as follows:

```js
var cat = localStorage.getItem('myCat');
```

The syntax for removing the localStorage item is as follows:

```js
localStorage.removeItem('myCat');
```

The syntax for removing all the localStorage items is as follows:

```js
// clear all items
localStorage.clear();
```

### setTimeout()

单次异步延迟

`setTimeout(function(){}, ms);`

### setInterval()

重复异步延迟

`setInterval(function(){}, ms)`

### getcomputedStyle()

说明: 获取元素的计算后的样式

语法: `getComputedStyle(element, pseudoElt)`

- **pseudoElt** 一个字符串, 用伪元素来进行匹配, 该选项必须有值, 如果没有特别设置要用`null`填充
- **return** 一个样式对象, 可以通过`.样式`来访问元素的样式属性

> 在IE8中使用 elem.currentStyle

