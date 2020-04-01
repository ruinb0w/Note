## XMLHttpRequest

### 创建 XMLHttpRequest 对象

```js
var xmlhttp = new XMLHttpRequest();
```

### xmlhttp 属性

`xmlhttp.readyState` 异步执行AJAX的状态

`xmlhttp.status` 请求返回的状态码

### xmlhttp 方法

`xmlhttp.open(method, url, sync)`

说明: 打开一个AJAX请求

参数

* method 可以是POST或GET
* url
* sync 为true则是异步, 为false则是同步(不要用)

`xmlhttp.send([string])`

说明: 发送AJAX请求

参数: 用于在POST中发送请求体

### 事件

```js
xmlhttp.onreadystatechange=function(){
  // 判断异步是否执行完成, 判断返回的头部信息是否为200
	if(xmlhttp.readyState === 4 && xmlhttp.status === 200){
  	// 执行的内容
  }
}
```

