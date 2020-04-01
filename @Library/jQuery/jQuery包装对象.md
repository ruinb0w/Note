# jQuery包装对象

jQuery实例对象是一个伪数组, 其包含n个DOM对象.

## 获取DOM对象

```js
// 直接通过[]来取
let domObj = jqObj[index];
// 通过get方法来取
let domObj = jqObj.get([index]);
```

# 查询操作

## 子查找

### children()

说明: 查找子元素

语法: `jqObj.children([selector])`

- **return** jqObj

### find()

说明: 查找后代元素

语法: `jqObj.find(selector)`

- **return** jqObj

## 父查找

### parent()

说明: 查找父元素

语法: `jqObj.parent([selector])`

- **return** jqObj

### parents()

说明: 查找祖先

语法: jqObj.parents([selector])

### parentUntil()

### closest()

## 兄弟查找

### prev**()**

说明: 查找前面的某个匹配元素

语法: `jqObj.prev([selector])`

### prevAll()

说明: 查找前面的所有匹配元素

语法: `jqObj.prevAll([selector])`

- **return** jqObj

### prevUntil()

### next()

### nextAll()

### nextUntil()

### siblings()

说明: 查找匹配的兄弟标签

语法: `jqObj.siblings([selector])`

- **return** jqObj

## 过滤操作

> 过滤后得到的是jQuery实例对象

### eq()

语法: `jqObj.eq(index|-index)`

### first()

### last()

### slice()

### filter**()**

语法: `jqObj.filter(selector)`

### has()

说明: 过滤得到包含selector指定子元素的jqObj

语法: `jqObj.has(selector)`

示例:

```html
<ul>
    <li>not include span</li>
    <li><span>include span</span></li>
</ul>
<script>
    let jqObj = $("li").has("span");
    // 这里就会选中第二个li
</script>
```

# 修改操作

## 元素内容

### html()

说明: 获取元素包含的html

### text()

说明: 获取元素包含的text

## 元素属性和值

### 值操作

**val()**

说明: 获取或设置元素的value

语法: `jqObj.val([value])`

### 属性操作

### attr()

说明: 获取或设置值为非bool的属性

语法: `jqObj.attr(attrName[, value])`

### removeAttr()

说明: 删除元素属性

语法: `jqObj.removeAttr(attrName)`

### prop()

说明: 获取或设置值为bool的属性

语法: `jqObj.prop([true|false])`

### removeProp()

说明: 删除属性

语法: `jqObj.removeProp(propName)`

### jqObj.data()

说明: 将数据缓存挂载到元素上(attr是直接添加到元素上)

### jqObj.removeData()

### 类操作

**addClass()**

说明: 给元素添加class

语法: `jqObj.addClass(className)`

- **className** 字符串, 多个可以用空格分开

**removeClass()**

说明: 移除指定的class

语法: `jqObj.removeClass(className)`

- **className** 字符串, 多个可以用空格分开

**toggleClass()**

说明: 有就删,没有就加

语法: `jqObj.toggleClass(className)`

- **className** 字符串, 多个可以用空格分开



## 元素样式

### css()

说明: 获取或设置元素的样式

语法: 

- `jqObj.css(styleName[,style])`
  - 获取或修改单个样式
- `jqObj.css({styleName:style[,styleName:style]*})`
  - 修改多个样式

### 元素位置

**offset()**

说明: 获取/设置元素相对页面的left和top

语法: `jqObj.offset([{left:value, top:value}])`

- **return** 返回一个对象包含`left`和`top`值

**position()**

说明: 获取/设置元素相有定为的祖先的left和top, 不计算margin值

语法: `jqObj.position([{left:value, top:value}])`

- **return** 返回一个对象包含`left`和`top`值

### 滚动距离

**scrollTop()**

说明: 获取/设置scrollTop

语法: `jqObj.scrollTop([value])`

**scrollLeft()**

说明: 获取/设置scrollLeft

语法: `jqObj.scrollLeft([value])`

### 元素尺寸

**width()**

说明: 获取content的width

**heght()**

说明: 获取content的height

**innerWidth()**

说明: 获取content+padding的width

**innerHeight()**

说明: 获取content+padding的height

**outerWidth()**

说明: 获取content+padding+border的width

语法: `outerWidth(true|false)`

- true则包含margin, 默认为false

**outerHeight()**

说明: 获取content+padding+border的height

语法: `outerHeight(true|false)`

- true则包含margin, 默认为false

### 可视区&页面宽高

`$(window).width()`

`$(window).height()`

`$(document).width()`

`$(document).height()`

### 显示/隐藏

**show()**

说明: 显示(改变height,width,opacity)

语法: `jqObj.show([ms|fast|normal|slow])`

**hide()**

说明: 隐藏(改变height,width,opacity)

语法: `jqObj.hide([ms|fast|normal|slow])`

**toggle()**

说明: 切换显示/隐藏(改变height,width,opacity)

语法: `jqObj.toggle([ms|fast|normal|slow])`

fadeIn()

说明: 淡入(改变opacity)

fadeOut()

说明: 淡出(改变opacity)

fadeToggle()

说明: 切换显示/隐藏(改变opacity)

slideDown()

说明: 下滑显示(改变height)

slideUp()

说明: 上滑隐藏(改变height)

slideToggle()

说明: 切换显示/隐藏(改变height)

# 删除/添加操作

## 删除

### jqObj.remove()

说明: 删除元素

语法: `jqObj.remove()`

- **return** obj 被删除的dom元素, 不会保留行为

### jqObj.detach()

说明: 删除元素

语法: `jqObj.detach()`

- **return** obj 被删除的dom元素, 会保留行为

## 替换

### replaceWith()

说明: 用elem替换jqObj的元素

语法: `jqObj.replaceWith(elem)`

### replaceAll()

说明: 用jqObj替换所有elem

语法: `jqObj.replaceAll(elem)`

## 插入/剪切

### insertBefore()

### before()

### insertAfter()

**after()**

**append()**

说明: 添加到元素中的最后

语法: `jqObj.append(HTML|element|jQuery)`

**appendTo()**

说明: 将元素添加到指定元素中的最后

语法: `jqObj.appendTo(jqObj|selector)`

**prepend()**

**prependTo()**

> 以上的操作如果使用的source是已有的元素,则执行的是剪切操作

## 复制

**clone()**

说明: 复制节点(包括子元素), 默认不会复制行为

语法: `jqObj.clone(itself[, son])`

- **itself** bool 默认为false, true则表示复制行为
- **son** bool 默认与itself相同, true则表示复制行为

# 链式操作

### jqObj.end()

说明: 后退链式操作

示例

```js
$('div').next().css('background', 'red').end('color', 'green')
```

### jqObj.addBack()

说明: 将当前和前一个jqObj添加到一起进行操作

### jqObj.add()

说明: 将当前和任意一个jqObj添加到一起进行操作

语法: `jqObj.add(jqObj)`

# 其他操作

## 长度

### length

说明: 获取jqObj包含的DOM元素个数

### size()

说明: 获取jqObj包含的DOM元素个数

## 遍历

### each()

说明: 遍历jqObj

语法: `jqObj.each(callback)`

- **callback(index, domEle)**
  - return false 可以结束遍历

### 获取索引

index()

说明: 获取jqObj在兄弟节点中的index

语法: `jqObj.index([selector])`

### 包装

**wrap()** 

说明: 给每一个元素包上标签

语法: `jqObj.wrap(tag)`

**wrapAll()**

说明: 给整体包上标签

语法: `jqObj.wrapAll(tag)`

**wrapInner()**

说明: 将元素的子节点给包上

**unwrap()**

说明: 删除包装, 不包括body

## 队列操作

### jqObj.queue()

### jqObj.dequeue()