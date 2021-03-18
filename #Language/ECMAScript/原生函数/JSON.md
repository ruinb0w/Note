### JSON.stringify()

> (1) 字符串、数字、布尔值和 null 的 JSON.stringify(..) 规则与 toString() 基本相同。
> (2) 如果传递给 JSON.stringify(..) 的对象中定义了 toJSON() 方法,那么该方法会在字符串化前调用,以便将对象转换为安全的 JSON 值。

* 语法: `JSON.stringify(值)`

* 语法: `JSON.stringify(对象, 替换)`

  * **替换**可以是**字符串数组**或者**函数**

  * 示例

    ```js
    let a = {
    	b: 42,
    	c: "42",
    	d: [1,2,3]
    };
    
    JSON.stringify( a, ["b","c"] );
    // "{"b":42,"c":"42"}"
    
    JSON.stringify( a, function(k,v){
    	if (k !== "c") return v;
    });
    // "{"b":42,"d":[1,2,3]}"
    ```

* 语法: `JSON.stringify(对象, 替换, 格式)`

  * 格式可以是数字或字符, 数字代表每一级缩进的空格数, 字符则会代替空格

  * 示例

    ```js
    var a = {
    b: 42,
    c: "42",
    d: [1,2,3]
    };
    
    JSON.stringify( a, null, 3 );
    // "{
    //    "b": 42,
    //    "c": "42",
    //    "d": [
    //       1,
    //       2,
    //       3
    //    ]
    // }"
    
    JSON.stringify( a, null, "--" );
    // "{
    // --"b": 42,
    // --"c": "42",
    // --"d": [
    // ----1,
    // ----2,
    // ----3
    // --]
    // }"
    ```

`JSON.parse(jsonObj)`



