## router

```js
const getRouter = require('router');
const router = getRouter();
router.get('/add', (req, res)=>{
    
})
server.on('request', (req,res)=>{
    router(req,res, ()=>{});
})
```

