# fs模块

> 内置模块

路径如果是相对路径, 则相对的是执行命令的路径, 而不是执行文件的路径

## 获取文件信息

#### fs.stat

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

## 文件操作

### 文件

#### fs.readFile

说明: 读文件

语法: `fs.readFile(路径 [, 编码], 回调函数)`

* 编码: 默认为Buffer类型
* 回调函数
  * 参数1: 操作的结果信息
  * 参数2: 文件内容

#### fs.readFileSync

说明: 同步读取文件

#### fs.writeFile

说明: 写文件, 有则覆盖, 没有则创建

语法: `fs.writeFile(路径, 内容 [, 选项], 回调函数)`

* 选项
  * encoding: 默认 "utf-8"
  * mode: 文件读写权限, 默认 666
  * flag: 文件系统标志, 默认 "w"
* 回调函数: 只有一个参数, 包含写入文件的结果信息

#### fs.writeFileSync

说明: 同步写文件

#### fs.appendFile

说明: 如果文件存在则追加内容, 不存在则新建

语法: `fs.appendFile(路径, 内容, 回调函数)`

* 回调函数: 只有一个参数, 包含写入文件的结果信息

#### fs.unlink

说明: 删除文件

语法: `fs.unlink(路径, 回调函数)`

### 目录

#### fs.readdir

说明: 读目录

语法: `fs.readdir(路径, 回调函数)`

* 回调函数
  * 参数1: 执行信息
  * 参数2: 目录内的文件(目录)

#### fs.mkdir

说明: 创建文件夹

语法: `fs.mkdir(路径 [,权限] [,回调函数])`

* 权限: 默认777
* 回调函数: 接收一个参数, 创建文件是否成功等信息

#### fs.rename

说明: 可以重命名或移动文件

语法: `fs.rename(源路径, 目标路径, 回调函数)`

#### fs.rmdir

说明: 删除文件夹

语法: `fs.rmdir(路径, 回调函数)`

流操作文件

## 底层文件操作

`fs.open()`

`fs.read(pathname, function (err, data))`

`fs.write`

`fs.close`

### stream

stream是一种有序的数据结构

#### readStream

创建读文本流

示例:

```js
const fs = require('fs');
let rs = fs.createReadStream('filePath', ["enctype=UTF-8"]);
rs.on("data", (data)=>{
    console.log(data);
})
```

**rs对象**

| 方法                   | 说明                                                    | 返回值 |
| ---------------------- | ------------------------------------------------------- | ------ |
| rs.pause()             | 暂停读取数据流                                          |        |
| rs.resume()            | 继续读取数据流                                          |        |
| rs.pipe(anotherStream) | 连接管道, 默认read stream完了之后会自动停止write stream |        |

| 事件  | 说明             |
| ----- | ---------------- |
| data  | 有数据读入时触发 |
| end   | 读取结束         |
| error | 错误信息         |

#### writeStream

创建写文本流

示例:

```js
const fs = require('fs');
let ws = fs.createWriteStream('./hello', [enctype=UTF-8]);
ws.write("hello world")
ws.end(); // 使用`end()`方法来标记写入结束
```

**ws对象**

| 事件   | 说明             |
| ------ | ---------------- |
| drian  | 缓存内容写入完成 |
| finish | 监听写入完成     |

#### pipe

连接管道

示例:

```js
const fs = require('fs');
let rs = fs.createReadStream('./source');
let ws = fs.createWriteStream('./target');
rs.pipe(ws);
```
