## 模块

### 模块分类

<div style="display: flex; background: #f0f1f4">
    <img style="width: 30%" src="https://i.loli.net/2021/02/03/FG8EJ9y4fUacQKx.png">
    <pre >
&bull; 模块可以使用c++,js或者json来写, c++模块的后缀为.node
&bull; 有些模块会被编译到node的二进制文件中,该模块即称为内部模块.有些模块在使用时才会引入,这些模块称为外部模块(或第三方模块).
&bull; 对于内部js模块来说,它会被转为字符串,然后放到二进制文件中, 继而在node运行时放到内存中
&bull; 对于外部c++模块来说,它会通过process.dlopen()方法被动态加载.
	</pre>
</div>

### node在引入模块所要经历的步骤

1. 检查缓存: 

   在缓存中检查模块是否被加载过, 加载过则优先使用加载的模块对象(缓存的是模块导出的对象不是文件)

2. 路径分析: 

   有**模块名**形式和**路径**形式

   ```js
   // 下面两个是模块名形式, 模块名形式会先在核心查找, 找不到则先找当前文件同级的node_modules目录, 找不到就找上一级的node_modules目录, ... 以此类推
   const fs = require('fs');
   const express = require('express');
   // 下面是路径形式, 路径形式就只会按照指定的路径来找
   const hello = require("../hello");
   ```

3. 文件定位:

   1. 分析扩展名(依次自动补上 `.js`, `.json`, `.node` 进行查找)
   2. 如果补全找不到, 但是找到了文件夹名字和模块名匹配, 则进到目录里面找 `packge.json`, 如果有 `main` 字段则以 `main` 为包入口. 
   3. 如果没有`packge.json` 或者没有`main` 或者 `main` 指定的入口不能用, 则在目录里面找`index.js` `index.json` `index.node` 

4. 编译执行

### 其它

#### 浏览器, node与各组织和协议的关系

![image-20210201114620937](https://i.loli.net/2021/02/01/qNRtWygK9aTkCvI.png)

## 包和NPM

### 包

包的结构很简单, 就是几个模块(有一个模块作为整个包的出口)和一个包描述文件

CommonJS规范的包结构如下

* package.json: 包描述文件
* bin: 放可执行文件
* lib: 放js文件
* doc: 放文档
* test: 放单元测试用例

#### package.json

npm和CommonJS包规范

> devDependencies, author, bin, main是npm在commonjs基础上增加的

| 字段            | 说明                                                         | npm  | commonjs |
| --------------- | ------------------------------------------------------------ | ---- | -------- |
| name            | 用于唯一标识一个包                                           | 需要 | 需要     |
| description     | 包的简介                                                     | 需要 | 需要     |
| version         | 版本, 格式: major.minor.revision                             | 需要 | 需要     |
| keywords        | 方便他人找到这个包                                           | 可选 | 需要     |
| repositories    | 托管源码的位置                                               | 需要 | 需要     |
| scripts         | 脚本(npm通过它方便的进行测试编译等)                          | 可选 | 可选     |
| engine          | 支持的js引擎                                                 | 可选 | 可选     |
| dependencies    | 依赖包的列表                                                 | 可选 | 可选     |
| devDependencies | 开发依赖                                                     | 可选 |          |
| author          | 包作者                                                       | 需要 |          |
| bin             | 指出包中可作为命令执行的文件的位置                           | 可选 |          |
| main            | 包的入口                                                     | 需要 |          |
| maintainers     | 维护者, 结构: [{"name": "名字", "email": "邮箱", "web": "个人主页"}, ...] |      | 需要     |
| contributors    | 贡献列表 , 结构通maintinaers                                 |      | 需要     |
| bug             | bug反馈网站或邮箱                                            |      | 需要     |
| licenses        | 许可证列表, 结构: [{"type": "许可证名字", "url": ""}]        |      | 需要     |
| homepage        | 包的网站地址                                                 |      | 可选     |
| os              | 支持的操作系统                                               |      | 可选     |
| cpu             | 支持的处理器                                                 |      | 可选     |
| builtin         | 是否是内 在系统的组件                                        |      | 可选     |
| directories     | 包目录说明                                                   |      | 可选     |
| implements      | 实现的规范列表                                               |      | 可选     |

### npm

npm(nodejs package manager): 用于管理包的工具

#### npm钩子命令

例如下面的package.json中的script字段, `preinstall`和`install`会在`npm install`时执行, `uninstall`也会在`npm uninstall`时执行,

其中的`preinstall`, `install`, `uninstall` 就是npm钩子命令

```json
"scripts": {
	"preinstall": "preinstall.js",
	"install": "install.js",
	"uninstall": "uninstall.js",
	"test": "test.js"
}
```

#### npm 命令

npm adduser 创建npm仓库账户

npm publish 发布包

npm ls 列出当前目录下可以找到的包

### 异步I/O

 异步I/O与非阻塞I/O

### 异步编程

偏函数: 通过指定部分参数来生成一个新的函数的函数. 例如下面的示例:

```js
// isType通过传入type来动态生成一个用于判断类型的函数
const isType = function (type) {
	return function (obj) {
		return toString.call(obj) == '[object ' + type + ']';
	};
};

const isString = isType('String');
console.log("isString?", isString("a string")); //true
console.log("isString?", isString(123)); //false

const isFunction = isType('Function');
console.log("isFunction?", isFunction(()=>{})); //true
```

**多个异步操作统一处理**

```js
const axios = require("axios");

function requestA(){
  let index = axios
    .get("https://zxapi.lcwmkj.cn/cppcc/index?token=M19seHpoenh0b2tlbl8yNQ==")
    .then( (res) => {
      console.log('singal handle', res.data);
      return res.data;
  })
  console.log('index', index);
  let group = axios
    .get("https://zxapi.lcwmkj.cn/cppcc/group_detail?gid=1&token=M19seHpoenh0b2tlbl8yNQ==")
    .then( (res) => {
      console.log('singal handle', res.data);
      return res.data;
  })
  Promise.all([index, group]).then( (res) => {
    console.log('handle all', res);
  })
}

requestA();
```

**同一SQL的高并发**

```js
var proxy = new events.EventEmitter();
var status = "ready";
var select = function (callback) {
proxy.once("selected", callback);
	if (status === "ready") {
		status = "pending";
		db.select("SQL", function (results) {
			proxy.emit("selected", results);
			status = "ready";
		});
	}
};
```

**尾触发**

要手工调用才能继续后续调用的这类方法, 这类方法常用的关键词(名字)是 `next`

## 性能

v8内存限制为1.6G左右, 过大的内存会影响垃圾回收的效率, 而低的垃圾回收效率会让js代码执行hang住.利用堆外内存(Buffer)可以解决内存限制的问题, 因为Buffer并不属于v8而是node自己实现的.

### 垃圾回收

新生代内存区: 使用scavenge算法

老生代内存区: 使用Mark-Sweep ,Mark-Compact和惰性清理

> 需要小心闭包和全局变量

**查看内存占用**

` process.memoryUsage()` 查看node进程相关内存

`os.totalmem()` 查看物理机内存 

`os.freemem()` 查看物理机空闲内存

**查看日志**

```bash
# 生成v8日志
node --prof *.js
# 查看日志
node --prof-process *v8.log
```

### 内存泄漏

#### 常见泄漏场景

**缓存**

由于存在内存限制和垃圾回收效率的平衡问题, 故node的内存是十分昂贵的, 所以不应该大量使用node的内存作为"缓存". 且node的内存并不共享, 所以不同进程之间无法共享"缓存", 所以推荐将"缓存"从node内存中转移出来, 推荐使用 [node-redis](https://github.com/NodeRedis/node-redis) 来管理"缓存".

**队列**

例如日志就可能出现记录速度没有日志生成速度快的问题, 进而导致内存泄漏. 应当对队列采用超时处理机制, 同时对于日志的场景, 应该直接记录到文件中而不是数据库中.

#### 内存泄漏排查

可以通过[node-memwatch](https://github.com/lloyd/node-memwatch) 或 [node-heapdump](https://github.com/bnoordhuis/node-heapdump)

### Buffer

由于v8对内存的使用有限制, 这对大文件来说十分不友好. 同时由于前端开发并不会涉及到二进制数据和文件流, 网络流等, 所以ECMA并没有相关的定义, 但是node却需要面对这些操作. 于是node提供了一个内置模块Buffer, 通过该模块可以在不动用v8的情况下对大文件进行读写. 你可以通过Buffer构造函数来创建出Buffer实例, 同样也可以用fs模块提供的接口, 这些接口使用了Buffer.

```js
let reader = fs.createReadStream("in.txt");
let writer = fs.createWriteStram("out.txt");
reader.on("ready", (chunk)=>{
    writer.write(chunk);
})
reader.on("end", ()=>{
    writer.end();
})

// 当然你可以直接使用pipe, 该方法封装了上面的读写及关闭操作
reader.pipe(writer);
```

对于大量的字节数据, 如果每需要一点就和系统请求一点内存, 就会产生大量的内存申请请求, 所以node通过c++来请求成片的内存, 再通过js来分配.

Node用了slab分配机制,  该机制有一块固定大小的内存以及三个状态, full 分配完了, partial 分配了一部分, empty 还未曾分配. 

对于小的Buffer对象(<8KB), 会先生成一个slab单元, 大小为8KB(你可以通过 `Buffer.poolSize` 得到该值). 然后依据Buffer对象要用的大小来分slab单元. 如果当前slab不够分就会舍弃当前的slab创建一个新的slab.

对于大的Buffer对象(>8KB), 通过SlowBuffer创建一个slab单元, 该slab单元为Buffer对象独占.



**拼接Buffer**

```js
let chunks = [];
let size = 0;
res.on('data', function (chunk) {
	chunks.push(chunk);
	size += chunk.length;
});
res.on('end', function () {
    const buf = Buffer.concat(chunks, size);
    const str = iconv.decode(buf, "utf-8");
    console.log(str);
})
```

## c/c++

条件编译

```c
#define  A 0  //把A定义为0

#if (A > 1)
  printf("A > 1");  //编译器没有编译该语句,该语句不生成汇编代码
#elif (A == 1)
  printf("A == 1"); //编译器没有编译该语句,该语句不生成汇编代码
#else
  printf("A < 1");   //编译器编译了这段代码，且生成了汇编代码，执行该语句
#endif
```

## other

**global.toString 能用来判断基础类型, 对象, 函数, 数组!**

**优美的代码**

```js
const url_list = [
    "https://www.something.com",
    "https://www.something1.com",
    "https://www.something2.com"
];

const fetchURL = (url) => axios.get(url);

const promise_array = url_list.map(fetchURL);

Promise.all(promise_array)
.then((data) => {
  data[0]; // first promise resolved 
  data[1];// second promise resolved 
})
.catch((err) => {
});
```

## question

**对比commonjs amd cmd umd es6, 为什么node用commonjs浏览器用es6?**

CommonJs定义了文件系统, TCP协议, 数据流, 缓存等

**什么是单元测试? 为什么要用单元测试?**

**什么是线程池?**

**红黑树是什么?**

**es6的class和传统的构造函数有什么区别?**

**下面的util.inherit做了哪些事情, 为什么要有events.EventEmitter.call(this)这句话?**

```js
var events = require('events');
function Stream() {
	events.EventEmitter.call(this);
}
util.inherits(Stream, events.EventEmitter);
```

**编程范式**

指令式, 函数式, 声明式, 过程式

**现在的v8用delete还是重新赋值好?**