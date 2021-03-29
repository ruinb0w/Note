## vue实例

### 实例属性

示例属性在实例对象中通过this访问

| 属性     | 描述                                                        |
| -------- | ----------------------------------------------------------- |
| $data    | vue组件实例化后的data选项                                   |
| $props   | vue组件实例化后的props选项                                  |
| $el      | 组件挂载的元素                                              |
| $options | 未经实例化组件的所有选项, 通常用于组件的自定义选项          |
| $parent  | 获取父实例, 以此可以访问到父实例的属性                      |
| $root    | 获取根实例                                                  |
| $slot    | 用于渲染函数设置插槽, 例如 `h('div', this.$slot.default())` |

## vue指令

| 指令                         | 说明                                                         |
| ---------------------------- | ------------------------------------------------------------ |
| v-cloak                      | 在vue加载完毕后会去除该属性                                  |
| v-text="值"                  | 在元素中显示文本, 值可以是data中的属性<br/>不会出现插值表达式的延迟问题, 但会直接覆盖元素中的内容 |
| v-html="值"                  | 将值渲染为html                                               |
| v-bind:属性<br/>:属性        | 绑定元素属性                                                 |
| v-on:事件<br/>@事件          | 绑定事件                                                     |
| v-model                      | 数据双向绑定                                                 |
| v-for                        | 遍历数组, 对象, 数字                                         |
| v-if<br/>v-else<br/>v-elseif | 根据if条件来选择显示哪个元素<br/>                            |
| v-show                       | 显示或隐藏某个元素<br/>                                      |

### v-cloak

```html
<style>
    [v-cloak] {
        display:none;
    }
</style>

<div id="app">
    <p v-cloak>
        {{msg}}
    </p>
</div>
```

### v-for

1. 遍历数组

   ```html
   <div v-for="(item, index) in list" :key="item">
       {{index}}---{{item}}
   </div>
   <!--index非必须-->
   ```

2. 遍历对象

   ```html
   <div v-for="(value, key, index) in object" :key="value">
       {{index}} --- {{key}} --- {{value}}
   </div>
   ```

3. 遍历数

   ```html
   <div v-for="index in 10" :key="index">
       这是第{{index}}
   </div>
   ```

> key可以保证数据关联

### v-if vs v-show

`v-if`创建或删除一个元素,切换性能消耗较高

`v-show`使用`style="display:none"`来实现,初始性能消耗较高

### v-model

#### 绑定

**绑定input**

```vue
<template>
	<input v-model="username"/>
</template>
<script>
	export default {
  		name: 'App',
  		data(){
            return {
                username: "小白"
            }
        }
	}
</script>
```

**绑定radio**

```vue
<template>
	<label>
        <input type="radio" name="sex" v-model="sex" value="1"/>男
    </label>
	<label>
        <input type="radio" name="sex" v-model="sex" value="2"/>女
    </label>
</template>
<script>
	export default {
  		name: 'App',
  		data(){
            return {
                sex: 1
            }
        }
	}
</script>
```

**绑定select**

```vue
<template>
	<select v-model="city">
        <option v-for="(item, index) in cityList" :key="index" :value="item">{{item}}</option>
    </select>
</template>
<script>
	export default {
  		name: 'App',
  		data(){
            return {
                cityList: ['北京','上海','广州'],
                city: '北京'
            }
        }
	}
</script>
```

**绑定checkbox**

```vue
<template>
	<label v-for="(item, index) in boxList" :key="index">
        <input type="checkbox" v-model="item.checked"/>{{item.label}}
    </label>
</template>
<script>
	export default {
  		name: 'App',
  		data(){
            return {
                boxList: [
                    {label: '吃饭', checked: true},
                    {label: '睡觉', checked: false},
                    {label: '写代码', checked: false},
                ]
            }
        }
	}
</script>
```

#### 修饰符

| 修饰符    | 说明                                                        |
| --------- | ----------------------------------------------------------- |
| `.number` | 自动转为数字                                                |
| `.trim`   | 自动去除前后空格                                            |
| `.lazy`   | 默认在input事件同步数据, 加上lazy后则会在change事件同步数据 |

#### 组件双向数据绑定

```vue
<!--下面是双向数据绑定的写法, 其实际上是一个语法糖-->
<input v-model="content" />

<!--对于input type=text 其实现方式如下-->
<input :value="content" @input="content = $event.target.value" />

<!--对于组件其实现方式如下, 也就是说它会绑定一个prop名字为 model-value, 子组件可以通过触发 update:model-value 来向父组件传值-->
<custom-input
  :model-value="content"
  @update:model-value="content = $event"
></custom-input>
```

下面是一个简单的示例

```vue
<div id="app">
  father: {{content}} ----- son: <son v-model="content"></son>
</div>
<script>
  const app = Vue.createApp({
    data(){
      return {
        content: 'aaa'
      }
    },
    methods: {
      handleInputFromSon(e){
        console.log('handleInputFromSon', e);
      }
    },
    components: {
      son: {
        template: `<input @input="handleInput" :value="modelValue"/>`,
        props: ['modelValue'],
        emits: ['update:modelValue'],
        methods: {
          handleInput(e){
            console.log("handle son input")
            this.$emit('update:modelValue', e.target.value);
          }
        }
      }
    }
  });
  const mount_point = app.mount("#app");
</script>
```

#### 自定义属性名

`v-model` 可以自定义属性名, 用在父子组件双向数据绑定, 当然你也可以指定多个自定义的双向数据绑定. 通过指定参数来自定义属性名, 例如指定 `v-model:title="title"` 在子组件的props就能拿到 `title` , 更新所需触发的事件也改为 `update:title` , 而不是默认的 `modelValue` 和 `update:modelValue`

下面的例子中当子组件点击click me后, 父组件的fathersTitle将变为"hello world"

```vue
<!--父组件-->
<template>
	<son v-model:fathers_age="fathers_age" v-model:sons_name="sons_name">fathers title is: {{fathersTitle}}</son>
</template>
<script>
    export default{
        data(){
            return {
                fathers_age: 10,
                sons_name: "nick"
            }
        },
        compoents: ['son']
    }
</script>
```

```vue
<!--子组件-->
<template>
	<div @click="changeFathersAge">change fathers name</div>
	<div @click="changeSonsName">change sons name</div>
</template>
<script>
    export default{
        props: {
            fathers_age: Number,
            sons_name: String
        }
        emits: ['update:fathers_age', 'update:sons_name'],
        methods:{
            changeFathersAge(){
                this.$emit("update:fathers_age", this.fathers_age + 1);
            },
            changeSonsName(){
                this.$emit("update:sons_name", 'jack');
            }
        }
    }
</script>
```

#### 自定义修饰符

在父组件中使用了修饰符后, 子组件可以在props中通过 `modelModifiers.修饰符` 访问到该修饰符, 其值为true.

如下例中父组件使用了自定义的 `capitalize` 修饰符, 在子组件中给props选项添加 `modelModifiers` ,我们就可以通过`this.modelModifiers.capitalize`  是否为真来判断父组件的v-model是否用了修饰符, 或用了哪一个.

```vue
<!--父组件-->
<template>
	<son v-model.capitalize:title="title">fathers title is: {{fathersTitle}}</son>
</template>
<script>
    export default{
        data(){
            return {
                title: 'hello world'
            }
        },
        compoents: ['son']
    }
</script>
```

```vue
<!--子组件-->
<template>
	<div @click="capitalizeTitle">capitalize title</div>
</template>
<script>
    export default{
        props: ['modelValue', 'modelModifiers'],
        emits: ['update:modelValue']
        methods:{
            capitalizeTitle(){
                let value = this.title;
                if(this.modelModifiers.capitalize){
                    value = value.charAt(0).toUpperCase() + value.slice(1)
                }
                this.$emit("update:moduleValue", value);
            }
        }
    }
</script>
```

### v-bind

遍历对象放到属性中

```vue
<template>
	<div v-bind="people"></div>
	<!--通过上面的方式绑定渲染后可以得到下面的div-->
	<div name="xiaobai" age="20" pid="0"></div>
</template>
<script>
	export default {
  		name: 'App',
  		data(){
            return {
                people: {
                    name: 'xiaobai',
                    age: 20,
                    pid: 0
                }
            }
        }
	}
</script>
```

### 自定义指令

```js
// 定义全局指令
Vue.directive('指令名', { // 自定义指令在定义时不需要加`v-`前缀, 但在使用时需要加
    bind(el, arg){ // el就是原生的dom对象
        // 在指令绑定到该元素时执行, 函数只执行一次
        // 通常放样式相关的内容
    },
    inserted(el, arg){
        // 元素插入到DOM中时执行, 只触发一次
        // 通常放初始行为相关的内容
    },
    updated(el, arg){
        // 元素更新时执行, 可能触发多次
    }
})

// 定义私有指令
let vm = new Vue({
    el: "app",
    directives: {
        指令名: {}
    }
})
```

使用自定义指令

```html
<div id="app">
    <h2>I'm h2</h2 v-color="'red'">
</div>
<script>
    let vm = new Vue({
        el: 'app',
        directives: {
            'color': {
                bind(el, arg){ // 第一个参数默认为元素, 从第二个参数为传入的内容
                    el.style.color = arg.value;
                }
            }
        }
    })
</script>
```

### 指令属性

`v-bind` 和 `v-on` 指令可以添加属性, 例如

```vue
<template>
	<div v-bind:data="mydata">test</div>
</template>
<script>
export default{
    data(){
        return{
            mydata: 'hello'
        }
    }
}
</script>

<!--我们就得到了-->
<div data="hello">test</div>
```

#### 动态指令属性

```vue
<template>
	<img v-bind:[arg]="{{img_src}}"/>
	<!--use square brakets to wrap dynamic directives-->
</template>
<script>
export default{
    data(){
        return{
            img_arg: 'src',
            img_src: "123.png"
        }
    }
}
</script>

<!--then we got-->
<img v-bind:src="123.png"/>
```

## 事件

### 绑定事件

```vue
<template>
	<!--绑定单个事件处理函数-->
    <div @click="func1" data-name="xiaobai"></div>
	<!--一次绑定多个事件处理函数-->
	<div @click="func1,func2" data-name="xiaobai"></div>
</template>
<sctipt>
    export default {
    	methods: {
    		func1(){console.log("run func1")},
    		func2(){console.log("fun func2")}
    	}
    }
</sctipt>
```

### 事件对象

#### 获取事件对象

处理函数默认会得到一个事件对象

```html
<template>
    <div @click="getname" data-name="xiaobai"></div>
</template>
<sctipt>
    export default {
    	name: 'test',
    	data(){
    		return {
    			
    		}
    	},
    	methods: {
    		getname(e){
    			console.log('name', e.target.dataset.name);
    		}
    	}
    }
</sctipt>
```

#### 事件对象常用属性



### 事件修饰符

| 修饰符        | 说明                                                         |
| ------------- | ------------------------------------------------------------ |
| @事件.stop    | 阻止事件冒泡                                                 |
| @事件.prevent | 阻止默认事件                                                 |
| @事件.capture | 在捕获阶段触发事件(默认是冒泡)                               |
| @事件.self    | 只当在 event.target 是当前元素自身时触发处理函数             |
| @事件.onece   | 只触发一次事件处理函数                                       |
| @事件.passive | 告诉浏览器这个事件是消极的, 即阻止 event.preventDefault() 如此可以优化性能. |

> 事件修饰符可以串联

### 按键修饰符

说明: 按键修饰符用于按键事件, 按键事件有 `keyup`, `keydown`等

语法: `@按键事件.修饰符`, 例如 `@keyup.enter`

vue提供的按键修饰符别名:

- `.enter`
- `.tab`
- `.delete` (captures both "Delete" and "Backspace" keys)
- `.esc`
- `.space`
- `.up`
- `.down`
- `.left`
- `.right`

系统按键修饰符(需要结合其它按键或者鼠标点击)

- `.ctrl`
- `.alt`
- `.shift`
- `.meta`

鼠标按键修饰

- `.left`
- `.right`
- `.middle`

自定义按键修饰符别名

```js
// 通过Vue的config.keyCodes属性即可自定义按键修饰符别名
Vue.config.keyCodes.f1 = 112;
```

### 表单修饰符

| 修饰符       | 说明                           |
| ------------ | ------------------------------ |
| @事件.number | 转换为数字                     |
| @事件.trim   | 去除两边的空格                 |
| @事件.lazy   | 在捕获阶段触发事件(默认是冒泡) |

## 样式

### 使用class

1. 数组

   ```html
   <div :class="['thin', 'red']"></div>
   ```

2. 三元表达式

   ```html
   <div :class="isactive ? 'red' : 'blue' "></div>
   ```

3. 直接使用对象

   ```html
   <div :class="{thin: isTrue}"></div>
   ```


> 数组, 三元表达式和对象可以互相嵌套使用, 从而绑定多个值

你也可以设置默认的class, 它将一直存在.

```vue
<div class="default" :class="{red: is_red}">hello world</div>
```

### 内联样式

1. 对象形式

   ```vue
   <template>
   	<div :style="style"></div>
   </template>
   <script>
   	data: {
   		style: {color:'red', fontSize:'10px'},
   	}
   </script>
   ```

2. 数组形式

   ```vue
   <template>
       <div :style="[style1, style2]"></div>
</template>
   <script>
       data: {
       	style1: {color: 'red', fontSize:'10px'},
       	style2: {margin-top: '10px'}
   	}
   </script>
   ```
   
   

## 过滤器filter

只能用在`mustache`和`v-bind`中

### 公共过滤器

过滤器基本使用

```html
<!--使用过滤器-->
<div>{{name | 过滤器名称1}}</div>

<script>
// 创建过滤器
Vue.filter('过滤器名称1', (data)=>{
    return data+'123';
})
// data默认就是管道符前的值
</script>
```

过滤器可以进行**参数传递**

```html
<div>{{name | 过滤器名称2('哈哈', '呵呵')}}</div>

<script>
Vue.filter('过滤器名称2', (data, arg1, arg2)=>{
    return data+arg1+arg2;
})
</script>
```

过滤器可以**串联使用**

```html
<div>{{name | 过滤器1 | 过滤器2}}</div>
<script>
    Vue.filter('过滤器1',(data)=>{
        return "===" + data;
    });
    Vue.filter('过滤器2',(data)=>{
        return data + "===";
    });
</script>
```

过滤器可用于绑定属性

```html
<div :id="id | 过滤器"></div>
<script>
    Vue.filter('过滤器1',(data)=>{
        return "===" + data;
    });
</script>
```

### 私有过滤器

私有过滤器的优先级高于公共过滤器

```html
<script>
    let vm = new Vue({
        filters: {}
    })
</script>
```

## 监听属性watch

可以用于监听各种属性的改变, 不仅仅只能监听data上的属性, 也可以监听路由

```html
<input v-model="name"/>
<script>
    let vm = new Vue({
        data: {
            name: "xiaobao",
        },
        watch: {
            // 当属性name发生改变时触发
            name(newValue, oldValue){
                console.log(newValue + '---' + oldValue)
            }
        }
	})
</script>
```

## 计算属性computed

计算属性可以当作属性来直接使用

计算属性所指定的函数内部的数据发生改变则会重新计算

```html
firstName: <input v-model="firstName"/>
lastName: <input v-model="lastName"/>
fullName: <input :value="fullName"/>
<script>
    let vm = new Vue({
        data: {
            firstName: 'xiao',
            lastName: 'bai'
        },
        computed: {
            fullName(){
                return this.firstName+this.lastName
            }
        }
    })
</script>
```

计算属性默认只是一个getter, 但你也可以通过把方法改为对象来给计算属性加上setter

```js
computed: {
    fullName: {
        get(){
            return this.first_name + " " + this.last_name;
        },
        set(newVal){
            const [first_name, last_name] = newVal.split(" ");
            this.first_name = first_name;
            this.last_name = last_name;
        }
    }
}
```



## 生命周期

<img src="../../../../../Downloads/lifecycle.svg" alt="lifecycle" style="zoom:80%;" />


### 创建期

beforecreate: 实例刚被创建, 还未初始化data和methods

created: data和methods初始化完成, 还未编译模板

beforeMount: 模板编译完成, 还未挂载到页面

mounted: 模板挂载到页面

### 运行期

beforeUpdate: 状态更新前

updated: 状态更新后

### 销毁期

beforeDestroy: 实例销毁前

destroyed: 实例销毁后

### keep-alive

用于在不同路由切换时缓存组件

```vue
<keep-alive>
    <自定义组件></自定义组件>
</keep-alive>
```

#### activated 和 deactivated

这两个用于缓存的组件, 当缓存的组件被销毁则触发deactivated, 当缓存的组件被恢复则触发activated

### $nextTick

指定在下一周期执行回调函数

```vue
<template>
	<div id="hello">hello</div>
</template>
<script>
    export default {
        name: "nextTick",
        beforeMount(){
            console.log('beforeMount', document.querySelctor("#hello").innerHTML); 
            // 在beforeMount中是访问不到DOM的
            this.$nextTick( =>{
            	console.log('nexttick', document.querySelctor("#hello").innerHTML);
            	// 通过nextTick即可在下一个周期(mounted)访问DOM
            })
        }
    }
</script>
```

## vue过场动画

通过 `transition` 包裹来让元素在显示和隐藏时执行过场动画

![image-20210220213649266](https://i.loli.net/2021/02/20/r2WvSbJxVzI6BM7.png)

其有四个关键帧(v-enter-from, v-enter-to, v-leave-from, v-leave-to) 和两个过程(v-enter-active, v-leave-active).

**关键帧** 用于指定动画的开始和结束, 如果没有结束就以元素的样式作为结束. 

> 需要知道关键帧只是动画, 并不会实际影响元素的样式, 即在动画结束后, 元素会回到它本来的样式.

**过程** 指定动画的相关参数, 如指定运动的属性, 时间, 运动模式. 详见 CSS [transition](https://developer.mozilla.org/en-US/docs/Web/CSS/transition) 属性

### 基础使用方法

```vue
<template>
	<transition>
        <transition name="fade">
        	<div class="hello" v-show="msg && show"> hello world </div>
      	</transition>
      	<div class="button" @click="clickButton">
        	hide/show
      	</div>
    </transition>
</template>
<style>
    .hello{
        position: absolute;
        top: 0;
        transform: translateX(50px); 
        color: red;
      }

      .fade-enter-active,
      .fade-leave-active {
        transition: all 0.5s ease;
      }
      
      .fade-enter-from,
      .fade-leave-to {
        opacity: 0;
        transform: translateX(0px); 
        color: green;
      }

      .button{
        border: 1px solid;
        margin-top: 100px;
      }
</style>
```

### 动画模式

默认情况下, 在两个相互替代的组件进行替换动画时, 两个元素的动画是同时发生的, 这样会造成位移的情况. 而mode可以指定先执行哪个元素的动画

> mode="out-in" 表示先执行退出动画, 再执行进入动画(一般都用这个)
>
> mode="in-out" 表示先执行进入动画, 再执行退出动画

```vue
<transition mode="out-in">
    <div class="button" v-if="stat">on</div>
    <div class="button" v-else>off</div>
</transition>
```

### 动画钩子

```vue
<transition
  @before-enter="beforeEnter"
  @enter="enter"
  @after-enter="afterEnter"
  @enter-cancelled="enterCancelled"
  @before-leave="beforeLeave"
  @leave="leave"
  @after-leave="afterLeave"
  @leave-cancelled="leaveCancelled"
>
  <!-- ... -->
</transition>
<script>
// ...
methods: {
  // --------
  // ENTERING
  // --------

  beforeEnter(el) {
    // ...
  },
  // the done callback is optional when
  // used in combination with CSS
  enter(el, done) {
    // ...
    done()
  },
  afterEnter(el) {
    // ...
  },
  enterCancelled(el) {
    // ...
  },

  // --------
  // LEAVING
  // --------

  beforeLeave(el) {
    // ...
  },
  // the done callback is optional when
  // used in combination with CSS
  leave(el, done) {
    // ...
    done()
  },
  afterLeave(el) {
    // ...
  },
  // leaveCancelled only available with v-show
  leaveCancelled(el) {
    // ...
  }
}
</script>
```

### 使用第三方动画

enter-active-class 指定进入动画

leave-active-class 指定离开动画

duration 指定动画时长

* duration="毫秒数"
* duration="{enter:毫秒数, leave: 毫秒数}"

示例

```html
<link rel="stylesheet" href="./animate.css"/>
<transition enter-active-class="animated bounceIn" 
            leave-active-class="animated bounceOut"
            :duration="200">
    <h3>使用transition包裹要使用动画的元素</h3>
</transition>
```

> 可以在[animate](https://daneden.github.io/animate.css/)获取到各种动画,对于animate来说animated是基础类

### 半场动画

```html
<div id="app">
    <transition @before-enter="beforeEnter"
            @enter="enter"
            @after-enter="afterEnter">
    	<h3>使用transition包裹要使用动画的元素</h3>
	</transition>
</div>
<script>
    let vm = new Vue({
        el:"#app",
        methods:{
            beforeEnter(el){
                el.style.transform="translate(0,0)"
            },
            enter(el, done){
                el.style.transform="translate(100px, 200px)";
                el.style.transition="all 1s ease";
                // 下面两句规定要有
                el.offsetWidth;
                done()
            },
            afterEnter(el){
                this.flag=!this.flag;
            }
        }
    })
</script>

```

### 列表动画

通过 `<transition-group></transition-group>` 来包裹需要动画的列表

需要注意

- 默认情况下 `<transition-group>` 标签不会被渲染出来, 如果要渲染包裹列表的标签则需要用 `tag` 属性指定, 例如指定包裹标签为ul的语法为 `tag="ul"`
- 动画模式不能用在列表
- 列表中的元素必须要用唯一的 `key` , 不能使用index作为key.
- css动画会被用在列表中的元素, 而不是整个列表.
- transition-group同transition一样, 也可以通过name指定进出动画

#### v-move

对于列表元素, 我们可以用 `.v-move` 类样式来指定列表元素移动的动画. 这样列表中的某个元素删除时, 下面的元素会通过动画上移而不是直接跳上来

```css
.v-move{
	transition: transform .8s ease .8s;
}
/* v-move 可以指定作用的transition元素. 例如name="list" 样式就为: */
.list-move{
    transition: transform .8s ease .8s;
}
```

### 组件切换/路由

```html
<transition mode="out-in">
    <component :is="comName"></component>
</transition>
```

## 其它

### ref获取DOM元素或组件

1. 在标签上加上`ref=自定义名字`属性
2. 调用`this.$ref.自定义名字`获取

```html
<p ref="aPhrase">hello world</p>
<script>
    ...
    methods: {
        printText(){
            console.log(this.$ref.aPhrase.innerText);
        }
    }
</script>
```

### render function

```js
const { createApp, h } = Vue

const app = createApp({})

app.component('anchored-heading', {
  render() {
    return h(
      'h' + this.level, // tag name
      {}, // props/attributes
      this.$slots.default() // array of children
    )
  },
  props: {
    level: {
      type: Number,
      required: true
    }
  }
})
```

