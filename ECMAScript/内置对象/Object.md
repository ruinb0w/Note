访问对象属性

1. 通过`obj.property`

2. 通过`obj[property]`

   在对象属性名**包含特殊字符**或属性名为一个**变量**时可以用到

### 检测对象是否拥有某一属性

1.  `in` 操作符

   会搜索原型链

   ```js
'name' in obj
   ```

2. `obj.hasOwnProperty(property)` 

   不会搜索原型链

# 类

### 工厂模式

ES原生没有类, 可以通过函数来模拟

```js
function person(name, age){
    let obj = new Object();
    obj.name=name;
    obj.age=age;
    obj.sayHi = function(){
    	console.log(`hello, I\'m ${this.name}`);
    }
    return obj;
}
let xiaoming = person("xiaoming", 10);
```

## 构造函数

ES提供了构造函数, 通过构造函数创建的对象可以使用`instanceof`关键字判定类型

```js
function Person(name, age){
    let obj = new Object();
    this.name=name;
    this.age=age;
}
Person.sayHi = function(){
    console.log(`hello, I\'m ${this.name}`);
}
let xiaoming = new Person("xiaoming", 10)
```

