## http模块

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

常用属性

* `url` url标识
* `headers` 请求报文头(处理为一个对象)
* `rawHeaders ` 请求报文头(未处理的数组)
* `httpVersion` http版本
* `method` 请求的方法

常用事件

* `data` 发生post数据传输时触发
* `end` 数据传输完毕时触发

### res 对象

* `write(chunk[, encoding][, callback])`
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

## util模块

promisify将普通回调函数转化为异步函数

```js
const promisify = requrie("util").promisify;
const fs = require("fs");
const readFile = promisify(fs.readFile);
async function run(){
    let f1 = await readFild('./1.txt', 'utf8');
    let f2 = await readFild('./2.txt', 'utf8');
    let f3 = await readFild('./3.txt', 'utf8');
}
```

## querystring模块

使用方法

```js
const querystring = require('querystring');
let willparse = "name=xiaobai&age=99";
console.log(querysting.parse(willparse));
```

## path模块

path在nodejs中独立为一个模块, 可以通过`require("path")`引入

| 方法                     | 说明                           | 返回值 |
| ------------------------ | ------------------------------ | ------ |
| path.normalize(path)     |                                |        |
| path.join(path[, path]*) | 将传入的多个路径拼接为标准路径 | String |
| path.extname(path)       | 获取文件扩展名                 | String |

`__dirname` 当前文件所在绝对路径

## fs模块

### fs.stat

异步获取文件信息

```js
fs.stat(path, function(err, stat){
	stat.size // 文件大小
    stat.birthtime // 创建时间
    stat.mtime // 最后修改时间
    stat.isFile() // 判断是一个文件
    stat.isDirectory() // 判断是一个目录
});
```

`fs.chmod`

`fs.chown`

### 文件内容读写

### fs.readFile

说明: 读文件

语法: `fs.readFile(filePath[, encoding], function(err,data){})`

* 如果不指定`encoding`则data默认为Buffer对象, 指定了data就是字符串
* `filePath` 如果使用相对路径, 则相对的是执行命令的路径

### fs.writeFile

说明: 写文件

语法: `fs.writeFile(file, content[, options], function(err){})`

`fs.readdir(dir, function(err, files))`

### fs.mkdir

说明: 创建文件夹

语法: `fs.mkdir(path)`



### 底层文件操作

`fs.open()`

`fs.read(pathname, function (err, data))`

`fs.write`

`fs.close`

### stream

stream是一种有序的数据结构

### 读文本流

创建readStream:

```js
var fs = require('fs');
var rs = fs.createReadStream('filePath', [enctype=UTF-8]);
```

**rs对象**

| 方法                   | 说明                                                    | 返回值 |
| ---------------------- | ------------------------------------------------------- | ------ |
| rs.pause()             | 暂停读取数据流                                          |        |
| rs.resume()            | 继续读取数据流                                          |        |
| rs.pipe(anotherStream) | 连接管道, 默认read stream完了之后会自动停止write stream |        |

| 事件 | 说明             |
| ---- | ---------------- |
| data | 有数据读入时触发 |
| end  | 读取结束         |

写文本流

创建writeStream: 

```js
var fs = require('fs');
var ws = fs.createWriteStream('filePath', [enctype=UTF-8]);
ws.end(); // 注意使用`end()`方法来关闭写数据流
```

**ws对象**

| 事件  | 说明             |
| ----- | ---------------- |
| drian | 缓存内容写入完成 |

### Buffer

### 创建Buffer实例

```js
var buffer = new Buffer();
```

**buffer对象**

| 属性           | 说明           |
| -------------- | -------------- |
| buffer[inedex] |                |
| buffer.length  | Buffer实例长度 |

| 方法                                                         | 说明                 | 返回值   |
| ------------------------------------------------------------ | -------------------- | -------- |
| `buffer.write(string[, offset=0][, length][, encoding='utf-8'])` |                      | 写入长度 |
| `buffer.toString(encoding, start=0, end=buffer.length)`      | 将buffer转换为字符串 |          |
| `buffer.copy(target[, tStart][, sStart][, sEnd=buffer.length])` | 将buffer复制到target | 写入长度 |
| buffer.slice(start, end)                                     |                      |          |
| buffer.compare(otherBuffer)                                  |                      |          |
| buffer.equals(otherBuffer)                                   |                      |          |
| buffer.fill(value, offset, end)                              |                      |          |

## https模块

### 创建https服务

https与http的区别在于`https`模块需要额外处理SSL证书

```js
var https = require('https');

var certification = {
        key: fs.readFileSync('./ssl/default.key'),
        cert: fs.readFileSync('./ssl/default.cer')
    };

var server = https.createServer(certification, function (request, response){});

// 添加多组证书
server.addContext('foo.com', {
    key: fs.readFileSync('./ssl/foo.com.key'),
    cert: fs.readFileSync('./ssl/foo.com.cer')
});
```

### 访问https服务

```js
var request = https.request(options, function (response) {});
```

## url模块

### 创建url实例

```js
var url = require('url');
```

### url.parse()

说明: 解析url, 返回一个对象

语法: `url.parse(url[, parseQuery][, noProtocal])`

* parseQuery
  * ture: 将query解析为对象
  * false(默认): query解析为一个字符串
* noProtocal
  * true: 解析不带protocal的url
  * false(默认): 解析带protocal的url