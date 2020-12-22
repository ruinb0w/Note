# 静态方法

### Date.now()

说明: 获取从1970/1/1 到现在的毫秒数

语法: `let time = Date.now()`

* **time** number

# 实例方法

## 获取日期

### date.getFullYear()

说明: 获取年

语法: `let year = date.getFullYear()`

* **year** number

### date.getMonth()

说明: 获取月份. 月份从0开始, 即实际月份为month+1

语法: `let month = date.getFullYear()`

- **month** number

### date.getDate()

说明: 获取一个月的第几号

语法: `let date = date.getDate()`

- **date** number

### date.getDay()

说明: 获取一周的第几天. 从0-6, 0是周末

语法: `let day = date.getDay()`

- **day** number

## 获取时间

### date.getTime()

说明: 获取从1970/1/1到date的毫秒数

语法: `let ms = date.getTime()`

* **ms** number

## 将字日期转换为字符串

```js
date.toDateString() // 'Tue Oct 09 2018'
date.toTimeString() // '15:46:33 GMT+0800 (China Standard Time)'
date.toLocaleDateString() // '10/9/2018'
date.toLocaleTimeString() // '3:46:33 PM'
```

