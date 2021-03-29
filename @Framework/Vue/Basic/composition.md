# Composition

vue3中加入了Composition API用于提高代码的复用性

> composition-api 提供的函数
>
> * 生命周期hooks
> * setup
> * ref
> * reactive
> * watchEffect
> * watch
> * computed
> * toRefs

## life hook

onMounted

## setup

通过setup选项来使用composition API, setup在beforeCreate 和 created这两个hook之间执行, 所以在setup中不能使用this和methods, 但可以获取到props.

```js
export default{
    name: 'com',
    setup(props, context){
        console.log("msg", props.msg);
        console.log("context", context.attrs, context.slots, context.emit)
    }
}
```

setup接收两个参数 props和 context

### props

props 是一个reactive对象, 如果要使用es6的语法将其中的属性抽出来, 需要使用toRefs

```js
setup(props, context){
    const {name, id} = toRefs(props);
    return {
        name,
        id
    }
}
```

### context

context 是普通对象, 故可用es6的解构语法, 其包含了attrs, slots 和 emit

```js
setup(props, {attrs, slots, emit}){
    console.log('attrs', attrs);
    console.log('slots', slots);
    console.log('emit', emit);
}
```

### render

在setup中可以直接返回一个渲染函数

```js
import { h, ref, reactive } from 'vue'

export default {
  setup() {
    const readersNumber = ref(0)
    const book = reactive({ title: 'Vue 3 Guide' })
    // Please note that we need to explicitly expose ref value here
    return () => h('div', [readersNumber.value, book.title])
  }
}
```

## Reactivity

可以通过 `reactive` 和 `ref` 来声明响应对象



## ref&reactive

ref和reactive用来申明响应式数据

* ref 申明的变量只能通过value属性来改变他的值, 即变量对应的整个值都会改变, 所以如果值是一个对象则会把该对象替换掉,而无法修改对象的属性
* reactive 可用于 object

```vue
<template>
	<div>{{msg}}</div>
	<div @click="changeMsg">changeMsg</div>
	<div>{{name}}</div>
	<div @click="changeName">changeName</div>
	<div>{{book.title}} -- {{book.no}}</div>
	<div @click="changeBookTitle">changeBookTitle</div>
	<div @click="changeBookNo">changeBookNo</div>
</template>
<script>
    import {ref, reactive} from 'vue';
    export default{
        name: 'com',
        setup(){
            // 下面的msg并没有申明为响应式数据, 所以在changeMsg触发后msg值修改了却不会渲染到页面
            let msg = "hello"; 
            const changeMsg = ()=>{
                msg = "hello world"
            }
            
            let name = ref("xiaobai");
            const changeName = ()=>{
                name.value = "xiaohei"
            }
            
            let book = reactive({
                title: '小黄书',
                no: 999
            })
            const changeBookTitle = ()=>{
                book.title = '小白书'
            }
            const changeBookNo = ()=>{
                book.no = '0'
            }
            return {
                msg,
                changeMsg,
                name,
                changeName,
                book,
                changeBookTitle,
                changeBookNo
            }
        }
    }
</script>
```

## toRefs&toRef

将reactive类型的对象的**属性**转化为ref类型的对象, 以此让reactive类型对象的属性可以实现响应式. 

```js
import {reative, toRefs} from 'vue';
export default{
    name: 'com',
    setup(){
        const people = reactive({
            name: 'xiaobai',
            age: 10
        })
        const {name} = toRefs(people);
        return {
            name
        }
    }
}
```

## computed

```vue
<template>
  <div id="container">
    <input v-model="firstName">
    <input v-model="lastName">
    <div >{{fullName}}</div>
  </div>
</template>

<script>
import {reactive, computed, toRefs} from 'vue';
export default{
    name: 'com',
    setup(){
      const people = reactive({
        firstName: 'san',
        lastName: 'zhang'
      })
      const {firstName, lastName} = toRefs(people);
      const fullName = computed( () => {
        return firstName.value + " " + lastName.value
      })
      return {
        firstName,
        lastName,
        fullName
      }
    }
}
</script>
```

## watch&watchEffect

>  注意: watch只能监听 getter/effect 函数, ref/reactive 对象

```vue
<template>
  <div id="container">
    <div >{{vOfWatch}}</div>
    <div >{{vOfWatchEffect}}</div>
  </div>
</template>

<script>
import {reactive, watch, watchEffect} from 'vue'
export default {
  name: 'test',
  setup(){
    const vOfWatch = reactive({
      num: 10
    })
    const vOfWatchEffect = reactive({
      num: 10
    })
    // 1. watch 需要指定监听对象
    // 2. watch 可以得到改变前的值
    watch(()=>vOfWatch.num, (newData, oldData) => {
      console.log('watch', newData, oldData);
    })
    // watchEffect 无需手动指定监听对象
    watchEffect( (arg) => {
      console.log('watchEffect', vOfWatchEffect.num, arg);
    })
    let count = 0;
    const interval = setInterval( () => {
      if (count == 10) {
        clearInterval(interval);
      }
      vOfWatch.num ++;
      vOfWatchEffect.num ++;
      count ++;
    }, 1000)
    return {
      vOfWatch,
      vOfWatchEffect
    }
  }
}
</script>
```

## provide&inject

通过provide和inject可以让子(孙)组件方便的获取父(祖)组件中的值

下面的示例是非响应式

```vue
<!--parent.vue-->
<template>
	<div>{{parantTitle}}</div>
</template>
<script>
    export default{
        name: 'parent',
        data(){
            return{
                parentTitle: 'parent title'
            }
        },
        provide(){
            return{
                parentTitle: this.parentTitle
            }
    	}
    }
</script>
```

```vue
<!--son.vue-->
<template>
	<div>{{parantTitle}}</div>
</template>
<script>
    export default{
        name: 'son',
        inject: ['parentTitle']
    }
</script>
```

下面的示例是响应式

> 需要注意的是, 如果子组件对通过 `inject` 获取的属性进行修改, 会影响父组件. 这是与 `props` 不同的

```vue
<!--parent.vue-->
<template>
	<div>这是父组件---{{parantTitle}}</div>
	下面是子组件
	<son></son>
</template>
<script>
    import {ref, provide} from 'vue';
    import Son from 'Son.vue';
    export default{
        name: 'parent',
        setup(){
            const parentTitle = ref('parent title');
            provide('parentTitle', parentTitle);
            return {
                parentTitle
            }
        },
        components: {
            son: Son
        }
    }
</script>
```

```vue
<!--Son.vue-->
<template>
	<div>{{parantTitle}}</div>
</template>
<script>
    import {inject} from 'vue';
    export default{
        name: 'son',
        setup(){
            let parentTitle = inject("parentTitle");
            return {
                parentTitle
            }
        }
    }
</script>
```

## 组合方法

### setup

说明: 将属性和方法放在一起, 然后通过return将属性和方法暴露出去

```vue
<template>
	<form>
        <input v-modal="tmpStudent.id"/>
        <input v-modal="tmpStudent.name"/>
        <input v-modal="tmpStudent.age"/>
        <button @click="addStudent">添加</button>
    </form>
	<ul>
        <li v-for="(student, index) in students" :key="index" @click="delStudent(index)">
            {{student.name}} - {{student.age}}
    	</li>
    </ul>
</template>
<script>
    import {ref} from "vue";  // 只能监听简单类型的变化
    import {reactive} from "vue";  // 用于监听复杂类型的变化
    export defalt {
        name: 'App',
        setup(){
            const {students, tmpStudent, addStudent, delStudent} = useStudent();
            return {student, tmpStudent, addStudent, delStudent};
        }
    }
    function useStudent(){
        const students = reactive([
            {id: 1, name:'小白', age:10},
            {id: 2, name:'小黑', age:20},
        	{id: 3, name:'小黄', age:30},
        ])
        const tmpStudent = reactive({});
        function addStudent(){
            students.push(Object.assign(tmpStudent));
            tmpStudent.id = '';
            tmpStudent.name = '';
            tmpStudent.age = '';
        }
        function delStudent(index){
            students = students.splice(index, 1);
        }
        return {students, tmpStudent, addStudent, delStudent};
    }
</script>
```

setup 注意点

* 由于setup在created之前(beforeCreated -> setup -> created), 而data和methods在created后才会初始化好, 所以在setup中不能使用data和methods
* setup不能设置为异步

### reactive

注意点

* reactive 只能接收对象作为参数
* 接收的对象如果不是自定义对象/数组, 则修改对象不会更新UI, 如果要更新则需要重新赋值

### ref

给ref传参是深拷贝, ref中数据的变化并不会引起原数据的变化

```js
let p = {name: 'xiaobai'};
let state = ref(p.name);
// 上面等价于 let state = ref('xiaobai');
```



shallowReactive

shallowRef

isReactive

isRef

triggerRef

### toRaw

`import {toRaw} from 'vue';`

从响应式数据中获取原始数据

### markRaw

用markRaw包装的数据不会被追踪

### toRef

对响应式数据的处理会影响原始数据, 且界面不会更新?

```js
let obj = {name: 'xiaobai'}
let state = toRef(obj, 'name');
state.name = 'xiaohei';
console.log(obj); //{name: 'xiaohei'}
console.log(state); // {name: 'xiaohei'}
```

### toRefs

对响应式数据的处理会影响原始数据, 且界面不会更新?

可以传多个值

```js
let obj = {name: 'xiaobai', age: 10}
let state = toRef(obj);
state.name = 'xiaohei';
state.age = 20;
console.log(obj); // {name: 'xiaohei', age: 20}
console.log(state); // {name: 'xiaohei', age: 20}
```

### customeRef

创建自定义ref

### readonly

创建只读数据

### shadllowReadonly

创建第一层只读的数据

### isRadyonly

检查数据类型是否为只读数据