### 检测对象是否拥有某一属性

1.  `in` 操作符

   会搜索原型链

   ```js
'name' in obj
   ```

2. `obj.hasOwnProperty(property)` 

   不会搜索原型链

## 静态方法

Object.getOwnPropertyDescriptor

Object.defineProperty

Object.preventExtensions(..)

Object.seal(..): 对对象执行preventExtensions后, 将属性设置为 `configurable:false`

Object.freeze(..) 对对象执行seal后, 将属性设置为 `writable: false`

Object.asign(target, [souce]*)

Object.create()

* 说明: 创建一个对象, 其[[prototype]]基于传入的对象
* 语法: `Object.create(proto, [propertiesObject])`

Object.setPrototypeOf()

* 说明: 修改一个对象的[[prototype]]
* 语法: `Object.setPrototypeOf(obj, prototype)`

Object.is()

* 说明: 判断两个值是否相等, 可用于NaN和-0
* 语法: `Object.is(值1, 值2)`

# 类(模拟)

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

