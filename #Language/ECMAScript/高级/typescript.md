### 数据类型

number 包括整型和浮点

```js
let n:number = 123;
```

string 字符串

```js
let s:string = 'hello'
```

array 数组

```js
// 定义单一类型数组
let a:string[] = ['hello', 'world'];
// 或者
let a:Array<string> = ['hello', 'world'];

// 定义元组类型数组. 元组类型,长度要与定义相同, 类型也要与定义相同
let a:[string, number, boolean] = ['hello', 123, true];
```

enum 枚举类型

```typescript
enum Flag {
    success= 1,
    error= 2
}

let f:Flag = Flag.success;
console.log(f);
// f = 1

// 枚举类型不赋值会给一个默认值
enum Color {red, blue, yellow}
console.log(red, yellow, blue);
// 0 2 1

// 如果给其中一个赋值, 后面则会+1

enum Week{mon, sat=6, sun}
console.log(mon, wed, sun)
// 0 6 7
```

any 任意类型

```typescript
let v:any = 'hello';
console.log(v);
// 'hello'
v = 123;
console.log(v);
// 123
```

void 空类型

> 通常用于函数没有返回值

```typescript
function run():void {
	console.log('run');
}
```

never 其他类型

> 包括undefined和null, 用于接收抛出的异常

```typescript
let n:never;
n = ()=>{
    throw new Error('错误')
}
```

### 一个元素设置多个类型

```typescript
let a:numer|undefined|null;
```

### 函数

普通传参

```typescript
function hello(name:string, age:number):void{
    console.log(`hello${name}-${age}`);
}
```

参数可有可无

```typescript
function hello(name:string, age?:number):void{
    console.log(`hello${name}-${age||'保密'}`);
}
```

剩余参数

```typescript
function sum(...items:number[]):number{
    let count = 0;
    for (let i=0; i < items.length; i++){
        count += items[i];
    }
    return count;
}
```

### 类和继承

创建类

```typescript
class Person {
	name:string;
    
    constructor(name:string){
        this.name = name;
    }
    
    run():void{
        console.log(`${this.name}在run`);
    }
}
```

继承

```typescript
class Web extends Person{
    age: number;
    
    constructor(name:string, age:number){
        this.age = age;
        
        super(name); //初始化父类的属性
    }
    
    sayHi():void{
        console.log(`hello im ${this.name}, ${this.age} years old`)
    }
}
```

属性修饰符

* `public` 在类,子类,类外都可以访问(默认)

* `protected` 在类, 子类可以访问, 外部不可以访问

* `private` 在类中可以访问, 子类和外部都不可以访问

* 类内部即实例只能通过类定义的方法来访问

* 类外部即实例可以直接访问属性, 类外部示例

  ```typescript
  let a = new Web('哈哈', 20);
  console.log(a.name);
  // 哈哈
  console.log(a.age);
  //20
  ```

静态方法和属性

```typescript
class Silent {
    static name:string="静静";
    
    static saySome(){
        console.log("i don't want to say");
    }
}

Silent.saySome();
// "i don't want to say"
console.log(Silent.name);
// "静静"
```

