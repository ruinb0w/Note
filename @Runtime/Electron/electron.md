初始化项目

```js
const {app, BrowserWindow} = require("electron");
function createWindow (){
    mainWindow = new BrowserWindow({
        width: 800, //打开默认宽度
        height: 600,	//打开默认高度
        Webpreferences: {
            preload: path.join(__dirname, 'preload.js');
            nodeIntegration: true //开启node集成, 开启后可以访问系统接口例如process
        }
    })
}
```



### process对象

说明: 获取系统信息



### file对象

说明: 进行文件操作

> 文件默认是buffer可以通过toSting()转为字符串



### window对象

打开新的窗口

* 语法: `window.open(url, name);`
* url: '打开窗口的地址',
* name: 打开窗口的名字,
* 返回值: BrowserWindowProxy

关闭打开的窗口

* 语法: `BrowserWindowProxy.close()`

父子窗口传值

```js
// 子窗口调用该方法向父窗口传值
window.opener.postMessage(value);

// 父窗口通过监听message事件获取
window.addEventListener("message", (msg)=>{
    console.log("接受到的消息", msg)
})
```

* 说明: 子窗口向父窗口传值
* value: 传递的值

### BrowserWindow

```js
let mainWindow = BrowserWindow({
	width: 800, //宽度
    height: 600, //高度
    frame: true, //窗口边框
})
```

父子窗口

说明: 父窗口关闭子窗口也会跟着关闭

```js
const {BrowserWindow} = require('electron');
let top = new BrowserWindow();
let child = new BrowserWindow({
    parent: top // 指定父窗口
});
child.show();
top.show();
```

模态窗口

说明: 子窗口开启了模态, 则除非子窗口关闭否则不能操作父窗口

```js
const {BrowserWindow} = require('electron');
let top = new BrowserWindow();
let child = new BrowserWindow({
    parent: top,
    modal: true // 设置模态
});
child.show();
top.show();
```

### BrowserView

类似webview

### dialog

打开或保存文件, 警告等对话框

```js
const {dialog} = require('electron');

```

### webview组件

需要在主进程中启用webview

```js
function createWindow (){
    mainWindow = new BrowserWindow({
        width: 800, 
        height: 600,	
        Webpreferences: {
            preload: path.join(__dirname, 'preload.js');
            nodeIntegration: true,
            webviewTag: true //启用webview
        }
    })
}
```

### electron常用生命周期

```js
const {app} = require("electron");
app.on("ready", callback);
app.on("window-all-close", callback);
app.on("before-quit", callback);
app.on("will-quit", callback);
app.on("quit", callback);
```

### 快捷键

```js
const {globalShortcut} = require("electron");
app.on
```

### 主进程与渲染进程通信

ipcMain

ipcRender

### 应用菜单

menu

### 网络api

net

## other

优雅的显示

避免页面加载闪烁

```js
const { BrowserWindow } = require('electron')
let win = new BrowserWindow({ show: false })
win.once('ready-to-show', () => {
  win.show()
})
```



