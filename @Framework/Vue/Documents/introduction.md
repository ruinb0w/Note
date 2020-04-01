# Introduction(介绍)

## [What is Vue.js?](https://vuejs.org/v2/guide/#What-is-Vue-js)(什么是Vue.js)

Vue (pronounced /vjuː/, like **view**) is a **progressive framework** for building user interfaces. Unlike other monolithic frameworks, Vue is designed from the ground up to be incrementally adoptable. The core library is focused on the view layer only, and is easy to pick up and integrate with other libraries or existing projects. On the other hand, Vue is also perfectly capable of powering sophisticated Single-Page Applications when used in combination with [modern tooling](https://vuejs.org/v2/guide/single-file-components.html) and [supporting libraries](https://github.com/vuejs/awesome-vue#components--libraries).

> Vue是一个先进的框架用于构建用户界面. 不像其他大型框架, Vue被设计为可递增的. 核心库只专注于视图层, 但可以很容易的与其他库进行交互.另一方面, 当与现代工具和支持库组合起来, Vue也有很强的能力来驱动一个单页面应用

If you’d like to learn more about Vue before diving in, we [created a video](https://vuejs.org/v2/guide/#) walking through the core principles and a sample project.

> 如果你想要先了解更多有关Vue的内容, 我们创建了一个视频带你走进Vue的核心原则以及示例项目

If you are an experienced frontend developer and want to know how Vue compares to other libraries/frameworks, check out the [Comparison with Other Frameworks](https://vuejs.org/v2/guide/comparison.html).

> 如果你是一个有经验的前端开发者并且想比较一下Vue和其他库或者框架, 查和其他框架的对比.

[Watch a free video course on Vue Mastery](https://www.vuemastery.com/courses/intro-to-vue-js/vue-instance/)

>免费观看Vue视频课程

## [Getting Started](https://vuejs.org/v2/guide/#Getting-Started)(开始吧)

[Installation](https://vuejs.org/v2/guide/installation.html)(安装)

The official guide assumes intermediate level knowledge of HTML, CSS, and JavaScript. If you are totally new to frontend development, it might not be the best idea to jump right into a framework as your first step - grasp the basics then come back! Prior experience with other frameworks helps, but is not required.

> 官方引导假设你有中级的HTML,CSS和JavaScript知识. 如果你完完全全是个新人, 直接使用框架或许不是一件好事, 学好基础再来! 有其他框架的经验有助于学习,  但并非必要.

The easiest way to try out Vue.js is using the [JSFiddle Hello World example](https://jsfiddle.net/chrisvfritz/50wL7mdz/). Feel free to open it in another tab and follow along as we go through some basic examples. Or, you can [create an `index.html` file](https://gist.githubusercontent.com/chrisvfritz/7f8d7d63000b48493c336e48b3db3e52/raw/ed60c4e5d5c6fec48b0921edaed0cb60be30e87c/index.html) and include Vue with:

> 最简单的方法来尝试Vue.js, 使用JSFiddle Hello World示例. 打开链接跟着基础示例走. 或者你可以创建一个`index.html`文件然后把Vue加进去:

```
<!-- development version, includes helpful console warnings -->
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
```

or:

```
<!-- production version, optimized for size and speed -->
<script src="https://cdn.jsdelivr.net/npm/vue"></script>
```

The [Installation](https://vuejs.org/v2/guide/installation.html) page provides more options of installing Vue. Note: We **do not** recommend that beginners start with `vue-cli`, especially if you are not yet familiar with Node.js-based build tools.

> 安装页面提供更多安装Vue的选项. 注意: 我们不推荐初学者使用`vue-cli`,特别是不熟悉以Node.js为基础的构建工具.

If you prefer something more interactive, you can also check out [this tutorial series on Scrimba](https://scrimba.com/playlist/pXKqta), which gives you a mix of screencast and code playground that you can pause and play around with anytime.

> 如果你倾向于更有交互的方式来学习, 你也可以在Scrimba找到教程, 它提供了屏幕录像和代码区, 你可以随时暂停和播放

## [Declarative Rendering](https://vuejs.org/v2/guide/#Declarative-Rendering)(陈述渲染)

[Try this lesson on Scrimba](https://scrimba.com/p/pXKqta/cQ3QVcr)(在Scrimba尝试这个课程)

At the core of Vue.js is a system that enables us to declaratively render data to the DOM using straightforward template syntax:

>Vue.js的核心系统让我们陈述渲染数据到DOM中, 只需要使用简单的模板语法:

```vue
<div id="app">
  {{ message }}
</div>
var app = new Vue({
  el: '#app',
  data: {
    message: 'Hello Vue!'
  }
})
```

We have already created our very first Vue app! This looks pretty similar to rendering a string template, but Vue has done a lot of work under the hood. The data and the DOM are now linked, and everything is now **reactive**. How do we know? Open your browser’s JavaScript console (right now, on this page) and set `app.message` to a different value. You should see the rendered example above update accordingly.

> 这样我们就已经创建了我们的第一个Vue应用! 渲染一个字符串模板看上去很简单, 但Vue在背后做了很多工作. 现在数据和DOM建立了连接. 我们怎么知道建立了连接? 打开你的浏览器的Javascript终端(立刻, 在这个页面上)设置`app.message`的值为另一个值.你应该可以看到上面例子的渲染相应地更新了.

In addition to text interpolation, we can also bind element attributes like this:

> 除了插入文本, 我们也可以绑定元素的属性

```vue
<div id="app-2">
  <span v-bind:title="message">
    Hover your mouse over me for a few seconds
    to see my dynamically bound title!
  </span>
</div>
var app2 = new Vue({
  el: '#app-2',
  data: {
    message: 'You loaded this page on ' + new Date().toLocaleString()
  }
})
```

Hover your mouse over me for a few seconds to see my dynamically bound title!

> 把你的鼠标放在span上几秒可以看到动态绑定的title

Here we are encountering something new. The `v-bind`attribute you are seeing is called a **directive**. Directives are prefixed with `v-` to indicate that they are special attributes provided by Vue, and as you may have guessed, they apply special reactive behavior to the rendered DOM. Here, it is basically saying “keep this element’s `title`attribute up-to-date with the `message` property on the Vue instance.”

> 这里我们有一个新东西. `v-bind`属性被称作指令. 指令用`v-`作为前缀, 通过这个表示该属性由Vue提供, 或许你已经猜到了, 它们使用了特别的交互行为来渲染DOM. 这基本上就是说"保持这个元素的`title`属性和Vue实例的`message`保持更新"

If you open up your JavaScript console again and enter `app2.message = 'some new message'`, you’ll once again see that the bound HTML - in this case the `title` attribute - has been updated.

> 如果你再次打开你的JavaScript终端并输入`app2.message = 'some new message'`,你将会再次看到绑定的HTML--在这个例子中是`title`属性被更新

## [Conditionals and Loops](https://vuejs.org/v2/guide/#Conditionals-and-Loops)(条件和循环)

[Try this lesson on Scrimba](https://scrimba.com/p/pXKqta/cEQe4SJ)(在Scrimba学习这节课)

It’s easy to toggle the presence of an element, too:

> 切换显示的元素很简单

```vue
<div id="app-3">
  <span v-if="seen">Now you see me</span>
</div>
var app3 = new Vue({
  el: '#app-3',
  data: {
    seen: true
  }
})
```

Go ahead and enter `app3.seen = false` in the console. You should see the message disappear.

> 在console输入`app3.seen=false`,你会看到消息消失了

This example demonstrates that we can bind data to not only text and attributes, but also the **structure** of the DOM. Moreover, Vue also provides a powerful transition effect system that can automatically apply [transition effects](https://vuejs.org/v2/guide/transitions.html)when elements are inserted/updated/removed by Vue.

> 这个例子展示了我们不仅可以绑定数据到文本和属性, 还可以控制DOM结构. 除此之外, Vue也提供了一个强大的动画效果系统, 当通过Vue插入,更新或删除元素时可以自动显示动画效果.

There are quite a few other directives, each with its own special functionality. For example, the `v-for` directive can be used for displaying a list of items using the data from an Array:

> 这里还有几个其他的指令, 每一个都有独特的功能. 例如, `v-for`指令可以用数组中的数据来现实一个项目列表:

```vue
<div id="app-4">
  <ol>
    <li v-for="todo in todos">
      {{ todo.text }}
    </li>
  </ol>
</div>
var app4 = new Vue({
  el: '#app-4',
  data: {
    todos: [
      { text: 'Learn JavaScript' },
      { text: 'Learn Vue' },
      { text: 'Build something awesome' }
    ]
  }
})
```

In the console, enter `app4.todos.push({ text: 'New item' })`. You should see a new item appended to the list.

> 在终端中输入`app4.todos.push({text:'New item'})`你应该会看到一个项目添加到列表中

## [Handling User Input](https://vuejs.org/v2/guide/#Handling-User-Input)(处理用户输入)

[Try this lesson on Scrimba](https://scrimba.com/p/pXKqta/czPNaUr)

> 在Scrimba学习这一课

To let users interact with your app, we can use the `v-on`directive to attach event listeners that invoke methods on our Vue instances:

> 为了让用户和你的应用交互, 我们可以使用`v-on`指令来添加事件监听, 事件触发时会调用Vue实例中的方法:

```vue
<div id="app-5">
  <p>{{ message }}</p>
  <button v-on:click="reverseMessage">Reverse Message</button>
</div>
var app5 = new Vue({
  el: '#app-5',
  data: {
    message: 'Hello Vue.js!'
  },
  methods: {
    reverseMessage: function () {
      this.message = this.message.split('').reverse().join('')
    }
  }
})
```

Note that in this method we update the state of our app without touching the DOM - all DOM manipulations are handled by Vue, and the code you write is focused on the underlying logic.

> 注意我们更新应用状态并没有触碰到DOM--所有的DOM都是由Vue操作的, 并且你的代码也应当遵循这一逻辑.

Vue also provides the `v-model` directive that makes two-way binding between form input and app state a breeze:

> Vue还提供了`v-model`指令, 该指令双向绑定了form中的输入和应用状态.

```vue
<div id="app-6">
  <p>{{ message }}</p>
  <input v-model="message">
</div>
var app6 = new Vue({
  el: '#app-6',
  data: {
    message: 'Hello Vue!'
  }
})
```

## [Composing with Components](https://vuejs.org/v2/guide/#Composing-with-Components)(通过组件组成)

[Try this lesson on Scrimba](https://scrimba.com/p/pXKqta/cEQVkA3)

> 在Scrimba学习该课

The component system is another important concept in Vue, because it’s an abstraction that allows us to build large-scale applications composed of small, self-contained, and often reusable components. If we think about it, almost any type of application interface can be abstracted into a tree of components:

> 组件系统是另一个重要的Vue概念, 因为它是一个抽象的东西, 这让我们可以通过小的, 自包含和可重用的组件组成大的应用.几乎所有类型应用界面都可以被抽象为一个组件树.

![Component Tree](assets/components.png)

In Vue, a component is essentially a Vue instance with pre-defined options. Registering a component in Vue is straightforward:

> 在Vue中, 一个组件本质上就是一个预先定义好选项的Vue实例, 很容易就能在Vue里注册组件

```js
// Define a new component called todo-item
Vue.component('todo-item', {
  template: '<li>This is a todo</li>'
})
```

Now you can compose it in another component’s template:

> 现在你可以将其组织进另一个组件的模板

```html
<ol>
  <!-- Create an instance of the todo-item component -->
  <todo-item></todo-item>
</ol>
```

But this would render the same text for every todo, which is not super interesting. We should be able to pass data from the parent scope into child components. Let’s modify the component definition to make it accept a [prop](https://vuejs.org/v2/guide/components.html#Props):

>但是这会在所有的todo渲染相同的文本, 这就没意思了. 我们应该可以从父作用域传递数据给子组件. 让我们修改组件定义, 让它可以接收属性.

```js
Vue.component('todo-item', {
  // The todo-item component now accepts a
  // "prop", which is like a custom attribute.
  // This prop is called todo.
  props: ['todo'],
  template: '<li>{{ todo.text }}</li>'
})
```

Now we can pass the todo into each repeated component using `v-bind`:

> 现在我们可以用`v-bind`传递todo到每一个重复的组件

```vue
<div id="app-7">
  <ol>
    <!--
      Now we provide each todo-item with the todo object
      it's representing, so that its content can be dynamic.
      We also need to provide each component with a "key",
      which will be explained later.
    -->
    <todo-item
      v-for="item in groceryList"
      v-bind:todo="item"
      v-bind:key="item.id"
    ></todo-item>
  </ol>
</div>
Vue.component('todo-item', {
  props: ['todo'],
  template: '<li>{{ todo.text }}</li>'
})

var app7 = new Vue({
  el: '#app-7',
  data: {
    groceryList: [
      { id: 0, text: 'Vegetables' },
      { id: 1, text: 'Cheese' },
      { id: 2, text: 'Whatever else humans are supposed to eat' }
    ]
  }
})
```

This is a contrived example, but we have managed to separate our app into two smaller units, and the child is reasonably well-decoupled from the parent via the props interface. We can now further improve our `<todo-item>`component with more complex template and logic without affecting the parent app.

>这是一个人为的例子, 我们设法分离我们的应用为两个更小的单元, 并且子单元从父单元通过属性接口进行很好的解耦合

In a large application, it is necessary to divide the whole app into components to make development manageable. We will talk a lot more about components [later in the guide](https://vuejs.org/v2/guide/components.html), but here’s an (imaginary) example of what an app’s template might look like with components:

> 在一个大型应用中, 将整个应用分为组件来开发可维护的应用是有必要的. 我们将在后面讨论更多的组件有关内容, 但这里是一个(虚假的)例子, 应用模板或许和组件类似:

```vue
<div id="app">
  <app-nav></app-nav>
  <app-view>
    <app-sidebar></app-sidebar>
    <app-content></app-content>
  </app-view>
</div>
```

### [Relation to Custom Elements](https://vuejs.org/v2/guide/#Relation-to-Custom-Elements)(和自定义元素的关系)

You may have noticed that Vue components are very similar to **Custom Elements**, which are part of the [Web Components Spec](https://www.w3.org/wiki/WebComponents/). That’s because Vue’s component syntax is loosely modeled after the spec. For example, Vue components implement the [Slot API](https://github.com/w3c/webcomponents/blob/gh-pages/proposals/Slots-Proposal.md) and the `is` special attribute. However, there are a few key differences:

> 你或许注意到Vue组件非常像自定义元素, 自定义元素是网页组成的规范的一部分. 因为Vue组件的语法是遵循规范的. 例如Vue组件执行了Slot API以及`is`特殊属性. 然而, 这里还有一些重要区别.

1. The Web Components Spec has been finalized, but is not natively implemented in every browser. Safari 10.1+, Chrome 54+ and Firefox 63+ natively support web components. In comparison, Vue components don’t require any polyfills and work consistently in all supported browsers (IE9 and above). When needed, Vue components can also be wrapped inside a native custom element.
2. Vue components provide important features that are not available in plain custom elements, most notably cross-component data flow, custom event communication and build tool integrations.

Although Vue doesn’t use custom elements internally, it has [great interoperability](https://custom-elements-everywhere.com/#vue) when it comes to consuming or distributing as custom elements. Vue CLI also supports building Vue components that register themselves as native custom elements.

## [Ready for More?](https://vuejs.org/v2/guide/#Ready-for-More)(准备好学习更多了吗?)

We’ve briefly introduced the most basic features of Vue.js core - the rest of this guide will cover them and other advanced features with much finer details, so make sure to read through it all!

> 我们简要介绍了Vue.js最核心的内容 -- 剩下的引导将会包含他们以及其他高级特性, 所以请确保你看完了上面的内容.