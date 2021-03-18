## https模块

### 创建https服务

https与http的区别在于`https`模块需要额外处理SSL证书

```js
var https = require('https');

var certification = {
        key: fs.readFileSync('./ssl/default.key'),
        cert: fs.readFileSync('./ssl/default.cer')
    };

var server = https.createServer(certification, function (request, response){});

// 添加多组证书
server.addContext('foo.com', {
    key: fs.readFileSync('./ssl/foo.com.key'),
    cert: fs.readFileSync('./ssl/foo.com.cer')
});
```

### 访问https服务

```js
var request = https.request(options, function (response) {});
```

