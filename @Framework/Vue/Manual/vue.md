# vue实例

```js
var vm = new Vue({
	el: "绑定root元素",
  data: {/* 数据 */}, 
  methods: {/* 方法 */},
  filters: {/* 过滤器 */},
  components: {/* 私有组件 */},
  watch: {/* 属性监听  */},
  computed: {/* 计算属性 */},
  render: {/* 渲染组件 */}
});
```

在vm实例中如果想要使用属性或调用方法,需要通过`this.属性名`或者`this.方法名`

当data发生变化时, vue会自动将其渲染到页面上

## 生命周期

```js
var vm = new Vue({
  // ---- 创建阶段 ----
  beforeCreate: function(){
    // 在完成基本事件和生命周期的初始化后执行
    // data和methods中的数据都还没被初始化
  },
  created: function(){
  	// 在初始化data和methods之后执行
  },
  beforeMount: function(){
    // 模板编译完成, 已在内存中, 但还未渲染到页面中
  },
  mounted: function(){
    // 模板已经挂载到页面中
	},
  // ---- 执行阶段 ----
  beforeUpdated: function(){
    // 当数据改变后
  },
  updated: function(){
    // 当重新渲染完成后
  },
  // ---- 销毁阶段 ----
  beforeDestory: function(){
    // 准备进行销毁, 但没有实际销毁
    // 依旧可以使用data, methods等
  },
  destoryed: function(){
  	// 实际销毁, 什么也做不了
	}
})
```

## 过滤器

用过滤器返回值替换插值表达式的内容

```html
<!--调用过滤器-->
<p {{name|过滤器名称(参数)}}><p/>

<script>
  // -- 定义过滤器 --
	// 全局过滤器, 所有vm实例都共享
	Vue.filter("过滤器名称", function(data[,参数]){})
	// 私有过滤器, 优先于全局过滤器
	var vm = new Vue({
    	filters:{
     	 过滤器名: function(data[,参数]){}
    	}
	});
</script>
```

> 参数可以有多个, 第一个固定为要过滤的数据, 后面的根据调用来增加
>
> 过滤器可以串联使用

## 属性监听

监听data中的属性, 发生改变时执行相应的方法

```js
let vm = new Vue({
  data: {
    fakeAge: 10,
    realAge: 0
  },
  watch: {
    // 监听处理函数有两个可选参数, 第一个是新值, 第二个是老值
    fakeAge(newValue, oldValue){
      this.realAge=this.fakeAge+10
    }
  }
})
```

## 计算属性

说明: 

* 实际是一个方法, 但使用时当作属性来用

* function中用到的data发生了改变, 则立即重新计算

* 计算属性的数据会被缓存

示例:

```html
<div id="app">
  <!--firstname和lastname是实际的属性-->
	<input type="text" v-model="firstname"/>
  <input type="text" v-model="lastname"/>
  <!--fullname是计算属性-->
  <input type="text" v-model="fullname"/>
</div>

<script>
	var vm = new Vue({
    el: "#app",
    data: {
      firstname: '',
      lastname: ''
    },
    computed: {
 	   // 函数名就是计算属性名 // 处理函数的返回值会替换使用到的计算属性名
      计算属性名(){return firstname+lastname}
 	 }
	})
</script>
```

# Vue指令

vue指令就是HTML中的自定义属性

## 默认提供的指令

### v-cloak

说明: 在vue渲染后会去掉这个指令可以用来避免插值表达式在渲染之前显示的问题.

语法: `v-cloak`

### v-text

说明: 

- 替换元素的innerText
- 功能和插值表达式相同, 不会出现插值表达式在渲染之前显示的问题. 

语法: `v-text="sentence"`

### v-html

会将module渲染为html, 插值表达式和v-text都做不到

### v-bind

说明: 用于绑定属性, 格式`v-bind:属性="表达式"`

示例: `v-bind:title="mytitle +'哈哈'"` 这样titile的值就为`vue.data.mytitle + "哈哈"`

简写: `:属性="表达式"`

### v-on

说明: 用于绑定事件

语法: `v-on:事件="事件处理函数"`

简写: `@事件`

### v-model

说明: 实现双向数据绑定. 只能用于表单元素.

语法: `v-model="表达式"`

### v-show

增加/移除`display:none`样式, 初始性能消耗较大, 合适频繁切换

### v-if

根据if的规则选择一个表达式为true的组件进行显示

```html
<component1 v-if="表达式"></component1>
<component2 v-else-if="表达式"></component2>
<component3 v-else></component3>
```

### v-for

迭代数组

```html
<p v-for="item in array">{{item}}</p>
<p v-for="(item,index) in array">{{index}} : {{item}}</p>
```

迭代对象

```html
<p v-for="(value, key) in object">{{key}} : {{value}}</p>
<p v-for="(value, key, index]) in object">{{index}} : {{key}} : {{value}}</p>
```

迭代数字

```html
<p v-for="num in count">{{num}}</p>
<!--从1开始到count-->
```

> 遍历的对象可以是一个表达式

key属性

如果不指定key值会导致一些渲染问题

```html
<p v-for="item in list" :key="item.id">{{num}}</p>
```

## 自定义指令

### 全局指令

```js
Vue.directive(指令名称, {
  // elem表示要执行动画的元素, 是一个原生的DOM对象
  bind: function(elem[, binding]){
    // 当指令绑定到元素上时会立即执行一次
  },	
  inserted: function(elem[, binding]){
    // 当元素插入到DOM中时立即执行一次
  },	
  updated: function(elem[, binding]){
    // vNode更新时执行. 可能触发多次
  }
})
// 指令名称是一个字符串.指令名称不加v-前缀,但调用时要加
// elem 就是指令所绑定的元素的DOM对象
// ---- 简写 ----
Vue.directive(指令名称,function(elem[, binding]){
  // 等于挂了bind和updated钩子
})
```

### 私有指令

```js
var vm = new Vue({
  directives:{
    指令名: {
      钩子: function(elem[, binding]){}
    } 
  }
})
// 钩子就是上面的bind,inserted
// ---- 简写 ----
var vm = new Vue({
  directives: function(elem[, binding]){
    // 等于挂了bind和updated钩子
  }
})
```

bingding 对象

- name 指令名(不包括v-)
- value 指令的绑定值
- oldValue 指令的前一个绑定值
- expression 指令表达式的字符串格式

# 修饰符

## 事件修饰符

`@事件.stop` 阻止事件冒泡

`@事件.prevent` 阻止事件默认行为

`@事件.capture` 启用事件捕获

`@事件.self` 只阻止自己冒泡或捕获的事件触发

`@事件.once` 事件只能被触发一次

> 事件修饰符可以串在一起

## 按键修饰符

默认提供的

`@keyup.enter` `@keyup.tab` `@keyup.delete` 删除和退格`@keyup.esc` `@keyup.space` `@keyup.up` `@keyup.down` `@keyup.left` `@keyup.right`

自定义

`@keyup.键盘码`

# 样式操作

## 操作class

绑定class属性, 其值为表达式, 类型可以是字符串, 数组, 对象

字符串

```html
<h1 :class="'red bold'"></h1>
<!--注意如果是字符串, 要用引号包裹-->
```

数组形式

```html
<h1 :class="[red, 'bold']"></h1>
<!--可以是变量也可以直接是字符串, 但变量的值的类型要是字符串-->
```

对象形式

```html
<h1 :class="{red: true, bold: true}"></h1>
<!--flag为true则将对象名添加为类-->
```

数组内嵌对象形式

```html
<h1 :class="['red', {bold: true}]"></h1>
```

## 操作style

通过一个对象来设置样式

```html
<h1 :style="{attr:value}"></h1>
```

通过数组和多个对象来设置样式

```html
<h1 :style="[styleObj1, styleObj2]"></h1>
```

# 动画

![Transition Diagram](https://cn.vuejs.org/images/transition.png)

## 基本动画

如果`transition`不设置name则共用`v-`指定的动画

```html
<transition>
  <h3>
    hello
  </h3>
</transition>

<style>
  .v-enter-to,
  .v-leave {
    opacity: 0;
  }
  .v-enter-active,
  .v-leav-active {
    transition: all 0.3s;
  }
</style>
<!--对于通过vue渲染出的列表, 需要使用transition-group包裹-->
<ul>
	<transition-group>
		<li v-for="item in list">
      {{item}}
    </li>
	</transition-group>
</ul>
```

## 自定义动画类名

如果`transition`指定了name则只使用`name-`的动画

```html
<!--定义动画名为hello-->
<transition name="hello">
  <h3>
    hello
  </h3>
</transition>
<!--设置样式时也以hello作为前缀-->
<style>
  hello-enter-to,
  hello-leav {
    opacity: 0;
  }
  hello-enter-active,
  hello-leav-active {
    transition: all .3s;
  }
</style>
```

## 第三方动画

### 使用第三方动画

````html
<transition enter-active-class="进入的动画类名" leave-active-class="出去的动画类名">
  <h3>
    hello
  </h3>
</transition>
````

### 第三方动画时间

```html
<!--统一指定-->
<transition enter-active-class="进入的动画类名" leave-active-class="出去的动画类名" :duration="毫秒">
  <h3 class="基础类名">
    hello
  </h3>
</transition>
<!--分别指定-->
<transition enter-active-class="进入的动画类名" leave-active-class="出去的动画类名" :duration="{enter: 毫秒, leave: 毫秒}">
  <h3 class="基础类名">
    hello
  </h3>
</transition>
```

## 动画钩子

```html
<transition
  @before-enter="beforeEnter"
  @enter="enter"
  @after-enter="afterEnter"
  @enter-cancelled="enterCancelled"
            
  @before-leave="beforeLeave"
  @leave="leave"
  @after-leave="afterLeave"
  @leave-cancelld="leaveCancelled"
>
</transition>
<script>
  var vm = new Vue({
    el: "",
    data:{},
    methods: {
      // el表示要执行动画的元素, 是一个原生的DOM对象
      beforeEnter: function(el){
        // 动画开始之前元素的状态
        // 例如定义 
        el.style.transform = "translate(0,0)"
      },
      enter: function(el,done){
        // 强制动画刷新(必须写)
        el.offetWidth
        // 动画动画结束后元素的状态, 例如定义 
        el.style.transform = "translate(100px,100px)"
        el.style.transition = "all 0.5s ease"
        // 这里的done其实就是afterEnter函数, 不调用会出现问题
        done();
      },
      afterEnter: function(el){
        // 动画完成之后的操作
        // 如果只执行前半场动画, 则需要在这里将结束状态的样式改为初始样式
        el.style.transform = "translate(0,0)"
      }
    }
  })
</script>
```

## 特殊效果

实现列表删除后, 后面的元素渐渐上浮

```html
<style>
  .v-move {
    transition: all 0.6s ease;
  }
  .v-leave-active {
    position: absolute;
  }
</style>
```

## transition元素

### transition

```html
<!--组件切换模式-->
<transition mode="out-in"></transition><!--先出后进-->
<transition mode="in-out"></transition><!--先进后出-->
```

### transition-group

```html
<transition-group appear tag="ul">
  <!--appear 属性会让transition在插入DOM时执行动画-->
  <!--tag可以指定transition-group会渲染为什么元素, 如果不指定就是一个span-->
</transition-group>
```

# vue组件

组件通过对UI界面进行拆分来减少代码量

> 组件只能有一个根元素

## 公有组件

```html
<!--使用组件-->
<!--注意在html中使用组件时, 如果组件名是驼峰命名, 则需要改为小写并用-分隔-->
<my-com1></my-com1>
<script>
// ---- 先创建模板, 后注册组件 ----
// 创建组件
var com1 = Vue.extend({
  template: "<div>这是一个vue组件</div>" //指定了组件要展示的HTML结构
});
// 注册组件 Vue.component("组件名称", 组件实例对象)
Vue.component("myCom1", com1);
  
// ---- 创建并注册组件 ----
Vue.component("myCom2", Vue.extend({
  template: "<div>这是一个vue组件</div>"
}));
  
// ---- 简写形式的创建并注册组件 ----
Vue.component("myCom3", {
  template: "<div>这是一个vue组件</div>"
});
</script>
```

## 私有组件

```html
<script>
  var vm = new Vue({
    el:"vm",
    components: {
      componentName: { // 定义组件名
        template: "" // 组件对应的template
      }
    }
  })
</script>
```

## 抽离出template

```html
<!-- 使用组件, template元素不会显示, 而需像挂载组件一样进行渲染 -->
<myCom4></myCom4>

<!-- 通过 id来指定template-->
<!-- 注意: 标签名一定要是template -->
<template id="tmp4"></template>

<script>
	Vue.component("myCom4", {
	  template: "#tmp4"
	});
</script>
```

## data

组件的data

```html
<script>
  Vue.component("com", {
    template: "<h1></h1>",
    // 组件的data会在组件挂载前执行函数来初始化, 避免同一组件复用导致的数据污染
    data: function(){
      return {};
    }
  })
</script>
```

## 子组件与父组件通讯

### 父组件向子组件传值

步骤

1. 在子组件元素中绑定属性 `:parentMsg=msg`

2. 在子组件对象中定义props属性并添加元素中绑定的属性 `props:['parentMsg']`

示例

```html
<div id="app">
  <!--通过属性来将父组件的数据传递给子组件-->
  <com1 :parentmsg="msg"></com1>
</div>

<script>
  var vm = new Vue({
    el: "#app",
    data: {
      msg: "world"
    },
    components: {
      com1: {
        template: "<h1>hello --- {{parentmsg}}</h1>",
        data: function(){
          return {} // data中的数据是可读可写的
        },
        props: ['parentmsg'] // 需要在props中定义后才能使用, props中的数据是只读的
      }
    }
  })
</script>
```

### 父组件向子组件传递方法

同时也可以通过这样来让子组件向父组件传值

```html
<div id="app">
  <!--通过属性来将父组件的数据传递给子组件-->
  <com1 @func="sayhi"></com1>
  <!--func为自定义事件名-->
</div>

<script>
  var vm = new Vue({
    el: "#app",
    data: {},
    methods: {
      sayhi: function(){
        console.log("hello world");
      }
    }
    components: {
      com1: {
        template: "<input type='button' value='sayhi' @click='myclick'/>",
        methods: {
          myclick: function(){
            this.$emit('func'); // 第一个为调用事件名, 后面可以跟参数
          }
        }
      }
    }
  })
</script>
```

## 组件切换

```html
<!--vue定义了component元素-->
<component :is="组件名"></component>
```

## 渲染组件

说明: 用于vue的runtime-only模式, 该模式下无法使用vm实例的components属性

```js
var login = {
  template: "<h1>这是login组件</h1>"
}

var vm = new Vue({
  el: "#app",
  render: function(createElements){
    return createElements(login);
    // return的结果会替换vm实例el属性指定的元素内容
  }
});
```

## .vue文件

```html
<template></template>
<script></script>
<style scoped lang="scss"></style>
```

> scoped 属性可以让样式只作用于自己内部(包括自己和子组件)
>
> lang 属性指定所使用的样式语法

# Vue.config

```js
Vue.config.keyCodes.按键名 = 按键码
// 示例
Vue.config.keyCodes.f2 = 113;
```

# ref

获取DOM对象

步骤

1. 通过给元素添加`ref="变量名"`属性来将DOM对象绑定到`vm.$ref`上
2. 通过访问`vm.$ref.变量名`来操作DOM对象

示例

```html
<div id="myapp">
  <!--通过ref="DOM名称"来获取一个DOM-->
  <span ref="elm">hello world</span>
  <input type="button" value="clickMe" @click="sayhi"/>
</div>

<script>
  var vm = new Vue({
    el:"#myapp",
    methods:{
      sayhi(){
        // 通过vue.$refs.DOM名称来操作一个DOM
        console.log(this.$refs.elm);
      }
    }
  })
</script>
```

