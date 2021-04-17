## tsc

`tsc [选项] [文件名]` 

* 选项
  * `-w` 监听文件改变, 并自动编译
* 文件名
  * 如果不写文件名会自动从当前位置开始进行递归监听(需要先创建 `tsconfig.json` 文件)

## tsconfig.json

```json
{
	"include": [  //指定要编译的文件路径
        "./src/**/*" // ** 表示任意目录, * 表示任意文件
    ],
    "exclude": [], //剔除不编译的文件
    "extends": "", //继承其他配置文件
    "files": [], //单个指定要编译的文件
    "compilerOptions": {
        "target": "ES5", //指定编译目标, 可以是ES5,ES6, ESNext等
        "module": "ES6", //指定模块化方案, 可以是ES6, commonjs等
        "lib": [], //使用到的库
        "outDir": "./dist", //输出文件路径
        "outFile": "./dist/app.js", //将代码合并为一个文件, 通常不配置而是通过打包工具打包
        "allowJS": true|false, //对js进行编译, 默认false
        "checkJS": true|false, //检查js语法规范, 默认false
        "removeComments": true|false, //移除注释, 默认false
        "noEmit": true|false, //不生成编译文件, 默认false
        "noEmitOnError": true|false, //当有错误时不生成编译后的文件, 默认false
        // 检查设置
        "strick": true|false, //设置所有检查都为true, 可以手动将某一项关掉. 默认false
        "strickNullChecks": true|false, //检查有可能为null的变量
        "noImplicitThis": true|false, //不允许隐式this, 默认false
        "noImplicitAny": true|false, //不允许隐式any, 默认false
        "alwaysStrict": true|false, //编译时使用严格模式, 默认false
        
    }
}
```

处理strickNullChecks

```js
const box = document.querySelector("#box");
box?.addEventListener("click", ()=>{
    console.log("clicked");
})
```

模块导入导出

```ts
// m.ts
const name = "xiaobai";

export {
	name
}
```

```ts
// app.ts
import {name} from "./m";
```

