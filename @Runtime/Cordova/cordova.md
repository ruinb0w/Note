## 开发环境搭建

开启浏览器调试

chrome://inspect

## cordova-cli

## 基础

### 项目结构

### 代码入口

```js
document.addEventListener("deviceready", (e)=>{
	// 所有的代码都要从这里开始
})
```



### 生命周期

`deviceready` 底层api加载完成

`pause` 应用在后台挂起

`resume`  应用程序从后台恢复

> pause和resume需要在deviceready的回调函数中使用

### plugin

> plugin需要在deviceready的回调函数中使用

插件安装

```
cordova plugin 插件名
```



