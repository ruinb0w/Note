#  gulp

## 简介

说明:

* 压缩合并HTML,CSS,JS
* 语法转换
* 公共文件抽离
* 修改文件,浏览器自动刷新

使用

1. 在项目根目录创建gulpfile.js
2. 在src目录放源文件, 然后就可以在dist目录获取目标文件``

`gulp.src()` 指定源文件

`gulp.dest()` 指定目标目录

`gulp.task()` 建立gulp任务

`gulp.watch()` 监控文件变化

```js
gulp.task('first', ()=>{
	gulp.src('./src/css/base.css').pipe(gulp.dest('./dist/css'))
})
```

gulp是一个自动化构建工具

* 自动编译代码, 如将sass转为css, 将ts转为js.

gulp通过一个命令行工具 `gulp-cli` 来自动构建项目, 具体构建方式在 `gulpfile.js` 中实现

### 配置gulp环境

### 默认任务

gulp命令不跟 task name, 则会执行default task

```js
gulp.task("default", ["task1", "task2"]);
```

### 监听代码

```js
gulp.task("watch", ()=>{
	gulp.watch("文件", ["要执行的task"]);
    gulp.watch(["文件1", "文件2"], ["要执行的task"])
})
```

> 文件单个可以用字符串, 多个用数组, 但task只能放在数组中

## 插件

### gulp-sass

安装

```

```

使用

```js
gulp.task("sass", ()=>{
    return gulp.src("style/index.sass")
    .pipe(sass())
    pipe(gulp.dest("dist/style"));
})
```

### gulp-minify-css

使用

```js
const minifyCss = require('gulp-minify-css');
gulp.task("sass", ()=>{
    return gulp.src("style/index.sass")
    .pipe(minifyCss())
    .pipe(gulp.dest("dist/style"));
})
```

### gulp-rename

使用

```js
const rename = require({'gulp-rename'});
gulp.task("rename", ()=>{
    return gulp.src("style/index.css")
    .pipe(rename("index.renamed.css"))
    .pipe(gulp.dest("dist/style"));
})
```

### gulp-uglify

说明: 用于压缩js文件

安装

使用

```js
const uglify = require({'gulp-uglify'});
gulp.task("uglify", ()=>{
    return gulp.src("style/index.js")
    .pipe(uglify())
    .pipe(gulp.dest("dist/style"));
})
```

## gulp-cli

gulp命令行工具

gulp插件

htlp-htmlmin: html文件压缩

gulp-csso: css压缩

gulp-babel: js语法转化

gulp-less: less语法转化

gulp-uglify: 压缩混淆js

gulp-file-include 公共文件包含

browsersync: 浏览器实时同步