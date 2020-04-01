vue-resource可以实现不操作DOM发送get,post,jsonp请求

## 请求

### 常用请求

```js
// ---- get请求 ----
Vue.$http.get(url, [config]).then(successCallback, failedCallback)

// ---- post请求 ----
Vue.$http.post(url, [body], [config]).then(successCallback, failedCallback)
// 在POST请求中最好设置{emulateJSON:true}
// body 是一个对象

// ---- jsonp请求 ----
Vue.$http.jsonp(url, [config]).then(successCallback, failedCallback)
// 可以解决跨域问题
```

### callback参数

### config参数

## vue-resource配置

设置根地址

```js
Vue.http.options.root = 根地址
// 根地址 为字符串
```

设置emulateJSON

```js
Vue.http.options.emulateJSON = true;
// 默认为false
```

