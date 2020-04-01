vuex用于组件共享数据

### 安装

```sh
npm install -D vuex
```

### 使用

```js
// -- 初始化工作 --
// 导入vuex
import Vuex from 'vuex'
// 注册 Vuex
Vue.use(Vuex);
// 创建store实例
var store = new Vuex.Store({
  state: {
    // 可以理解为data
    count: 0
  },
  mutations: {
    // 可以理解为methods
    increment(state, n){
      state.count += n;
    }
  },
  getters: {
    // 可以理解为computed
    sum(state,c){
      return c + state;
    }
  }
})
// 在App.vue中挂载store实例, 这样该组件及其子组件都能访问到store
let vm = new Vue({
  el: "#app",
  // 挂载store
  store
})

// -- 使用 --
// 在组件中使用store中的属性
$store.state.count
// 在实例中使用mutations中的方法
this.$.store.commit('方法名'[, 传递的参数])
// 在组件中使用getters中的计算属性
$.store.getters.sum
```

### 注意

不推荐直接通过`$store.state`来操作store中的值, 推荐通过在`mutaions`中定义方法来进行操作

commit方法只能支持两个参数, 如果需要往`mutations`中传递多个数据, 可以传递对象或数组