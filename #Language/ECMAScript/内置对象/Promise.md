Promise可以用来封装异步函数

`.then`

`.catch`

`.all` 所有异步都成功则执行resolve, 回调函数的参数是一个数组.

`.race` 只要有一个异步成功则执行resolve, 回调函数的参数是第一个成功异步方法的返回值.

`.final` 异步执行完后

Promise用于处理回调地域, 其有两个关键的`prototype`方法, `.then` 和 `.catch`

## promise对象

申明一个Promise对象, 并用函数包裹

```js
// 该函数用于读取文件
function getFileContent(filePath){
  return new Promise((resolve, reject)=>{
  	fs.readFile(path.join(__dirname, 'filePath'), (error, data)=>{
   	 if(error){
   	   reject(error);
  	  }else{
   	   resolve(data);
   	 }
 	 });
	});
}
```

> 需要知道的是在申明的时候会立即执行传入构造函数的方法
>
> 如果不想立即执行, 可以用函数包裹new Promise



### .then属性

通过.then传递异步函数的处理函数

```js
getFileContent('1.txt').then(
  // .then方法会将该函数作为Promise构造函数的回调函数的第一个实参
  (data)=>{
    console.log('data is:' + data);
    // 在一个promise完成后, 通过return来生成新的promise
    // 新的promise作为.then的返回值返回
    return getFileContent('2.txt')
  },
  // .then方法会将该函数作为Promise构造函数的回调函数的第二个实参
  (error)=>{
    console.log('oops:' + error.message)
  }
).then(
  ...
)
```

> .then方法会将第一个参数作为Promise构造函数的中的回调函数的第一个参数, 即会将



### .catch属性