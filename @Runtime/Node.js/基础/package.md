## 概念

### 模块

nodejs的模块化遵循commonjs规范, 一个文件就是一个模块

#### 导入导出模块

所有模块在执行过程中只初始化一次

模块导出: 可以对`module.exports`或者`exports`来实现对模块的导出

模块导入: 使用`require()`来实现模块导入

> 需要注意的是exports对象起初是module.exports的引用, 所以如果直接对exports进行赋值,则会打断引用.
>
> 而reuiqre方法实际是获取module.exports对象, 所以引用被打断了, 则无法获取到了.

#### 模块路径解析规则

1. 内置模块: 不解析路径, 直接导出模块给变量

2. [自定义模块](https://kdocs.cn/l/cqYbcI2HDlu3)

### 包

包就是一个文件夹, 里面有配置文件和模块, 通常包括

* package.json 包的描述文件
* bin: 二进制可执行文件
* lib: 放js代码
* doc: 存放文档

## package.json

#### dependencies字段

示例:

```json
"dependencies" : {
	"ejs": "^1.2.3",
    "express": "~1.2.3",
    "url": "*1.2.3",
    "axios": "1.2.3"
}
```

> ^ 表示第一位不变, 后面两位安装最新
>
> ~ 表示前两位不变, 最后以为安装最新
>
> \* 表示全部取最新
>
> 不带标识符就固定

## npm

### npm命令

#### 安装第三方包

语法: `npm install [-D] 包名[@版本]`

* 不加版本则安装最新
* `-D` 以开发依赖方式安装

#### 查看全局包位置

`npm root -g`

修改全局包位置

`npm config set prefix '目标目录'`

#### 设置代理

`npm --proxy http://127.0.0.1:12333`

### npm配置

#### 查看 global路径

```shell
npm config get prefix
```

#### npm 指定global路径

1. Make a directory for global installations:

   ```shell
    mkdir ~/.npm-global
   ```

2. Configure npm to use the new directory path:

   ```shell
    npm config set prefix '~/.npm-global'
   ```

#### 查看源

```shell
npm config get registry
```

#### 指定源

```shell
npm config set registry https://registry.npm.taobao.org 
```