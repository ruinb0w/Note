### $.ajax()

语法

```js
$.ajax({
    url: '',
    data: {
        key: value
    },
    // 或者是一个字符串用&分隔
    // data: "key=value&key1=value1"
    type: 'POST|GET',
    success: function(data){
        // 请求成功的回调
    },
    error: function(err){
        // 请求失败的回调
    },
    async: true|false, // 默认就是true表示异步
    dataType: 'json'|'xml'|'html'|'script' // 如果是对应类型则执行success否则执行error, 并且成功后会自动进新类型转换
})
```

### $.get()

说明: ajax中get请求的简写

语法1: `$.get(url, data, callback, dataType)`

语法2: `$.get(url, data, callback, dataType).error(callback)`

### $.post()

说明: ajax中post请求的简写

语法1: `$.post(url, data, callback, dataType)`

语法2: `$.post(url, data, callback, dataType).error(callback)`

### jqObj.load()

说明: 将url的内容加载到jqObj中

语法: `jqObj.load(url, callback)`

- **url** string 除了可以指定url 还可以用css选择器格式来进行内容的筛选 `hello.html div`

### $.getScript()

说明: 获取js并执行, 可以用于按需加载js

语法: `$.getScript(url, callback)`

### $.ajaxSetup()

说明: 修改ajax全局配置

## data转换

### $.param()

说明: 将data属性的JSON格式转为字符串格式 `key1=val1&key2=val2`

### $('form').serialize()

说明: 将表单(form)的值组合为字符串格式 `key1=val1&key2=val2`

### $('form').serialize()

说明: 将表单的值组合为对象数组格式 `[{key1:val1}, {key2:val2}, {key3:val3}]`

## 事件

### $('document').ajaxStart()

### $('document').ajaxStop()

### $('document').ajaxSuccess()

### $('document').ajaxError()

### $('document').ajaxComplete()

### $('document').ajaxSend()