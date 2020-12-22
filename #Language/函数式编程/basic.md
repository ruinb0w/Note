## 基本概念

### 函数式编程优点

更少的bug, 更易读, 更快的完成代码, 更好的重用

### 函数式编程应该具备的属性

函数是一等公民(该特性由语言决定): 一等公民是指函数和其它值是一样的, 例如一个函数可以作为另一个函数的参数, 一个函数可以将函数作为返回值, 一个函数可以被赋值给一个变量.

函数应当是纯的: 给一个函数同一个参数, 得到的结果应该是固定的, 不会出现意外的.

```typescript
let mature_line:numer = 18;
function isMature(age): bool{
    return age > mature_line;
}
// 上面的isMature会由于mature_line的变化而导致结果的变化.
function isMature(age){
    let mature_line: number = 18;
    return age > mature_line;
}
// 第二个isMature就不会因为外部的变化而导致明明相同的参数却得到不同的结果.
```

### 高阶函数



