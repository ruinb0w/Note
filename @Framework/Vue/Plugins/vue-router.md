# vue-router

说明: vue-router 用于实现前端路由

## 基本使用

1. 引入vue-router

   ```html
   <!--直接通过script标签引用-->
   <script src="vue-router.js"></script>
   ```

2. 创建路由实例

   ```js
   let router = new VueRouter({
       routes: [
           {path: '/login', component: 组件模板对象}, 
           //注意是模板对象, 不是注册后的模板名
           {path: '/register', component: 组件模板对象}
       ]
   })
   ```

3. 在vue实例上挂载路由

   ```js
   let vm = new Vue({
       router: router
       //或者
       router
   })
   ```

4. 在页面放置router-view, 路由指定的组件将会替代这个标签

   ```html
   <router-view></router-view>
   ```

5. 放置router-link, 用于实现路由跳转

   ```html
   <router-link to="/login"></router-link>
   <router-link to="/register"></router-link>
   ```

### 重定向

```js
let router = new VueRouter({
    routes: [
        {path: '/', redirect: '/login'},
        {path: '/login', component: 组件模板对象},
        {path: '/register', component: 组件模板对象}
    ]
})
```

### 高亮router-link

默认对激活的router-link会有一个, 可以自定义激活的类名:

```js
let router = new VueRouter({
    linkActiveClass: '自定义激活类名'
})
```

### 传参

```html
<router-link to="/login?id=10"></router-link>
<script>
    ...
    let login = {
        template: '<h3>{{$route.query.id}}<h3>', //可以直接在组件中使用
        methods:{
            showId(){
                console.log(this.$route.query.id); //也可以在方法中调用
            }
        }
    }
</script>
```

### 路由嵌套

在路由规则上添加children属性

```html
<router-view>
    账户组件
    <router-link to="/account/login">登录</router-link>
    <router-link to="/account/register">注册</router-link>
    <router-view></router-view>
</router-view>
<script>
    let router = new VueRouter({
        routes: [
            {path: "/account",
            component: account,
            children: [
            	{path:'login', component: login},
                {path: 'register', component: register}
        	]}
        ]
    })
</script>
```

### 命名视图

命名视图使用要在routes里面使用components属性, 然后在router-view上加上name属性

default表示默认, 即没有指定name的router-view

```html
<router-view></router-view>
<router-view name="left"></router-view>
<router-view name="main"></router-view>
<script>
    let router = new VueRouter({
        routes: [{
            path: '/',
            components: {
                default: head,
                left: left,
                main: main
            }
        }]
    })
</script>
```

### 手动跳转

```js
this.$router.push("路径");
```

## 进阶使用

### 路由导航守卫

```js
import vueRouter from 'vue-router';
const router = new vueRouter({
    rules: [
        {}
    ]
});

// 设置路由导航守卫
router.beforeEach( (to, from, next())=>{
	if(to.path == '/login') return next();
	const token = window.sessionStorage.getItem('token');
	if(!token) return next('/login');
	next();
})

export default = router;
```

beforeEach函数会在所有路由操作之前执行

to 是要访问的路径

from 是来自的路径

next 执行跳转, 参数为空表示直接跳转, 有路径则强制跳转到该路径