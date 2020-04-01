# 更新元素

### elem.innerHTML

### elem.innerText

说明: 不可以获取和修改隐藏元素的内容

### elem.textContent

说明: 可以获取和修改隐藏元素的内容

# 获取元素

## 属性方式获取

### elem.children

### elem.parentElement

### elem.firstElementChild

### elem.lastElementChild

### elem.previousElementSibling 

前一个兄弟元素

### elem.nextElementSibling 

后一个兄弟元素

## 方法方式获取

### elem.getElementById()

### elem.getElementsByTagName()

- **return** 伪数组

### elem.getElementsByClassName()

### elem.getElementsByName()

### elem.querySelector()

### elem.querySelectorAll()

# 创建元素

### document.write()

说明: 

- 在页面上创建元素
- 如果在页面加载时调用该方法则会添加该内容, 但如果在页面加载完毕后, 该方法会覆盖页面内容!

语法: `document.write("标签的代码及内容")`

### elem.innerHTML

说明: 将元素插入调用该属性的元素

语法: `elem.innerHTML="标签的代码及内容"`

### document.createElement()

说明: 

- 创建DOM元素
- 需要使用``来插入元素

语法: `document.createElement("标签名")`

# 插入元素

### elem.appendChild()

### elem.insertBefore()

# 删除元素

### elem.replaceChild()

### elem.removeChild()

# 元素属性

1. 通常对于只有一个值的属性, 在DOM操作中可以通过boolean值来进行设置
2. 操作元素的`class`属性需要用`.className`

### elem.getAttribute()

说明: 获取元素的属性和自定义属性

# 获取元素信息

## 获取元素位置

### elem.offsetLeft

说明: 元素距离左边的位置

- type number

### elem.offsetRight

说明: 元素距离右边的位置

### elem.scrollTop

说明: 内容向上卷曲出去的距离

### elem.scrollLeft

说明: 内容向左卷曲出去的距离

### elem.getBoundingClientRect()

## 获取元素大小

### elem.offsetWidth

说明: 元素的宽度, 包括边框

### elem.offsetHeight

说明: 元素的高度, 包括边框

### elem.scrollHeight

说明: 元素内容的高度

### elem.scrollWidth

说明: 元素内容的宽度

### elem.clientWidth

说明: 元素可视区的宽度

### elem.clientHeight

说明: 元素可视区的高度

### elem.clientTop

说明: 元素上边框的宽度

### elem.clientLeft

说明: 元素左边框的宽度

 