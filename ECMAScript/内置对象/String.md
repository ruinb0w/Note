# 属性

### str.length

说明: 获取字符串长度

### str[index]

说明: 获取字符串中的某个字符(不能修改)

# 静态方法

### String.fromCharCode()

说明: 返回由Unicode码创建的字符串

语法: `String.fromCharCode(num1,...,numN)`

示例:

```js
String.fromCharCode(66,67,68) // 'BCD'
```

# 实例方法

## 字符串查询

### indexOf()

说明: 从前向后找, 返回找到字符串第一个字符的位置

语法: `string.indexOf(key[, index])`

* **key** string 查找的字符串

* **index** number 查找的起始位置

* **return** number 找不到返回-1

### lastIndexOf()

说明: 从后向前找, 返回找到字符串第一个字符的位置

语法: `string.indexOf(string)`

- **return** number 找不到返回-1

### charAt()

说明: 获取索引位置的字符

语法: `string.charAt([number])`

* **number** 默认为0

- **return** string

### includes()

说明: 如果包含则返回true

语法: `string.includes(string)`

## 字符串转换

### toUpperCase()

说明: 将字符串内容转换为大写

### toLowerCase()

说明: 将字符串内容转换为小写

## 字符串截取

### substring()

说明: 根据开始和结束返回一个子字符串

语法: `string.substring([start,] end)`

* **start** number 起始位置, 没有则视为0
* **end** number 结束位置(不包括)
* **return** string

### substr()

说明: 根据开始和长度返回子字符串

语法: `str.substr(start[, length])`

* **start** number
* **length** number

### slice()

说明: 根据开始和结束返回一个子字符串

语法: `str.slice(beginSlice[, endSlice])`

* **beginSlice** number 起始位置
* **endSlice** number 结束位置(不包括), 没有则视为`str.length`

## 其他

### padStart()

语法: `str.padStart(length, padContent)`

- `Length` 数值, 表示填充后因该有的长度
- `padContent` 字符串, 表示用什么来填充

### padEnd()

语法: `str.padEnd(length, padContent)`

- `Length` 数值, 表示填充后因该有的长度
- `padContent` 字符串, 表示用什么来填充

### replace()

语法: `str.replace("替换目标", "替换内容")`

- 替换目标: 可以式是字符串, 也可以是正则表达式

### split()

说明: 将字符串分割为数组

语法: `str.split([separator[, limit]])`

- **separator** string 分隔符
- **limit** number 切割后保留的个数
- **return** array

### concat()

说明: 字符串拼接, 返回拼接后的字符串

语法: `string.concat(string1,...,stringN)`

- **return** string

### trim()

说明: 去处前后的空字符

语法: `str.trim()`