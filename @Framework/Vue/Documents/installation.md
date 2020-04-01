# Installation(安装)

### Compatibility Note(兼容性)

Vue does **not** support IE8 and below, because it uses ECMAScript 5 features that are un-shimmable in IE8. However it supports all [ECMAScript 5 compliant browsers](https://caniuse.com/#feat=es5).

> Vue 不支持IE8及以下, 因为它用到ECMAScript5的特性而IE8并不提供. Vue支持所有支持ECMAScript5的浏览器.

### Release Notes(发行记录)

Latest stable version: 2.6.10

> 最新稳定版: 2.6.10

Detailed release notes for each version are available on [GitHub](https://github.com/vuejs/vue/releases).

> 每一个版本的发布信息都在GitHub里面

## [Vue Devtools](https://vuejs.org/v2/guide/installation.html#Vue-Devtools)(Vue 开发工具)

When using Vue, we recommend also installing the [Vue Devtools](https://github.com/vuejs/vue-devtools#vue-devtools) in your browser, allowing you to inspect and debug your Vue applications in a more user-friendly interface.

> 在使用Vue的时候, 我们推荐在你的浏览器里安装Vue开发工具, 这个工具让你可以在一个友好的界面检查和除错. 

## [Direct `<script>` Include](https://vuejs.org/v2/guide/installation.html#Direct-lt-script-gt-Include)(直接包含在script标签中)

Simply download and include with a script tag. `Vue` will be registered as a global variable.

> 简单的下载和安装在一个script标签中. `Vue`将会注册为一个全局变量

Don’t use the minified version during development. You will miss out on all the nice warnings for common mistakes!

> 在开发过程中不要使用最小化版本. 你将会错过所有的常见错误警告.

[Development Version](https://vuejs.org/js/vue.js)With full warnings and debug mode

> 开发版有完整的警告和出错模式

[Production Version](https://vuejs.org/js/vue.min.js)Warnings stripped, 33.30KB min+gzip

> 产品版本警告被精简了, 33.3KB的gzip包

### [CDN](https://vuejs.org/v2/guide/installation.html#CDN)(content delivery network)

For prototyping or learning purposes, you can use the latest version with:

>出于原型设计或者学习, 你可以使用最新的版本

```
<script src="https://cdn.jsdelivr.net/npm/vue"></script>
```

For production, we recommend linking to a specific version number and build to avoid unexpected breakage from newer versions:

> 对于产品, 我们建议你连接到一个特定的版本来避免预料之外的崩溃.

```
<script src="https://cdn.jsdelivr.net/npm/vue@2.6.10/dist/vue.js"></script>
```

If you are using native ES Modules, there is also an ES Modules compatible build:

> 如果你使用本地ES模块, 这里也有一个ES模块的兼容版本:

```
<script type="module">
  import Vue from 'https://cdn.jsdelivr.net/npm/vue@2.6.10/dist/vue.esm.browser.js'
</script>
```

You can browse the source of the NPM package at [cdn.jsdelivr.net/npm/vue](https://cdn.jsdelivr.net/npm/vue/).

Vue is also available on [unpkg](https://unpkg.com/vue@2.6.10/dist/vue.js) and [cdnjs](https://cdnjs.cloudflare.com/ajax/libs/vue/2.6.10/vue.js) (cdnjs takes some time to sync so the latest release may not be available yet).

> 你可以浏览NPM包的源代码在cnd.jsdelivr.net/npm/vue.
>
> Vue也可以从unpkg和csnjs中获取(cdnjs需要一些时间来同步, 所以最新版本或许还不能用)

Make sure to read about [the different builds of Vue](https://vuejs.org/v2/guide/installation.html#Explanation-of-Different-Builds) and use the **production version** in your published site, replacing `vue.js` with `vue.min.js`. This is a smaller build optimized for speed instead of development experience.

>确保阅读有关Vue的不同版本信息并使用产品版本在你的站点, 通过替换掉`vue.js`为`vue.min.js`. 这是一个更小的优化版, 优化了速度.

## [NPM](https://vuejs.org/v2/guide/installation.html#NPM)(Node包管理)

NPM is the recommended installation method when building large scale applications with Vue. It pairs nicely with module bundlers such as [Webpack](https://webpack.js.org/) or [Browserify](http://browserify.org/). Vue also provides accompanying tools for authoring [Single File Components](https://vuejs.org/v2/guide/single-file-components.html).

> 在大项目中推荐使用NPM方式安装Vue. 它和模块捆绑工具匹配较好, 例如Webpack或者Browserify. Vue也为开发者提供了帮助工具--单一文件组件.

```
# latest stable
$ npm install vue
```

## [CLI](https://vuejs.org/v2/guide/installation.html#CLI)(命令行)

Vue provides an [official CLI](https://github.com/vuejs/vue-cli) for quickly scaffolding ambitious Single Page Applications. It provides batteries-included build setups for a modern front-end workflow. It takes only a few minutes to get up and running with hot-reload, lint-on-save, and production-ready builds. See [the Vue CLI docs](https://cli.vuejs.org/) for more details.

> Vue提供一个官方的命令行工具可以快速搭建一个单文件应用. 它给现代前端框架提供了包含电池的套件. 只需要几分钟就可以建立并启动一个可以热重启, 保存时更新, 产品级的版本. 查看Vue命令行文档以获取更多细节.

The CLI assumes prior knowledge of Node.js and the associated build tools. If you are new to Vue or front-end build tools, we strongly suggest going through [the guide](https://vuejs.org/v2/guide/)without any build tools before using the CLI.

> CLI假设你具备Node.js和相关构建工具. 如果你没有接触过Vue或者前端构建工具, 我们强烈建议你先去导览学一下.

[Watch a video explanation on Vue Mastery](https://www.vuemastery.com/courses/real-world-vue-js/vue-cli)

>说明如何掌握Vue的视频

## [Explanation of Different Builds](https://vuejs.org/v2/guide/installation.html#Explanation-of-Different-Builds)(解释不同版本)

In the [`dist/` directory of the NPM package](https://cdn.jsdelivr.net/npm/vue/dist/) you will find many different builds of Vue.js. Here’s an overview of the difference between them:

> 在NPM的`dist/`目录下你可以找到许多不同的Vue.js版本. 这里是一个区别预览

|                               | UMD                | CommonJS              | ES Module (for bundlers) | ES Module (for browsers) |
| :---------------------------- | :----------------- | :-------------------- | :----------------------- | :----------------------- |
| **Full**                      | vue.js             | vue.common.js         | vue.esm.js               | vue.esm.browser.js       |
| **Runtime-only**              | vue.runtime.js     | vue.runtime.common.js | vue.runtime.esm.js       | -                        |
| **Full (production)**         | vue.min.js         | -                     | -                        | vue.esm.browser.min.js   |
| **Runtime-only (production)** | vue.runtime.min.js | -                     | -                        | -                        |

### [Terms](https://vuejs.org/v2/guide/installation.html#Terms)

- **Full**: builds that contain both the compiler and the runtime.

  > 包含编译和运行

- **Compiler**: code that is responsible for compiling template strings into JavaScript render functions.

  > 负责编译模板为js渲染函数

- **Runtime**: code that is responsible for creating Vue instances, rendering and patching virtual DOM, etc. Basically everything minus the compiler.

  >负责创建Vue实例, 渲染和打包虚拟DOM等. 基本上就是去掉了编译器

- **UMD**: UMD builds can be used directly in the browser via a `<script>` tag. The default file from jsDelivr CDN at <https://cdn.jsdelivr.net/npm/vue> is the Runtime + Compiler UMD build (`vue.js`).

  > UMD版本可以直接引入`<script>`标签. 从jsDeliver内容分发网络获取的默认是运行+编译版本

- **CommonJS**: CommonJS builds are intended for use with older bundlers like [browserify](http://browserify.org/) or [webpack 1](https://webpack.github.io/). The default file for these bundlers (`pkg.main`) is the Runtime only CommonJS build (`vue.runtime.common.js`).

  > CommonJS版本倾向于老的捆绑工具像是Browserify或者webpack1. 为这些捆绑工具提供默认仅有运行时的CommonJS包

- **ES Module**: starting in 2.6 Vue provides two ES Modules (ESM) builds:
  - ESM for bundlers: intended for use with modern bundlers like [webpack 2](https://webpack.js.org/) or [Rollup](https://rollupjs.org/). ESM format is designed to be statically analyzable so the bundlers can take advantage of that to perform “tree-shaking” and eliminate unused code from your final bundle. The default file for these bundlers (`pkg.module`) is the Runtime only ES Module build (`vue.runtime.esm.js`).
  
    > ESM捆绑工具版, 倾向于现代捆绑工具像是webpack2或者Rollup. ESM的格式被设计为可静态分析, 所以捆绑工具可以进一步执行减少错误和无用代码. 为这些打包工具提供的默认文件是仅运行时ESM版本.
  
  - ESM for browsers (2.6+ only): intended for direct imports in modern browsers via `<script type="module">`.
  
    > ESM浏览器版倾向于直接引入到现代浏览器

### [Runtime + Compiler vs. Runtime-only](https://vuejs.org/v2/guide/installation.html#Runtime-Compiler-vs-Runtime-only)(对比运行时+编译器和仅仅运行时)

If you need to compile templates on the client (e.g. passing a string to the `template` option, or mounting to an element using its in-DOM HTML as the template), you will need the compiler and thus the full build:

> 如果你需要在客户端编译模板(例如传递一个字符串给`template`选项, 或者挂载一个元素并将其作为模板), 你将会需要有编译器的完整版.

```js
// this requires the compiler
new Vue({
  template: '<div>{{ hi }}</div>'
})

// this does not
new Vue({
  render (h) {
    return h('div', this.hi)
  }
})
```

When using `vue-loader` or `vueify`, templates inside `*.vue`files are pre-compiled into JavaScript at build time. You don’t really need the compiler in the final bundle, and can therefore use the runtime-only build.

> 当使用`vue-loader`或者`vueify`,在`*.vue`中的模板是被编译到javascript代码中的. 你并不需要把编译器放到最终打的包, 你只要用只有运行时的就好.

Since the runtime-only builds are roughly 30% lighter-weight than their full-build counterparts, you should use it whenever you can. If you still wish to use the full build instead, you need to configure an alias in your bundler:

>因为仅运行时版本大概比完整版小了30%, 只要可以你都应该使用它. 如果你依旧希望使用完整版, 你需要在你的bundler里面设置别名:

#### Webpack

```js
module.exports = {
  // ...
  resolve: {
    alias: {
      'vue$': 'vue/dist/vue.esm.js' // 'vue/dist/vue.common.js' for webpack 1
    }
  }
}
```

#### Rollup

```js
const alias = require('rollup-plugin-alias')

rollup({
  // ...
  plugins: [
    alias({
      'vue': require.resolve('vue/dist/vue.esm.js')
    })
  ]
})
```

#### Browserify

Add to your project’s `package.json`:

```
{
  // ...
  "browser": {
    "vue": "vue/dist/vue.common.js"
  }
}
```

#### Parcel

Add to your project’s `package.json`:

```
{
  // ...
  "alias": {
    "vue" : "./node_modules/vue/dist/vue.common.js"
  }
}
```

### [Development vs. Production Mode](https://vuejs.org/v2/guide/installation.html#Development-vs-Production-Mode)(开发和产品模式)

Development/production modes are hard-coded for the UMD builds: the un-minified files are for development, and the minified files are for production.

CommonJS and ES Module builds are intended for bundlers, therefore we don’t provide minified versions for them. You will be responsible for minifying the final bundle yourself.

> 开发/产品模式对于UMD来说未精简的用于开发, 精简了的用于产品.
>
> CommonJS和ES模块倾向于捆绑工具, 所以对他们并没有精简版.你需要自己去精简.

CommonJS and ES Module builds also preserve raw checks for `process.env.NODE_ENV` to determine the mode they should run in. You should use appropriate bundler configurations to replace these environment variables in order to control which mode Vue will run in. Replacing `process.env.NODE_ENV` with string literals also allows minifiers like UglifyJS to completely drop the development-only code blocks, reducing final file size.

> CommonJS和ES模块通过`process.env.NODE_ENV`来侦测要运行哪个模式. 你应该使用适当的捆绑工具的配置来代替环境变量, 从而来控制Vue的运行. 使用文本字符代替`process.env.NODE_ENV`也可以使用例如UglifyJS来完全去除仅用于开发的代码.

#### Webpack

In Webpack 4+, you can use the `mode` option:

> 在Webpack4以上, 你可以使用`mode`选项

```
module.exports = {
  mode: 'production'
}
```

But in Webpack 3 and earlier, you’ll need to use [DefinePlugin](https://webpack.js.org/plugins/define-plugin/):

> 但在Webpack3和更早的版本, 你需要使用DefinePlugin:

```
var webpack = require('webpack')

module.exports = {
  // ...
  plugins: [
    // ...
    new webpack.DefinePlugin({
      'process.env': {
        NODE_ENV: JSON.stringify('production')
      }
    })
  ]
}
```

#### Rollup

Use [rollup-plugin-replace](https://github.com/rollup/rollup-plugin-replace):

> 使用rollup-plugin-replace:

```
const replace = require('rollup-plugin-replace')

rollup({
  // ...
  plugins: [
    replace({
      'process.env.NODE_ENV': JSON.stringify('production')
    })
  ]
}).then(...)
```

#### Browserify

Apply a global [envify](https://github.com/hughsk/envify) transform to your bundle.

>应用全局envify. 转换到你的捆绑

```
NODE_ENV=production browserify -g envify -e main.js | uglifyjs -c -m > build.js
```

Also see [Production Deployment Tips](https://vuejs.org/v2/guide/deployment.html).

> 产品调度

### [CSP environments](https://vuejs.org/v2/guide/installation.html#CSP-environments)

Some environments, such as Google Chrome Apps, enforce Content Security Policy (CSP), which prohibits the use of `new Function()` for evaluating expressions. The full build depends on this feature to compile templates, so is unusable in these environments.

On the other hand, the runtime-only build is fully CSP-compliant. When using the runtime-only build with [Webpack + vue-loader](https://github.com/vuejs-templates/webpack-simple) or [Browserify + vueify](https://github.com/vuejs-templates/browserify-simple), your templates will be precompiled into `render` functions which work perfectly in CSP environments.

## [Dev Build](https://vuejs.org/v2/guide/installation.html#Dev-Build)

**Important**: the built files in GitHub’s `/dist` folder are only checked-in during releases. To use Vue from the latest source code on GitHub, you will have to build it yourself!

```
git clone https://github.com/vuejs/vue.git node_modules/vue
cd node_modules/vue
npm install
npm run build
```

## [Bower](https://vuejs.org/v2/guide/installation.html#Bower)

Only UMD builds are available from Bower.

```
# latest stable
$ bower install vue
```

## [AMD Module Loaders](https://vuejs.org/v2/guide/installation.html#AMD-Module-Loaders)

All UMD builds can be used directly as an AMD module.

[Introduction](https://vuejs.org/v2/guide/index.html) →



Caught a mistake or want to contribute to the documentation?

 

Edit this page on GitHub!