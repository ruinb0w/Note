# basic

## 类型

| 类型    | 例子                                            | 描述                        |
| ------- | ----------------------------------------------- | --------------------------- |
| number  | `let n:number`                                  | 对应基础类型number          |
| string  | `let s:string`                                  | 对应基础类型string          |
| boolean | `let b:boolean`                                 | 对应基础类型boolean         |
| 字面量  | `const v:"hello"`                               | 值只能是声明的字面量        |
| any     | `let a:any`                                     | 任意类型                    |
| unknown | `let u:unkown`                                  | 类型安全的any               |
| void    | `let v:void`                                    | undefined                   |
| never   | `let n:never`                                   | 不能有值, 用于函数抛出错误. |
| object  | `let obj:object`                                | 对象                        |
| Array   | `let arr:Array<number>` 或者 `let arr:string[]` | 数组                        |
| tuple   | `let tu: [1,2,3]`                               | 固定长度数组(ts新增)        |
| enum    | `ENUM Gender {Male = 0, Female = 1}`            | 枚举类型(ts新增)            |

## 声明

### 对象声明

通常我们不使用 `let obj:object` 的方式声明对象, 而是使用下面的形式

```typescript
let obj:{
    name:string, // 一定要有
    age?:number // 可有可无
}
```

对于可能任意添加属性的情况, 可以用下面的方式解决(参数名类型只能是string或number)

```typescript
let obj:{
    name: string,
    [prop_name: string]: string, // [prop_name:string]表示属性名是一个字符串, :string表示属性值为字符串
    [xxx: number]: string // 你也可以不叫prop_name
}
```

### 函数声明

对于没有返回值的函数我们可以指定返回值为void

```typescript
function printName(name:string):void{
    console.log(name);
}
```

对于有返回值的函数, 我们需要根据返回值来进行声明

```typescript
function printName(n1:number, n2:number):number{
    return n1+n2;
}
```

#### 箭头函数

```typescript
const arrowFunction: ()=>string = ()=>{
    return '返回string'
};
```

### 枚举声明

方便字符串到数字的映射

```ts
enum Gender{
    male= 1,
    female= 2
}

let p:{name: string, gender:Gender};
p = {
    name: 'xiaobai',
    gender: Gender.male
}
```

### 联合类型声明

联合或

```typescript
let v: string | number;
v = "hello";
v = 123;
v = false; //报错
```

联合与

```ts
let v:{name:string}&{age:number};
v = {
    name: 'xiaobai',
    age: 10
}
```

联合类型不止可以指定类型, 同时可以限制取值

```typescript
let s: "hello" | "world";
s = "hello";
s = "world";
s = "haha"; //报错

let n:1|2;
n = 1;
n = 2;
n = 3; //报错
```

### 定义类型

定义对象的类型, 关键字 `type`

```ts
type oneToFive = 1|2|3|4|5;
let n:oneToFive = 1;
let n:oneToFive = 6; // 报错
```

### 定义接口

定义类的结构, 也可以用于定义对象的类型, 关键字 `interface`

> 接口时可以重复声明的, 其定义的类结构等于两个接口的集合.
>
> 接口中的属性或方法都不能有实际的值或实现.

```typescript
interface MyInterface{
    name: string;
    
    sayHello():void; // 只能定义抽象方法
}

class MyClass implements myInterface{
    name: string; // 通过接口定义的属性必须实现
    
    constructor(name:string){
        this.name = name;
    }
    
    sayHello(){ // 通过接口定义的方法必须实现
        console.log(`I'm ${name}`)
    }
}
```

### 泛型

函数泛型: 用于后期指定函数参数以及返回值的类型

```js
// 单泛型
function join<T>(a: T, b: T): T{
  return a+b;
}
// 多泛型
function join1<T,P>(a:T, b: P): void{
    console.log(a, b);
}

// 不带类型调用(ts会自己推断)
console.log(join(1,2));
// 带类型调用
join1<string, number>("age", 1);
```

类泛型: 用于后期指定实例的类型

```js
class Person<T> {
  name: T;
	constructor(name){
    this.name = name;
  }
	sayHi(){
    console.log(this.name)
  }
}

let person = new Person('xiaobai');
person.sayHi();
```

通过interface约束泛型

```typescript
interface Person {
    name: string;
}

function sayHi<T extends Person>(p: T):void{
    console.log("I'm", p.name);
}

sayHi({name:'xiaohei'});
```



## 赋值

any类型的值可以赋值给任意类型的值且不会报错, 请用unknown代替any. 示例

```typescript
let a:any;
let u:unknown;
let s:string;
a = false;
s = a; // 这里并不会报错
u = false;
s = u; // 这里会报错
```

如果想让unkown类型的值赋给其它变量需要使用类型判断. 示例

```typescript
let u:unkown;
let s:string;
u = false;
if(typeof u == 'string'){
   s = u;
}
```

#### 类型断言

告诉编译器, 这个变量的值是什么类型, 而不让编译器自己判断.

类型断言有两种形式, 例如:

```typescript
let s:string;
let n:number;

s = n; //报错
s = n as string; // 方式一
s = <string>n; // 方式二
```

## 静态数据类型

静态数据类型, 即变量定义类型后不可更改

### 复杂类型

#### 自定义对象

```typescript
let myobj: {
    name: string,
    age: number
};
myobj = {name: 'xiaobai', age: 10};
```

#### 函数

```typescript
const normalFunction(): string{
    return '返回string'
}
// 对于错误和无限循环的函数使用never
```

### 类型注解&类型推断

ts可以**推断**出变量的类型

但无法认出函数形参的类型, 这时需要使用类型**注解**

示例: 

```typescript
let a = 10;
// a = 'haha'; 这里会报错, 因为在let a = 10时推断出a是number类型
let b = 20;
function sum(a: number, b:number){
    return a + b; // 这里同样会推断出函数的返回值是number
}

let c = sum(a, b);
// c = 40; 这里会报错, 由于函数的返回值是number所以推断出c是number
```

### 类型混合使用

```typescript
let a : (number|string) = 1;
a = 'haha';
```

### 元组

```typescript
// 数组无法控制某个位置的数据类型
let a1 : (string | number) = ['a', 'b', 10];
a1 = [10,'a', 'b']; 

// 元组可以控制某个位置的数据类型
let a2 : [string, string, number] = ['a', 'b', 10];
a2 = [10,'a', 'b']; //这里会报错
```

### 枚举类型

用于定义状态

```js
enum Status {
    show = 1,
    hide,
}
```

### 命名空间

```js
namespace num{
  let a = 10;
  export let b = 20;
  export function print(){
    console.log(a,b);
  }
}

num.print(); // 10 20
console.log(num.b); // 20
```

## Class

### 类的基本结构

```ts
class 类名 {
    属性名: 类型;
    
    constructor(参数:类型, ...){
        this.属性名 = 参数;
    }
    
    方法名(){
        ...
    }
}
```

#### constructor

用于执行创建类时的初始化工作

#### static

将属性(方法)设置为静态属性(方法), 静态属性(方法)直接通过类名访问.

```typescript
class Person {
    static age:number = 10;
}

console.elog(Person.age); // 10
```

#### readonly

```typescript
class Person {
    readonly age:number = 10;
    static readonly name:string = 'xiaobai'; //static要在readonly前
}

const p = new Person();
console.log(p.age); // 10
p.age = 20; // 报错
console.log(Person.name); // xiaobai
Person.name = 'xiaohei'l //报错
```

### 继承

```typescript
class Father{
    name: string;
    
    constructor(name:string){
        this.name = name;
    }
    
    sayHi(){
        console.log(`I'm ${name}`);
    }
}

class Son extends Father{
    age: number;
    
    constructor(name:string, age:number){
        this.age = age;
        super(name); // 在继承的过程中, 必须在子类的constructor中通过super调用父类的constructor, 来让父类的属性初始化
    }
    
    sonSayHi(){
        super.sayHi(); // super还可以用来调用父类的方法
    }
}

const son = new Son('xiaohei', 10);
```

#### super

* 可用于子类的constructor中初始化父类的属性
* 可在子类中调用父类的方法

### 抽象类

如果一个类用于作为其他类的基类, 而不该用于创建实例, 那么就将该类声明为一个抽象类.

```typescript
abstract class Animal{
	name: string;
    
    constructor(name:string){
        this.name = name;
    }
    
    abstract sayHi():void; // 抽象方法
}
```

#### abstract

* 用于将一个类声明为抽象类
* 用于将抽象类中的方法定义为抽象方法, 子类继承时必须实现抽象方法.

### 属性封装

```typescript
class Animal{
    public name: string;
    private _age: number;
    
    constructor(name: string, age: number, public hobby: string){
        // hobby 加了属性修饰符后就可以在构造函数中直接声明, 且无需显式的对hobby进行赋值.
        this.name = name;
        this._age = age;
    }
    
    get age(){
        return this._age;
    }
    
    set age(val:number){
        if(val < 0){
            console.log("age should great than 0");
            return;
        }
        this._age = val;
    }
}
```

#### public, private, proteced

public 标记属性为共有属性, 可以在类内, 类外访问

private 标记属性为私有属性, 只能在类内使用

protected 标记属性为保护属性, 可以在类内或子类内访问

> 加上属性修饰符后可以直接在constructor中定义属性, 且无需显示的对属性赋值

#### getter, setter

让对象封装属性像普通属性一样使用, 但实际上是调用了封装属性的方法