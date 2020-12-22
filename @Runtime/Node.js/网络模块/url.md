## url模块

### 创建url实例

```js
var url = require('url');
```

### url.parse()

说明: 解析url, 返回一个对象

语法: `url.parse(url[, parseQuery][, noProtocal])`

* parseQuery
  * ture: 将query解析为对象
  * false(默认): query解析为一个字符串
* noProtocal
  * true: 解析不带protocal的url
  * false(默认): 解析带protocal的url