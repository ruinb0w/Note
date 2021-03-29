# 组件

## vue组件的基本结构

### js文件形式

```js
const custom_conponent = {
	template: `<div>{{msg}}</div>`,
    data(){
        return {
            msg: 'hello world'
        }
    }
}
```

### vue文件形式

```vue
<template>
  <div>{{msg}}</div>
</template>

<script>
export default {
  name: 'App',
  data(){
      return {
          msg: 'hello world';
      }
  }
}
</script>
```

## 基本使用

### 全局组件

```html
<!--使用组件-->
<div id="app">
    <my-com1/>
    <my-com2/>
    <my-com3/>
</div>

<template id="tmp1">
    <div>
        <h3>这是com3组件</h3>
    </div>
</template>

<script>
    let vm = new Vue({
        el: "#app"
    })	
    // 1.------- 先创建后注册 ------
    // 创建全局组件
    let com1 = Vue.extend({
		template: "<h3>这是com1组件</h3>"
	})
    // 注册组件
    Vue.component('myCom1', com1);
    
    // 2.----- 直接通过component来创建并注册 -----
    Vue.component('myCom2', {
        template: "<h3>这是com2组件</h3>"
    })
    
    // 3.---- 引用定义在html的模板 -----
    Vue.component('myCom3', {
        template: '#tmp1'
    })
</script>
```

> 如果在注册时使用驼峰命名, 在使用是要用-来分隔
>
> template只能有一个根标签
>
> 引用定义在html的template应当写在#app外, 而使用组件则需要在#app内使用

私有组件

```html
<div id="app">
    <com4/>
</div>

<script>
    let vm = new Vue({
        el: "#app",
        components: {
            com4: {
                template: "<h3>这是com4</h3>"
            }
        }
    })
</script>
```

## 组件选项

### props

props用于指定接收从父组件传给子组件的值, 指定后来自父组件的值会被放到子组件实例中, 之后便可通过this访问.

> 即使不通过props指定 你也可以在子组件中通过 this.$attrs 拿到来自父组件的传值, 但不建议这么做.

#### 将props作为子组件的初始值

或者props的值在子组件中需要改变, 则应当用prop来初始化data

```js
{
    props: ['prop_title'],
	data(){
        return {
            title: prop_title
        }
    },
    methods: {
        changeTitle(){
            this.title += "!";
        }
    }
}
```

> 需要注意, 以上的方法仅仅是浅拷贝, 遇到传入的prop为对象或数组则修改prop的属性同样会影响父组件

#### 指定prop参数

```js
{
    props: {
        title: String, // 指定类型为string
        author: [String, Number] //指定类型为string或numebr
        content: { 
            type: String,
            default: "hello world" // 指定默认值
        },
        id: {
            type: Number,
            validator(val){ // 指定验证函数, 通过第一个参数接prop, 返回true则验证通过
                if(val > 0){
                    return true;
                }
            }
        }
    },
	data(){
        return {
            title: prop_title
        }
    }
}
```

### 非prop属性继承

> 1. 通过$attrs可以获取赋给子组件的属性
> 2. 如果只有一个根节点则属性自动继承到根节点上, 如果有多个根节点则不会自动继承, 事件也是可以继承的.

```vue
<!--父组件-->
<template>
    <my-button class="confirm" test-id="1">确认</my-button> 
	<!--上面的class和test-id会继承给button组件的根元素, 也就是button元素-->
	<my-input class="confirm" test-id="3"></my-input>
	<!--上面的class会继承给div元素, 而test-id会继承给input元素-->
</template>
<script>
    import Button from "Button";
    import input from "Input";
    export default {
        name: "father",
        data(){
            return {
                value: "hello"
            }
        },
        components: {
            "my-button": Button,
            "my-input": Input
        }
    }
</script>
```

```vue
<!--button组件-->
<template>
	<button>
        <slot>默认值</slot>
    </button>
</template>
<script>
    export default {
        name: "button"
    }
</script>
<style>
    .confirm{
        color: blue;
    }
    .cancel {
        color: red
    }
</style>
```

```vue
<!--input组件-->
<template>
	<div :class="$attrs['class']"> <!--手动设置继承的位置-->
        <input :test-id="$attrs['test-id']"/> <!--手动设置继承的位置-->
    </div>
</template>
<script>
    export default {
        name: "input",
        inheritAttrs: false // 禁用默认继承
    }
</script>
<style>
    .confirm{
        color: blue;
    }
    .cancel {
        color: red
    }
</style>
```

#### 继承函数

```vue
<template>
	<div id="app">
  		father: {{content}}<br/>
  		-----
  		<son @input="handleInput"></son>
        <!--
		上面渲染后就得到:
		<div @input="handleInput"><input/></div>
		-->
	</div>
</template>
<script>
  export default {
    data(){
      return {
        content: ''
      }
    },
    methods: {
      handleInput(e){
        this.content = e.target.value; // 子组件触发input事件时父组件可以拿到时间对象
      }
    },
    components: {
      son: {
        template: `<div><input/></div>`,
        data(){
          return {}
        }
      }
    }
  }
</script>
```

### 组件切换

可以通过动态指定组件名来进行组件切换

```html
<component :is="组件名"></component>
```

默认组件切换不会进行缓存(即每次切换都会生成新的vm对象), 可以通过 `<keep-alive>` 标签让组件缓存

```vue
<keep-alive>
    <component :is="组件名"></component>
</keep-alive>
```

### 父子组件传值

#### 父组件向子组件传值

子组件获取父组件的属性和方法有三种方式

1. 在子组件绑定属性
2. 在子组件绑定属性并把 `this` 传给子组件
3. 子组件使用 `this.$parent` 直接获取父组件

示例: 

```vue
<!--父组件-->
<template>
	<!--通过绑定属性来进行传值-->
	<son :msg="msg"></son>
	<!--你可以直接把父组件传给子组件, 但不建议这样做-->
	<son :father="this"></son>
</template>
<script>
    import son from "son";
    export default {
        name: "father",
        data(){
            return {
                msg: "hello son"
            }
        },
        components: {
            son
        }
    }
</script>
```

```html
<!--子组件-->
<template>
	<div>{{father ? father.msg : msg}}</div>
</template>
<script>
    export default {
        name: "son",
        props: ["msg", "father"],
        methods: {
            showFathersMsg(){
                // 子组件可以通过this.$parent来获取父组件和属性和方法, 但不建议这么做
                console.log(this.$parent.msg);
            }
        }
    }
</script>
```

> props中的属性是只读的

#### 子组件向父组件传值

有两种方式从子组件获取值

1. 通过自定义事件来向父组件传值
2. 父组件通过 `$refs` 直接获取子组件中的属性

示例:

```html
<!--父组件-->
<template>
    <!--通过子组件触发自定义事件-->
	<son @getMsgFromSon="getMsgFromSon"></son>
    <!--通过$refs直接获取子组件中的属性-->
    <son ref="son"></son>
</template>
<script>
    import son from "son";
    export default {
        name: "father",
        methods: {
            getMsgFromSon(data){
                console.log(data);
            },
            getArgFromSon(){
                console.log("this.$refs.son.msg");
            }
        }
    }
</script>
```

```vue
<!--子组件-->
<template>
	<div @click="sendMsgToFather"></div>
</template>
<script>
    import son from "son";
    export default {
        name: "son",
        data(){
            return {
                msg: 'hello father'
            }
        },
        methods: {
            sendMsgToFather(){
                this.$emit("getMsgFromSon", this.msg);
            }
        }
    }
</script>
```

> emit触发的事件名要小写(驼峰命名会转为小写)

#### emits

我们可以在 `emits` 属性中添加对 `$emit` 主动触发事件的监听

```vue
<!--子组件-->
<template>
	<div @click="sendMsgToFather"></div>
</template>
<script>
    import son from "son";
    export default {
        name: "son",
        data(){
            return {
                msg: 'hello father'
            }
        },
        emits: {
            getMsgFromSon(msg){
                if(!msg){
                    console.log('you should put something in msg');
                }
            }
        }
        methods: {
            sendMsgToFather(){
                this.$emit("getMsgFromSon", this.msg);
            }
        }
    }
</script>
```

### 自定义事件

#### 事件验证

同props选项, emits同样可以对来自父组件的事件进行验证

```vue
<script>
    emits: {
        sayHi: null, // 不做验证
        doSome(name){
            return name ? true: false // 验证是否有name参数
        }
    }
</script>
```

### 事件中心

事件中心实现了非父子组件之间的传值

在vue2中通过 `$on` 来监听广播, 通过 `$emit` 发送广播来实现实事件中心.

在vue3中去掉了 `$on` `$off` `$once` 我们需要通过第三方的[mitt](https://www.npmjs.com/package/mitt)来实现事件中心

### 自定义组件双向数据绑定

```vue
<!--父组件-->
<template>
    <son v-model:value="value"></son>
</template>
<script>
    import son from "son";
    export default {
        name: "father",
        data(){
            return {
                value: "hello"
            }
        }
    }
</script>
```

```vue
<!--子组件-->
<template>
	<input :value="value" @input="$emit('update:value', $event.target.value)"/>
</template>
<script>
    export default {
        name: "son",
        props: ["value"]
    }
</script>
```

### 属性继承

#### 阻止属性继承

可以通过 `inheritAttrs: false` 选项来阻止当前组件继承. 

#### 继承给某个子组件

在子组件上通过`v-bind="$attrs"` 就可以指定该子组件继承属性

```vue
<template>
	<div>
        <custom-component v-bind="$attrs"></custom-component>
    </div>
</template>
```

#### 多个根标签的属性继承

如果有多个根标签, 需要手动指定谁来继承

```vue
<template>
	<div></div>
	<custom-component v-bind="$attrs"></custom-component>
</template>
```

### slot

插槽分为具名插槽和不具名插槽, 其区别在于是否需要同时指定多个插槽以及是否需要写插槽名.

组件在填写具名插槽时需要使用template标签, 但默认的不需要, 默认插槽内容直接填写就可以, 当然你也可以用

`<template v-slot:default>默认插槽内容</template>`, 如果你有多个具名插槽, 建议这么写, 这样更清晰.

```vue
<!--父组件-->
<template>
	<son>
        <template v-slot:title>
            <div>title</div>
		</template>
        <template v-slot:footer></template>
		<div>main</div>
    </son>
</template>
```

```vue
<!--son组件-->
<template>
	<div>
        <slot name="title">
            标题
    	</slot>
        <slot ></slot>
        <slot name="footer">
            <div>脚</div>
    	</slot>
    </div>
</template>
<!--渲染后得到-->
<template>
	<div>
        <div>title</div>
        <div>main</div>
        <div>脚</div>
    </div>
</template>
```

插槽渲染顺序由子组件定义的顺序来决定: 从上面可以看到, 父组件中插槽的书写顺序是 title - footer - main, 但子组件实际渲染的是 title - main - footer. 

插槽可以填写默认值: 上例中父组件的 footer插槽没有写入内容, 渲染后用的就是子组件写的默认值 "脚".

父组件填写插槽内容会覆盖默认值: 上例中组组件填写了"title"覆盖了子组件插槽中的默认值"标题"

#### 命名插槽的简写

可以用`#插槽名`来代替`v-slot:插槽名`, 但如果这样写的话, 默认插槽就必须要写`#default`

### teleport

将一个组件放到dom中的任意位置, 而不包含在父组件中.

如下面son组件默认会被放到parent组件中, 但通过使用teleport标签指定放置位置后, son组件将会被放到body下面

> to 属性支持css选择器

```vue
<!--parent.vue-->
<template>
	<son></son>
</template>
<script>
    import son from "Son";
    export default {
        name: "parent",
        components: {
            son
        }
    }
</script>
```

```vue
<!--son.vue-->
<template>
	<teleport to="body">
        <div>hello world</div>
    </teleport>
</template>
```

### 异步组件

对于大型应用来说, 一次性从服务器获取整个应用并初始化是十分耗时的, 这是我们应当使用异步组件来解决SPA过大的问题

```js
import { createApp, defineAsyncComponent } from 'vue'

createApp({
  // ...
  components: {
    AsyncComponent: defineAsyncComponent(() =>
      import('./components/AsyncComponent.vue')
    )
  }
})
```

