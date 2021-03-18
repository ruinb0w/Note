## nodejs特点

事件驱动

单线程

异步I/O: 

1. nodejs提供了`callback queue`和`async API`
2. 当js调用`async API`时由nodejs接手执行异步操作, 处理完后如果有回调函数则将其放入`callback queue`
3. 当`call stack`中的代码执行完后会查看`callback queue`, 如果有回调函数则加载到`call stack`

[回调loop动画](http://latentflip.com/loupe)

无法通过try-catch捕获异步操作, 只能通过回调函数的`err` 对象来操作(如果有的话)

## 全局对象

nodejs的根对象是`global`, 全局对象和属性就是`global`的属性

## 全局属性

| 属性         | 说明                     |
| ------------ | ------------------------ |
| `__dirname`  | 执行文件所在的目录的路径 |
| `__filename` | 执行文件的路径           |

> 并不是真正的全局属性, 而是module本地属性

## querystring

### 序列化

说明: 将查询对象序列化为字符串

语法: `querystring.stringify(obj[, sep][, eq])`

- sep 连接符
- eq 民之对之间的符号

### 反序列化

说明: 将string反序列化为对象

语法: `querystring.parse(str[, sep][, eq][, max])`

### 转义

语法: `querystring.escape(str)`

### 反转义

语法: `querystring.unescape(str)`

## process

process 对象代表当前进程

| 属性           | 说明                                                         |
| -------------- | ------------------------------------------------------------ |
| `process.argv` | 保存了执行node脚本的参数<br/>argv[0]nodejs程序的路径<br/>argv[1]为js文件的路径<br/>后续则为命令行参数 |

| 方法                         | 说明                               | 返回值 |
| ---------------------------- | ---------------------------------- | ------ |
| `process.nextTick(function)` | 传入的函数将在下一轮事件循环中调用 |        |

## Buffer

### 创建Buffer实例

```js
var buffer = new Buffer();
```

#### buffer对象

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

# 工具

### npm

NPM(Nodejs PackageManager)

#### 安装模块

`npm install [packageName[@version]] [-g]`

- 没有`packageName`则根据package.json文件来安装
- `@version` 表示指定版本, 默认为最新
- `-g` 表示全局安装

#### 注册&发布模块

注册 `npm adduser`

发布 `npm publish [path]`

- 没有path则在当前路径下查找package.json

取消发布 `npm unpublish package@version`

#### 更新

`npm install -g npm@latest`

#### 帮助

`npm help [command]`

#### 初始化package.json

`npm init` 

#### package.json

```json
{
  "name": "",
  "version": "",
  "main": "",
  "scripts": { //scripts中的指令可以通过 `npm run 指令名` 来执行
    "start": "node .",
    "dev": "nodemon ."
  },
  
}
```

## 包

说明: 一个包必须要有`package.json`来进行描述

作用: 将多个子模块放在一个目录下, 通过入口文件来使用.

引入包: require一个包的路径则会自动解析出入口文件

- 默认入口文件名是`index.js`, 可以使用`package.json`来指定入口文件, 示例:

```json
{
	"main": "入口文件路径"
}
```

## package.json

描述包的文件

### package.json常用属性

```json
{
	"name": "包名",  //不可省略
    "version": "版本", //不可省略
    "description": "描述信息",
    "main": "入口文件",
    "dependencies": {
    	"package": "version"    // 依赖的包
    },
    "devDependecies": {
    	"package": "version"  // 开发时用的包
    }
}
```

### package-lock.json

1. npm5新增用于加快安装第三方包
2. 锁定包的版本, 以免在下次下载时出现兼容问题

## node模块加载规则

不省略后缀和路径则直接根据路径来进行查找

省略后缀不省略路径的情况下

1. 先查找路径下同名文件
2. 查找同名文件夹, 并找到`index.js`文件
3. 同名文件夹下没有`index.js`则看`package.json`下`main`字段指定的文件

省略后缀和路径

1. 当作nodeAPI来查找
2. 不是nodeAPI则到node_modules中查找, 匹配规则同省略后缀不省略路径的情况相同

### NVM

说明: NVM(Nodejs Version Manager)

安装:

```sh
pacman -S nvm
```

### nrm

### nodemon
