# react

react 基本使用

1. 创建挂载点
2. 创建虚拟DOM
3. 渲染虚拟DOM到挂载点

```react
<div id="container"></div>

<script type="text/babel">
    const msg = "hello jsx";
    
	const VDOM = (
    	<div className="container">
        	<h1 style={{color:'red'}}>{msg}</h1>
    	</div>)	
    
	ReactDom.render(VDOM, document.getElementById("container"));
</script>
```

操作DOM会导致页面重绘，那虚拟DOM就不会吗？
jsx可以方便的写元素
react 虚拟dom比原生dom轻

## jsx

1. 定义虚拟DOM时不用引号
2. js表达式用{}包裹
3. 类名用`className` 而不是`class`
4. 内联样式用 `style={{key:value}}`的形式
5. VDOM只能有一个根标签
6. 标签首字母大写表示该元素是一个组件.

## 组件

### 函数式组件

```react
<div id="container"></div>

<script type="text/babel">
    function MyCompoent(){
        const msg = 'hello compoent';
        return <h1>{msg}</h1>
    }
    ReactDOM.render(<MyComponent/>, document.getElementById("container"));
</script>
```

### 类式组件

## other
可以通过debuger来进行断点调试

表达式:  一个表达式会产生一个值