# basic

## 类型

| 类型    | 例子                                            | 描述                        |
| ------- | ----------------------------------------------- | --------------------------- |
| number  | 1 2 3                                           | 对应基础类型number          |
| string  | "hello" "world"                                 | 对应基础类型string          |
| boolean | true false                                      | 对应基础类型boolean         |
| 字面量  | 1 "hello" true                                  | 值只能是声明的字面量        |
| any     | *                                               | 任意类型                    |
| unknown | *                                               | 类型安全的any               |
| void    | undefined                                       | undefined                   |
| never   | 没有值                                          | 不能有值, 用于函数抛出错误. |
| object  | `let obj:object`                                | 对象                        |
| Array   | `let arr:Array<number>` 或者 `let arr:string[]` | 数组                        |
| tuple   | [1,2,3]                                         | 固定长度数组(ts新增)        |
| enum    | {A,B}                                           | 枚举类型(ts新增)            |

#### 对象声明

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
    [xxx: number]: string // 你也可以不叫prop_name 叫 xxx也可以
}
```

#### 函数声明

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



#### 联合类型声明

```typescript
let v: string | number;
v = "hello";
v = 123;
v = false; //报错
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

### 赋值

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

### 基础静态类型

number, string, boolean, undefined, null

### 复杂类型

#### 自定义对象

```typescript
let myobj: {
    name: string,
    age: number
};
myobj = {name: 'xiaobai', age: 10};
```

#### 数组

```typescript
let myarr: string[] = ['a', 'b']
```

#### 类

```typescript
class Students{}
const student: Students = new Students();
```

#### 函数

```typescript
const normalFunction(): string{
    return '返回string'
}
// 对于错误和无限循环的函数使用never
```

#### 箭头函数

```typescript
const arrowFunction: ()=>string = ()=>{
    return '返回string'
};
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

### 类型别名

```typescript
type Student = {
    name: string,
    age: number
}
let student : Student = {
    name: 'xiaobai',
    age: 10
}
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

### interface

说明: 用于在开发中做代码校验

#### 创建接口

```typescript
interface Person{
    name : string;
    age : number;
    work ?: string; // ?表示可有可无
    [propname: string]:any; //propname可以自定义属性名,且是可有可无的,string表示propname是sting,any表示属性值为任意
   	say(): string; // 返回值为string的方法say
}
```

#### 接口继承

```typescript
interface Student extends Person{
    id: number;
}

class Students implements Person{
    school_name: string;
}
```

### 枚举类型

用于定义状态

```js
enum Status {
    show = 1,
    hide,
}
```

### 泛型

#### 函数泛型

后期指定函数参数的类型

```js
// 单泛型
function join<T>(a: T, b: T){
  console.log(`${a}${b}`);
}
join<string>('hello', 'world'); // helloworld
join<number>(1,2); // 12
join<string>('hello', 1); //报错
join<number>('hello', 1); //报错
// 多泛型
function join1<T,P>(a:T, b: P){
    console.log(`${a}${b}`);
}
join1<string,number>('hello', 1); // hello1
join1<number,string>(1, 'hello'); // 1hello
```

#### 类泛型

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

### question

type 和 interface有什么区别

