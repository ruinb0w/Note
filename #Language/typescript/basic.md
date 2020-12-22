# basic

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
