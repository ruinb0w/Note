# screen

### screen.width

屏幕宽度，以像素为单位；

### screen.height

屏幕高度，以像素为单位；

### screen.colorDepth

返回颜色位数，如8、16、24。

# navigator

 表示浏览器的信息

### navigator.appName

浏览器名称；

### navigator.appVersion

浏览器版本

### navigator.language

浏览器设置的语言；

### navigator.platform

操作系统类型；

### navigator.userAgent

浏览器设定的`User-Agent`字符串。

# location

## 属性

### location.href

```js
// http://www.example.com:8080/path/index.html?a=1&b=2#TOP
location.protocol; // 'http'
location.host; // 'www.example.com:8080'
location.hostname; // 'www.example.com'
location.port; // '8080'
location.pathname; // '/path/index.html'
location.search; // '?a=1&b=2'
location.hash; // '#TOP'
```

> href属性也可用于页面跳转

## 方法

### location.assign() 

跳转到某个地址

### location.reload() 

刷新当前页面

### location.replace() 

跳转到某个地址,不会保留历史记录

# history

### history.back()

### history.forward()

### history.go()

# 操作文件

File API提供了`Files`和`FileReader`两个主要对象，可以获得文件信息并读取文件。

### files

`files`是`upLoadedFile.files`的一个属性, 是一个数组, 通过`upLoadedFile.files[0]`即可获取到第一个上传的文件

### FileReader()

`FileReader` 是一个新的对象, 可以用于读取文件

```js
var reader = new FileReader()
reader.onload = function(e){
    // e.target.result 就是文件的路径
}
reader.readAsDataURL(file);
```

