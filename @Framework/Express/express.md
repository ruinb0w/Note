## 简介

### 基本使用

```js
const express = require('express');
const app = express();

app.get("/", (req, res)=>{
    res.send("hello express");
})

app.listen(3000);
```

app.get/use/post语法

`app.use([路径][, 中间件], 处理函数)`

* 路径: 没有就是根路径
* 中间件: 没有就不用
* 处理函数: 

### app

#### app.use

根据父路由来进行匹配, 没有则是所有

```js
// app.use可以不添加请求地址参数, 只要有请求都会执行
app.use(function(req, res){
    res.send("hello world");
});

// 如果添加了地址, 则即可匹配post,也可匹配get
app.use("/request", (req,res)=>{
    res.send("hello");
})
```

#### app.status

```js
// status可以指定状态码, 并且可以链式调用
app.use((req,res)=>{
    app.status(404).send("当前访问的页面不存在");
})
```

## 路由

### 简单路由

```js
app.METHOD(PATH, HANDLER)
```

### 动态路由

```js
app.get("/user/:id", (req, res)=>{
    app.send(req.params.id);
})

// 请求 /user/123
// 返回 123
```

### 静态资源访问

```js
app.use(express.static('静态资源路径'))
```

### 路由模块化

1. 编写并导出路由

```js
// routes/user.js
const express = require('express');
const router = express.Router();
router.get('/', (req, res)=>{
	res.send('用户首页')
});
router.get('/login', (req, res)=>{
	res.send('登录页')
});
router.get('/about', (req, res)=>{
	res.send('用户信息')
});

module.exports = router;
```

2. 引入并使用路由

```js
const express = require("express");
const app = express();
const user = require("routes/user.js");

app.use("/user", user);
// 当用户访问 域名/user/about就会得到返回值"用户信息"
```

### 错误处理中间件

```js
app.get("/index", (req,res)=>{
    throw new Error("程序发生了未知错误");
})
// 上面抛出错误后就会执行下面的中间件
app.use((err,req,res,next)=>{
    res.status(500).send("服务器出错"+ err.message);
})
// 异步操作错误处理
app.get("/getAFile", (req,res)=>{
    fs.readFile('./nothing', 'utf8', (err, result)=>{
        if(err){
            // 如果next有值则表示要调用错误处理中间件
            next(err);
        }else{
            app.send(result);
        }
    })
})
// try-catch捕获异步函数错误
const readFile = promisify(fs.readFile);
app.get('/index', async (req,res)=>{
    try {
        await readFile('./notExistFile');
    }catch(err){
        next(err);
    }
})
```

### 模块化路由

创建模块化路由

```js
const express = require('express');
const app = express();

// 创建路由对象
const home = express.Router();
// 设置二级路由
home.get('/index', (req,res)=>{
    res.send('欢迎来到首页')
})
module.exports.home = home;
// 设置路由对象路径
app.use('/home', home);
```

引入模块化路由

```js
const home = require('./route/home');

app.use('/home', home)
```

### 获取请求参数

get请求只需要用`req.query`

```js
const bodyParser = require('body-parser');
// 使用bodyParser拦截并处理, 他会自动调用next方法
app.use(bodyParser.urlencoded({extended: false}));
// 在后面就可以获取到post请求参数
app.post('/add', (req,res)=>{
    console.log(req.body)
})
```

### 路由参数

```js
app.get('/index/:id', (req,res)=>{
    // params存储了参数
	console.log(req.params.id);
})
```

### 使用模板引擎

模板

> 模板要放在views文件夹下

```ejs
<h1>
    <%=msg%>
</h1>
```

路由

```js
// 配置模板引擎
app.set("view engine", "ejs");
app.get("/", (req, res)=>{
    res.render("index", {
        msg: "message"
    })
})
```

### 链式路由

使用 `app.route(path)` 然后跟各种http请求

```javascript
app.route('/book')
  .get(function (req, res) {
    res.send('Get a random book')
  })
  .post(function (req, res) {
    res.send('Add a book')
  })
  .put(function (req, res) {
    res.send('Update the book')
  })
```

## 捕获请求

### 正则匹配

路由方法的第一个参数是一个正则表达式, 匹配后会执行回调函数.

```js
app.get("/ab?cd", function(req,res){
    // 这里可以匹配到abcd和acd
	console.log(req.param.name);
});
```

### 捕获URL

用`:varName`的形式来捕获URL

```js
app.get("/:name", function(req,res){
    //假设如果URL为http://localhost:3000/hello
	console.log(req.params.name); // 则打印出 hello
});
```

### 获取query

使用`req.query`属性即可获取query, query会被解析为`query`对象的属性

```js
app.get("/", function(req,res){
    //假设如果URL为http://localhost:3000/?name=xiaoming
    console.log(req.query.name); //打印 xiaoming
});
```

### 获取POST(表单提交数据)

```js
// 需要使用到body-parser模块
var bodyParser = require("body-parser");
app.use(bodyParser.urlencoded({extended:false}));
app.post("/", function(){
	console.log(req.body.name);
});
```

## 中间件

> 匹配路由之前或匹配路由之后进行的一些列操作

### 中间件

```js
// 默认从上到下进行匹配, 匹配后执行并结束, 可以在参数中加入next来进一步进行处理
app.get('/request', (req,res,next)=>{
    res.name='xiaobai';
    next();
});
app.get('/request', (req,res)=>{
    app.send(res.name)
})
```

express中间件通过next()来实现, 例如

```js
const express = require("express");
const app = express();
app.use((req, res, next)=>{
    // 所有路由都会走到这个中间件
    next();
    //调用next()到下一个路由, 不然路由就会在这个中间件终止
}); 
```

上面的例子执行完后, 通过next()到下一个路由. 除了use也可以用post, get等, 只不过use既匹配post也匹配get

> 中间件通常用于实现业务逻辑, 并不向客户端发送响应

### 应用级中间件

> 放在路由前, 用于管理权限等

```js
const express = require("express");
const app = express();
app.use((req, res, next)=>{
    // 所有路由都会走到这个中间件
    next();
    //调用next()到下一个中间件, 不然路由就会在这个中间件终止
}); 
```

### 路由级中间件

> 默认路由匹配后执行完相关逻辑路由就会自动终止, 可以通过next()方法让路由继续尝试匹配规则

```js
const express = require("express");
const app = express();
app.get("/login/add", (req,res,next)=>{
    console.log(req);
    next();
})
app.get("/login/:id", (req,res)=>{
    console.log(req);
})
```

### 错误处理中间件

> 放在路由后, 用于处理错误, 例如没有匹配的路由等

示例

```js
app.use((req,res)=>{
    res.status(404).send("404");
})
```

### 内置中间件

> express内置的中间件, 例如express.static

示例

```js
app.use(express.static("public"));	
```

### 第三方中间件

### next

| Method          | description                                         |
| --------------- | --------------------------------------------------- |
| `next()`        | 执行**同一route**下的下一个中间件, 会构成中间件环   |
| `next('route')` | 执行**下一个同路径route**的中间件, 不会构成中间件环 |

## 处理函数(中间件)的参数

### request

| Parameter       | description                                                  |
| --------------- | ------------------------------------------------------------ |
| req.method      | request method                                               |
| req.originalUrl | the original URL which was requested                         |
| req.query       | get请求参数对象, 如请求`/home?name=xiaobai&age=10`           |
| req.body        | post请求参数                                                 |
| req.params      | 动态路由参数, 如请求 `/home/:id` params就有一个id属性与请求对应 |

### response 

| Method                                                       | async | description                                                  |
| ------------------------------------------------------------ | ----- | ------------------------------------------------------------ |
| [res.download()](https://expressjs.com/en/4x/api.html#res.download) |       | Prompt a file to be downloaded.                              |
| [res.end()](https://expressjs.com/en/4x/api.html#res.end)    |       | End the response process.                                    |
| [res.json()](https://expressjs.com/en/4x/api.html#res.json)  |       | Send a JSON response.                                        |
| [res.jsonp()](https://expressjs.com/en/4x/api.html#res.jsonp) |       | Send a JSON response with JSONP support.                     |
| [res.redirect()](https://expressjs.com/en/4x/api.html#res.redirect) |       | Redirect a request.                                          |
| [res.render()](https://expressjs.com/en/4x/api.html#res.render) |       | Render a view template.                                      |
| [res.send()](https://expressjs.com/en/4x/api.html#res.send)  | *     | Send a response of various types.                            |
| [res.sendFile()](https://expressjs.com/en/4x/api.html#res.sendFile) | *     | Send a file as an octet stream.                              |
| [res.sendStatus()](https://expressjs.com/en/4x/api.html#res.sendStatus) |       | Set the response status code and send its string representation as the response body. |

## 模板引擎

使用`app.set("view engine", "pug");`来指定模板引擎

## express-generator

### 说明

### 使用

安装:

```
yarn global add express-generator
```

使用: 

```
express [选项] [参数] 项目名
```

## Question

**实际操作无法实现**

通过`()`可控的获取一段值

```
Route path: /user/:userId(\d+)
Request URL: http://localhost:3000/user/42
req.params: {"userId": "42"}
```
