## util模块

promisify将普通回调函数转化为异步函数

```js
const promisify = requrie("util").promisify;
const fs = require("fs");
const readFile = promisify(fs.readFile);
async function run(){
    let f1 = await readFild('./1.txt', 'utf8');
    let f2 = await readFild('./2.txt', 'utf8');
    let f3 = await readFild('./3.txt', 'utf8');
}
```
