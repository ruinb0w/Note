## nodejs特点

事件驱动

单线程

异步I/O: 

1. nodejs提供了`callback queue`和`async API`
2. 当js调用`async API`时由nodejs接手执行异步操作, 处理完后如果有回调函数则将其放入`callback queue`
3. 当`call stack`中的代码执行完后会查看`callback queue`, 如果有回调函数则加载到`call stack`

[回调loop动画](http://latentflip.com/loupe)

无法通过try-catch捕获异步操作, 只能通过回调函数的`err` 对象来操作(如果有的话)

## 模块

只要能被`require`的js文件就是一个模块

### 导入导出模块

所有模块在执行过程中只初始化一次

模块导出: 可以对`module.exports`或者`exports`来实现对模块的导出

模块导入: 使用`require()`来实现模块导入

> 需要注意的是exports对象起初是module.exports的引用, 所以如果直接对exports进行赋值,则会打断引用.
>
> 而reuiqre方法实际是获取module.exports对象, 所以引用被打断了, 则无法获取到了.

### 模块路径解析规则

1.内置模块: 不解析路径, 直接导出模块给变量

2.第三方模块(自定义模块)

- 相对路径/绝对路径
- `foo/bar`形式: 会在各处的`node_modules`下进行查找
- `NODE_PATH`环境变量: 与`PATH`类似, 在使用`foo/bar`形式时会在指定路径下查找



## 全局对象&属性

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

## process对象

process 对象代表当前进程

| 属性           | 说明                                                         |
| -------------- | ------------------------------------------------------------ |
| `process.argv` | 保存了执行node脚本的参数<br/>argv[0]nodejs程序的路径<br/>argv[1]为js文件的路径<br/>后续则为命令行参数 |

| 方法                         | 说明                               | 返回值 |
| ---------------------------- | ---------------------------------- | ------ |
| `process.nextTick(function)` | 传入的函数将在下一轮事件循环中调用 |        |

## console

`console.log()`

`console.dir()`

# 工具

## npm

NPM(Nodejs PackageManager)

### 安装模块

`npm install [packageName[@version]] [-g]`

- 没有`packageName`则根据package.json文件来安装
- `@version` 表示指定版本, 默认为最新
- `-g` 表示全局安装

### 注册&发布模块

注册 `npm adduser`

发布 `npm publish [path]`

- 没有path则在当前路径下查找package.json

取消发布 `npm unpublish package@version`

### 更新

`npm install -g npm@latest`

### 帮助

`npm help [command]`

### 初始化package.json

`npm init` 

### package.json

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

## NVM

说明: NVM(Nodejs Version Manager)

安装:

```sh
pacman -S nvm
```

