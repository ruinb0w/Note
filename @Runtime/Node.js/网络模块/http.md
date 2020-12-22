## http模块

> 内置模块

http模块可以创建http服务器, 也可以通过该模块来访问http服务器

### 创建http服务

```js
const http = require("http");
//创建http服务器实例
var server = http.createServer();

server.on('request', ()=>{
    server.end('ok');
})

// 监听端口
server.listen(3000[, function(err){}]);
```

Content-Type

* text/html
* text/plain
* charset=utf-8

### req 对象

#### 常用属性

| 属性        | 说明                       |
| ----------- | -------------------------- |
| url         | url标识                    |
| headers     | 请求报文头(处理为一个对象) |
| rawHeaders  | 请求报文头(未处理的数组)   |
| httpVersion | http版本                   |
| method      | 请求的方法                 |

#### 常用事件

| 事件 | 说明                   |
| ---- | ---------------------- |
| data | 发生post数据传输时触发 |
| end  | 数据传输完毕时触发     |

### res 对象

#### write

说明: 向客户端发送数据

语法: `write(chunk[, encoding][, callback])`



* `end([data][, encoding][, callback])`
* `setHeader(name, value)` 设置响应头
* `statusCode` 状态码
* `statusMessage` 状态信息
* `writeHead(statusCode[, statusMessage][, headers])` 发送响应头(附带可以进行设置)
  * `res.writeHead(404, {"content-type": "text/html; charset=utf8"});`
  * `res.writeHead(301, {Location: '地址'})` 实现重定向

### 访问http服务

```js
var http = require("http");
var request = http.request(options, function(response));
// options为请求字符串
request.end(); 
```

### 常见HTTP响应代码

200 请求成功

301 重定向

404 资源没有找到

500 服务器端错误

400 请求语法有错