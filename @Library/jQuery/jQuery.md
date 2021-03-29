# 概念

## 隐式遍历

对一个包含多个DOM的jQuery对象进新udate操作会影响其包含的所有DOM

> 如果是read操作则只是第一个DOM

**示例**

```html
<input type="text" value="123">
<input type="text" value="456">
<script>
    $("input").val("789");
    // 上面的两个input的值都会变为789
</script>
```

## 链式操作

jquery的很多方法执行后返回的都是jquery对象, 所以可以很方便的进新链式操作

> read方法都不支持链式操作, update可以

**示例**

```js
<input type="text" value="456">
<script>
    $("input").val("789").css("color", "red").blur(function(){
    	alert($(this).val());
	});
</script>
```

