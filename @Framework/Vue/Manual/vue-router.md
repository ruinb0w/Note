# 基本使用

## 创建和使用

### 创建路由实例

```js
var routerObj = new VueRouter({
	// routes数组定义路由规则
  routes: [ 
		// 每条路由都是一个对象
		{path: '路径', component: 组件模板对象(不能是组件的引用名)}
	]
});
```

### 指定路由渲染的router-view

```html
<router-view name="名字"></router-view>

<script>
var routerObj = new VueRouter({
	// routes数组定义路由规则
  routes: [ 
		// 每条路由都是一个对象
		{path: '路径', 
     component: 组件模板对象(不能是组件的引用名), 
     name:"名字"}
	]
});
</script>
```

### 使用路由实例

```html
<div id="myapp">
  <!--由vue-router提供, 用于不同组件的链接, 默认渲染为a标签-->
  <router-link to="路径"></router-link>
  
  <!--由vue-router提供, 用来作为组件的占位符-->
  <router-view></router-view>
</div>

<script>
  var vm = new Vue({
    el: "myapp",
    // ---- 使用路由实例 ----
    router: routerObj
  })
</script>
```

### &ltrouter-link&gt 和 &ltrouter-view&gt

router-link 

1. 会被默认渲染为一个a标签
2. 当其激活是会带有`router-link-active`的类, 可以通过该类来设置激活高亮等效果
   * 可以通过给`vue-router`构造函数添加`linkActiveClass`属性来配置自己的激活类

router-view

1. 用于组件路由的占位, 当路由匹配后会用模板对象替换该元素

## 传参

### query传参

根据url来获取传参

```js
// URL为  ?参数名=参数值 多个参数可以用&分隔, ?参数1=参数值[&参数2=参数值]

var component = {
	template:'<h1>{{ $route.query.参数名 }}</h1>'
}
```

> 使用query传参不用修改路由

### 路由传参

根据路由匹配规则来获取参数

```js
var routerObj = new VueRouter({
  routes: [ 
    // :参数名 的形式来制定获取参数的匹配规则
    {path: '路径/:参数名', component: 模板对象}    
  ]
});
    
var component = {
	template:'<h1>{{ $route.params.参数名 }}</h1>'
}
```

## 路由重定向

```js
var routerObj = new VueRouter({
  routes: [ 
		// 可以使用redirect来重定向
		{path: '路径', redirect:'重定向路径'}
	]
});
```

## 组件嵌套(子路由)

```js
var routerObj = new VueRouter({
  routes: [
    // 通过children来定义子路由, 从而实现组件嵌套
    {path: '路径', 
     component: 模板对象, 
     children:[
      // 子路由(子路由路径前面不加根"/")
      {path: '路径', 模板对象}
    ]}
	]
});
```

## 多组件

```html
<router-view name="组件名1"></router-view>
<router-view name="组件名2"></router-view>

<script>
	var routerObj = new VueRouter({
	  routes: [
	    {path: '路径',
       components: {
         '组件名1': 组件实例对象,
         '组件名2': 组件实例对象
         // 如果组件名为default则会在没有指定name的router-view上放置该组件
       }
      }
    ]
});
</script>
```

## 监听路由

```js
var vm = new Vue({
  el:"#app",
  watch: {
    'this.$route.path': 处理函数([新数据][,旧数据])
  }
})
```

> 由此可以看到watch可以监听vue实例下的所有属性的变化

## vue-router提供的对象

### $route

`$router.http.get()`

### $router

`$router.push(URL)`

说明: 跳转

`$router.go(整数)`

说明: 根据历史来跳转

`$router.forward(正整数)`

说明: 根据历史来跳转

`$router.back(正整数)`

说明: 根据历史来跳转