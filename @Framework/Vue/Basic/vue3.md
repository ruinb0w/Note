## 项目结构

main.js

```js
import { createApp } from 'vue'; //导入创建vm的方法
import App from './App.vue'; //导入根组件
import './index.css';

createApp(App).mount('#app');
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