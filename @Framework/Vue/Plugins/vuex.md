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
  },
  action: {
    // 用于放置异步方法
    sumAsync(context){
      setTimeout( ()=>{
          context.commit('add');
      }, 1000)
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
// 在组件中使用getters中的计算属性
$store.getters.sum
// 在实例中使用mutations中的方法
this.$store.commit('方法名'[, 传递的参数])
// 在实例中使用action中的方法
this.$store.dispatch('sumAsync'[, 传递的参数])
```

### 注意

不推荐直接通过`this.$store.state`来操作store中的值, 推荐通过在`mutaions`中定义方法来进行操作

mutation中不可以进行异步操作, 不然会导致页面数据和vuex数据不同不

commit方法只能支持两个参数, 如果需要往`mutations`中传递多个数据, 可以传递对象或数组

action不能直接访问state, 只能通过context.commit来访问commit, 间接的修改state