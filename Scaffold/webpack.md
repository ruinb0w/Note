## Concept

**webpack** is a *static module bundler* for modern JavaScript applications.

### Entry

An **entry point** indicates which module webpack should use to begin building out its internal [dependency graph](https://webpack.js.org/concepts/dependency-graph/)

```js
// webpack.config.js
module.exports = {
  entry: './path/to/my/entry/file.js'
};
```

### Output

The **output** property tells webpack where to emit the *bundles* it creates and how to name these files. 

```js
// webpack.config.js
const path = require('path');
module.exports = {
  entry: './path/to/my/entry/file.js',
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'my-first-webpack.bundle.js'
  }
};
```

### Loaders

Webpack only understands JavaScript and JSON files. **Loaders** allow webpack to process other types of files and convert them into valid [modules](https://webpack.js.org/concepts/modules) that can be consumed by your application and added to the dependency graph.

```js
// webpack.config.js
const path = require('path');

module.exports = {
  output: {
    filename: 'my-first-webpack.bundle.js'
  },
  module: {
    rules: [
      { test: /\.txt$/, use: 'raw-loader' }
    ]
  }
};
```

### Plugins

While loaders are used to transform certain types of modules, plugins can be leveraged to perform a wider range of tasks like bundle optimization, asset management and injection of environment variables.

```js
// webpack.config.js
const HtmlWebpackPlugin = require('html-webpack-plugin'); //installed via npm
const webpack = require('webpack'); //to access built-in plugins

module.exports = {
  module: {
    rules: [
      { test: /\.txt$/, use: 'raw-loader' }
    ]
  },
  plugins: [
    new HtmlWebpackPlugin({template: './src/index.html'})
  ]
};
```

## 使用

webpack默认支持js和json的打包, 但不支持css/img等

支持ES6语法的模块化例如`import default from 'index.js'`

### 命令行使用

#### 安装

```sh
npm install webpack webpack-cli -g
# or
yarn global add webpack webpack-cli
```

#### 使用

打包命令

> 生产模式比开发模式多了一个代码压缩

* 生产模式: `webpack 输入文件 -o 输出文件 --mode=production`
* 开发模式: `webpack 输入文件 -o 输出文件 --mode=development`

### 项目中使用

```sh
npm install webpack webpack-cli --save-dev
```

### 项目结构

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

#### main.js

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

#### webpack.config.js

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
  // 配置插件, 功能比loader强
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
  },
  mode: 'development' mode 分为production和development
}
```

> limit=最大转换字节
>
> * 如果使用limit参数,则当图片大于等于最大转换字节使用实际图片,否则会将图片转换为base64
>
> name=[hash:8]-[name].[ext]
>
> * 固定参数名=[hash编码:8位]-[图片名].[后缀名]

## 压缩

## 其他工具

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
# --contentBase 指定默认打开路径例如 ./bundle/index.html 或 ./bundle
# --hot 增量打包, 热刷新
# --host 指定主机IP(默认localhost), 可以使用这个来进行手机端测试
# 示例
npx webpack-dev-server --open --port 3000 --contentBase src --hot
```

## development mode

### HMR

hot module replacement, HMR避免了更改某个文件, 整个项目重新打包

* 样式文件: `style-loader`默认实现了HMR功能

* html文件: html文件不需要热更新, 但开启HMR会导致html的移动编译失效, 需要修改entry为数组并加上html文件, 

  * 示例:  `entry:['./src/index.js', './src/index.html']`

* js文件:  不能对入口文件进行热更新, 只能对入口引入的js进行热更新, 示例: 

  ```js
  import print from './print.js'
  if(module.hot){
      module.hot.accept('./print.js', ()=>{
          console.log('热更新print.js后会执行该回调函数')
      })
  }
  ```

**通过配置webpack.config.js来启用热更新**

```js
// webpack.config.js
module.exports = {
  devServer: {
    contentBase: path.join(__dirname, 'build'),
    compress: true,
    port: 3000,
   	open: true,
    hot: true //将hot设置为true即可开启HMR
  }
}
```

### source-map

构建后代码出错可以追溯到源代码

使用

```js
module.exports = {
    devtool:'eval-source-map'
}
// 开发环境 eval-source-map
// 生产环境 source-map
```

### oneOf

oneOf中的loader匹配一次就结束, 不会继续匹配

如果对同一文件有多个loader则只能保留一个在oneOf中, 其他的loader需要拿出来

使用

```js
module.exports = {
	module: {
        rules: [
            {
                oneOf: [...] //oneOf中的loader匹配一次就结束, 不会继续匹配
            }
        ]
    }
}
```

### babel缓存

使用

```js
module.exports={
	module: {
        rules: [{
            test: '/\.js$/',
            loader: 'babel-loader',
            options: {
                cacheDIrectory: true
            }
        }]
    }
}
```



## production mode

### 提取css为独立文件

### css兼容性配置

1.  安装`postcss-loader` 和 `postcss-preset-env`
2.  编辑 webpack.config.js

```js
...
module: {
    rules: [
        {
            test: /\.css$/,
            use: [
                ...
                {
                    loader: 'postcss-loader',
                    options: {
                        ident: 'postcss',
                        plugins: ()=>{
                            require('postcss-preset-env')()
                        }
                    }
                }
            ]
        }
    ]
}
...
```

3. edit package.json (you can reference  [browserlist](https://github.com/browserslist/browserslist) to get more options)

```json
{
    "browserlist": {
        "development": [
            "last 1 chrome",
            "last 1 firefox",
            "last 1 safari"
        ],
        "production": [
            ">0.2%",
            "not dead",
            "not op-mini all"
        ]
    }
}
```

4. set nodejs environment in `webpack.config.js` for browserlist (browserlist is not rely on the mode in webpack.config.js)

```js
process.env.NODENV = 'development';
// or
// process.env.NODENV = 'production';
```

### compress for css

1. install `optimise-css-assets-webpack-plugin`

2. import `optimise-css-assets-webpack-plugin` in `webpack.js`

   ```js
   const OptimiseCssAssetsWebpackPlugin = require("optimise-css-assets-webpack-plugin")
   ```

3. set plugin

   ```js
   plugins: [
       new OptimiseCssAssetsWebpackPlugin()
   ]
   ```

### compress for js

just need set `mode = 'production'` in `webpack.config.js`

### compress for html

1. install `html-webpack-plugin`

2. config in `webpack.config.js`

   ```js
   const HtmlWebpackPlugin = require('html-webpack-plugin')
   
   module.exports = {
     ...
     plugins: [
       new HtmlWebpackPlugin({
           template: './src/index.html',
           minify: {
               collapseWhitespace: true,
               removeComments: true
           }
       })
     ]
   }
   ```



## loader

outputPath可以指定输出文件所在的目录

### css

**安装**:

```
npm install -D style-loader css-loader
```

**使用**

```js
module {
  rules: [
    {
        test: /\.css$/, 
        use: [
            // 在html中创建style标签, 把built.js中的样式放里面
            'style-loader', 
            // 把样式合并到built.js文件中
            'css-loader'
        ]
    }
  ]
}
```

### less

**安装**:

```
npm install -D less-loader less style-loader css-loader
```

**使用**

```js
module: {
  rules: [
    {test: /\.less$/, use: ['style-loader', 'css-loader', 'less-loader']}
  ]
}
```

### scss

**安装**:

```
npm install -D sass-loader node-sass style-loader css-loader
```

**使用**

```js
module: {
  rules: [{
    test: /\.scss$/, use: ['style-loader', 'css-loader', 'sass-loader']
  }]
}
```

### url

**说明**

解决图片或字体文件的引用问题

默认处理不了html文件中的img

**安装**:

```
npm install -D url-loader file-loader
```

**使用**:

```js
// 
module{
  rules: [{
  	test: /\.(jpg|png|gif|bmp|jpeg)$/, 
  	use: 'url-loader',
    options: {
        // 图片小于8kb, 就会被base64处理
        limit: 8*1024,
        // 不使用ES6的模块语法
        esModule: false,
        // [hash:8]表示保留8位hash值, [name]表示原文件名, [ext]表示原扩展名
        name: '[hash:8]-[name].[ext]'
    }
  }]
}
```

### html

**说明:**

处理html页面中的图片

负责引入img, 从而能被url-loader处理

**安装:** 

```
yarn add -D html-loader 
```

使用:

```
module: 
	rules: [{
	{
		test: /\.html$/,
		loader: 'html-loader'
	}
}]
```

### file

**说明**

打包其他资源

**安装**

```
yarn add -D file-loader
```

**使用**

```js
module: {
	rules: [
		{
            // 除了test还可以用exclude
			exclude: /\.(css|js|html)$/,
            // 如果只有一个loader可以直接用loader而不需要use
			loader: 'file-loader'
		}
	]
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

## plugins

### html

**说明**

默认创建一个空的HTML文件, 并将output引入到该文件中

template 属性: 复制该文件,并将output引入该文件中

**安装**

```sh
yarn add -D html-webpack-plugin
```

**使用**

```js
const htmlWebpackPlugin = require('html-webpack-plugin')

plugins: [
	new HtmlWebpackPlugin({
        template: '模板html路径'
    })
]
```

### mini-css-extract-plugin

说明: 将built.js中的css提取为单独的文件

安装

```
npm install -D mini-css-wxtract-plugin
```

使用

```js
const MiniCssExtractPlugin = require('mini-css-extract-plugin');
module: {
    rules: [
        {
            test: '/\.css$/',
            use: [
                MiniCssExtractPlugin.loader,
                'css-loader'
            ]
        }
    ]
}
plugins: [
	new MiniCssExtractPlugin({
        // 指定输出路径, 默认为output path下的main.css
        filename: 'build/built.css'
    });
]
```

