## bcrypt

加密工具

### 加密密码

```js
const bcrypt = require("bcrypt");
async function run(){
    let salt = await bcrypt.getSalt(10); // 默认为10
	let pass = await bcrypt.hash('名密码', salt);
}
```

### 对比密码

```
let isEqual = await bcrypt.compare('明文密码','加密密码')
```

### express-session

会话模块

```js
const session = require('express-session');
app.use(session({secret:'secret key'}))
```

