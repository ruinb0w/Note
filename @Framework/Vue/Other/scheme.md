# scheme

## 发布

### 一个项目一个服务器

直接将dist中的内容放到node服务器, 静态目录中即可

### 多个项目放到同一服务器

1. 修改 `vue.config.js` , 确保项目的根路径是服务器的子级, 例如

   ```js
   module.exports = {
     publicPath: process.env.NODE_ENV === 'production' ? '/production-sub-path/' : '/'
     // 根据 process.env.NODE_ENV 来动态设置根目录
     // /production-sub-path/ 指定项目的根路径为/production-sub-path/
   }
   ```

   上面的项目就可以通过 `http://localhost:port/production-sub-path/` 访问到 `vue-router` 的根路由(故vue-router不需要修改)

2. 配置vue-history路由重定向, 每个项目都需要指定重定向, 例如下面就有pet和car两个项目

   ```js
   const history = require("connect-history-api-fallback");
   
   app.use(history({
     rewrites: [
       // 这里只要匹配到根路径为"/pet"的请求就会发送/pet/index.html
       { from: /^\/pet/, to: '/pet/index.html' },
       // 这里只要匹配到根路径为"/car"的请求就会发送/car/index.html
       { from: /^\/car/, to: '/car/index.html' },
     ],
     // verbose: true, 用于打印输出
     htmlAcceptHeaders: ['text/html', 'application/xhtml+xml']
   }));
   ```


## 动态title

index.html

> 确保vue项目的index.html文件中有

```html
<title><%= htmlWebpackPlugin.options.title %></title>
```

router.js 

```js
Vue.use(VueRouter);

const routes = [
    {
        path: "/",
        component: index,
        name: "index",
        meta: {
            title: '首页'
        }
    }]
var router = new VueRouter({
    routes
})

router.beforeEach((to, from, next) => {
    /* 路由发生变化修改页面title */
    if (to.meta.title) {
        document.title = to.meta.title;
    }
    next();
})
export default router;
```

