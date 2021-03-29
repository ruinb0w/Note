vuex用于全局状态管理

[vuex document for vue3](https://next.vuex.vuejs.org/)

### 注意

不推荐直接通过`this.$store.state`来操作store中的值, 推荐通过在`mutaions`中定义方法来进行操作

mutation中不可以进行异步操作, 不然会导致页面数据和vuex数据不同不

commit方法只能支持两个参数, 如果需要往`mutations`中传递多个数据, 可以传递对象或数组

action不能直接访问state, 只能通过context.commit来访问commit, 间接的修改state

