## serve-static

静态资源访问服务

```js
const serveStatic = require('serve-static');
const serve = serveStatic('public')
serve.on('request', (req, res)=>{
    serve(req, res, ()=>{});
})
serve.listen(3000);
```