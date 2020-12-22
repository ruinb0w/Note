## vue-resource

vue-resource 用于发送ajax请求

vue-resource 依赖于vue, 所以需要先导入vue,再导入vue-resource

```js
// 示例
{
  // GET /someUrl
  this.$http.get('/someUrl').then(response => {

    // get body data
    this.someData = response.body;

  }, response => {
    // error callback
  });
}
```

[详细文档](https://github.com/pagekit/vue-resource)

### vue-resource配置

| 配置                              | 说明             |
| --------------------------------- | ---------------- |
| Vue.http.options.root="/root"     | 设置默认根路径   |
| Vue.http.options.emulateJSON=true | 默认启用表单格式 |

> 如果要让默认根路径启用, 请求必须为相对路径