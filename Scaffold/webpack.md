## 简介

**webpack** is a *static module bundler* for modern JavaScript applications.

功能

* 可以处理js文件的依赖关系
* 可以解决浏览器对js的兼容问题

### 安装

```sh
npm install -D webpack
```

## 项目结构

```sh
project
|- dist/
		|- bundle.js # 打包后的文件
|- src/
		|- css/
		|- js/
		|- images/
		|- index.html
		|- main.js # js 入口文件
		|- webpack.config.js # webpack配置文件
```

## main.js

说明: js代码的入口文件

示例:

```js
// 引入js类型的文件
import $ from 'jquery'
// 引入css类型的文件
import './css/style.css'
// 引入less类型文件
import './css/style.less'
// 引入scss类型文件
import './css/style.scss'
```

打包js文件:

```sh
webpack main.js ../dist/budle.js
# webpack 入口文件 目标文件
```

## webpack.config.js

说明: 当执行`webpack`时会在当前路径下查找该文件, 并根据该文件来执行

```js
const path = require('path');

module.exports = {
  // 入口文件
  entry: path.join(__dirname, "src/main.js"),
  // 输出文件
  output: {
    path: path.join(__dirname, "dist"),
    filename: 'bundle.js'
  },
  plugins:[],
  // 用于配置第三方loader
  module:{
    // loader 加载规则
    rules: [
      // use 是从右向左进行编译尝试
      // 字体路径 loader使用规则
      {test: /\.(ttf|eot|svg|woff|woff2)$/, use: 'url-loader'}
    ]
  },
  // 解析
  resolve: {
    // 定义别名
    alias: {
      "vue$": "vue/dist/vue.js"
    }
  }
}
```

> limit=最大转换字节
>
> * 如果使用limit参数,则当图片大于等于最大转换字节使用实际图片,否则会将图片转换为base64
>
> name=[hash:8]-[name].[ext]
>
> * 固定参数名=[hash编码:8位]-[图片名].[后缀名]

## loader

### css

安装:

```
npm install -D style-loader css-loader
```

使用

```js
module {
  rules: [
    {test: /\.css$/, use: ['style-loader', 'css-loader']}
  ]
}
```

### less

安装:

```
npm install -D less-loader less
```

使用

```js
module: {
  rules: [
    {test: /\.less$/, use: ['style-loader', 'css-loader', 'less-loader']}
  ]
}
```

### scss

安装:

```
npm install -D sass-loader node-sass
```

使用

```js
module: {
  rules: [{
    test: /\.scss$/, use: ['style-loader', 'css-loader', 'sass-loader']
  }]
}
```

### url

说明: 解决图片或字体文件的引用问题

安装:

```
npm install -D url-loader file-loader
```

使用:

```js
// 
module{
  rules: [{
  	test: /\.(jpg|png|gif|bmp|jpeg)$/, 
    // 如果图片小于 最大转换字节 则会被转换为base64格式的图片
  	use: 'url-loader?limit=最大转换字节&name=[hash:8]-[name].[ext]'
    // [hash:8]表示保留8位hash值, [name]表示原文件名, [ext]表示原扩展名
	}]
}
```

### babel

说明: 用于解决ES6和ES7的不兼容

安装:

```sh
# babel 核心
npm install -D babel-core babel-loader
# 转换插件
npm install -D babel-plugin-transform-runtime
# 转换规则
npm install -D babel-preset-env babel-preset-stage-0
```

使用

```json
// babel配置文件 `项目/.babelrc`
{
  "presets": ["env", "stage-0"],
  "plugins": ["transform-runtime"]
}
// webpack 配置
module: {
  rules: [{
    test: /\.js$/, use: 'babel-loader', exclude: '/node_modules/'
  }]
}
```

**移除webpack严格模式**

```sh
# 安装插件
npm install -D babel-plugin-transform-remove-strict-mode
# 修改.babelrc
{
	"plugins": ["transform-remove-strict-mode"]
}
```

### vue

安装: 

```
npm install -D vue-loader vue-template-compiler
```

使用

```js
module: {
  rules: [{
    test: /\.vue$/, use: 'vue-loader'
  }]
}
```

## 相关工具

### html-webpack-plugin

说明: 

- 在内存中生成一个页面
- 自动处理bundle.js的引用问题, 不需要在模板页面中引入bundle.js

安装:

```sh
npm install -D html-webpack-plugin
```

使用:

```js
// 在webpack.config.js中
const htmlWebpackPlugin = require("html-webpack-plugin");
// 在plugins属性中添加
plugins: [
  new htmlWebpackPlugin({
    template: 指定的模板页面路径,
    filename: 指定内存中生成页面的名称
  })
]
```

### webpack-dev-server

说明: 

1. webpack-dev-server是一个webpack自动打包工具
2. 其打包生成的`bundle.js`被挂载在本地**服务**的`/`路径上, 并不在本地**磁盘**的`/dist/`中. 需要通过访问本地服务来获取.
3. `budle.js`文件看不到, 但可以直接通过`<script src="/bundle.js">`来引入
4. 如果要使用webpack-dev-server即使全局安装了webpack也需要本地安装webpack

安装:

```sh
npm install -D webpack-dev-server
```

使用:

```sh
webpack-dev-server [选项]
#	选项
# --open 启动时打开项目页面
# --port 指定端口(默认8080)
# --contentBase 指定默认打开路径
# --hot 增量打包, 热刷新
# --host 指定主机IP(默认localhost), 可以使用这个来进行手机端测试
# 示例
webpack-dev-server --open --port 3000 --contentBase src --hot
```

