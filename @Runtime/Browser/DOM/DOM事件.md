# 事件绑定

## DOM2

### elem.addEventListener()

说明: 适用于chrome和firefox

语法: `elem.addEventListener("事件类型", 事件处理函数, 事件执行阶段)`

* 事件执行阶段: false为冒泡执行(默认), true为捕获阶段执行

### elem.attachEvent()

说明: 适用于IE8

语法: `elem.attachEvent("事件类型", 事件处理函数)`

## DOM0

`elem.on事件=事件处理函数`

# 解除绑定

DOM0形式: `elem.on事件=null`

DOM2 形式: 

- `elem.removeEventListener("事件类型", 事件处理函数名, 事件执行阶段)`
- IE8: `elem.detachEvent("事件类型", 事件处理函数)`

> 怎么绑定的事件就对应怎么解除绑定

# 事件阶段

## 事件捕获阶段

从外向内

## 事件目标阶段

## 事件冒泡阶段

从里到外, 子元素的事件会向祖先进行冒泡, 使得祖先的相同事件也被触发

### event.stopPropagation()

说明: 

- 阻止事件冒泡
- 可用于chrome/firefox

### window.event.cancelBuble=true

说明:

- 阻止事件冒泡
- 可用于chrome/IE8

# 事件对象

> 事件处理函数会在事件触发时默认接受到一个参数(通常写作event)

## 属性

### event.eventPahse

说明: 事件执行的阶段, 值为1是捕获阶段, 值为2是目标阶段, 值为3是冒泡阶段

### event.target

说明: 触发事件的元素, 通过该属性可以实现事件代理

### event.type

说明: 触发的事件类型

## 方法

### event.preventDefault()

说明: 阻止默认事件

## 鼠标事件

### mouseEvent.clientX

说明: 鼠标在可视区域中的位置

### mouseEvent.clientY

说明: 鼠标在可视区域中的位置

### mouseEvent.pageX

说明: 鼠标在页面中的位置

### mouseEvent.pageY

说明: 鼠标在页面中的位置

# 常用事件

## 滚动条事件

### scroll

当滚动条滚动时触发事件

## 鼠标事件

### click

鼠标点击

### mousemove

鼠标移动

### mouseover

鼠标进入

### mouseout

鼠标离开

# 其他

### this

在某个元素的事件处理函数中, `this` 指向的就是这个元素

```js
elem.onclick = function(){
    this.value="hello";
};
```

### 阻止超链接跳转

事件处理函数返回`false`即可

