### 使用async-await

**引入两个js**

[regeneratorRuntime.js](https://github.com/facebook/regenerator/blob/master/packages/regenerator-runtime/runtime.js)

promisify.js

```
module.exports = (api) => {
  return (options, ...params) => {
    return new Promise((resolve, reject) => {
      api(Object.assign({}, options, { success: resolve, fail: reject }), ...params);
    });
  }
}
```

**使用示例**

```js
//引入编译模块
const regeneratorRuntime =require("../libs/regeneratorRuntime.js")
const promisify = require('../libs/promisify.js');

//微信 API，转成返回 Promise 的接口 云开发API的有Promise 风格 不需要再转了
const getUserInfo= promisify(wx.getUserInfo);
const login = promisify(wx.login);
wx.cloud.init();

Page({
	data: {
	},
	onLoad: async function () {
		console.log(this)

		const user = await getUserInfo();
		console.log("onLoad user",user)

		const code = await login();
		console.log("onLoad code",code);
	},
	onShow: async function(){
		const user = await getUserInfo();
		console.log("onshow", user)
	}
})
```

## 后台获取(上报)位置

后台获取(上报)位置需要用到两个接口 

* [wx.startLocationUpdateBackground](https://developers.weixin.qq.com/miniprogram/dev/api/location/wx.startLocationUpdateBackground.html) 开始在后台监听位置
* [wx.onLocationChange](https://developers.weixin.qq.com/miniprogram/dev/api/location/wx.onLocationChange.html) 开始监听位置变化(如果只监听位置, 不监听变化则无效)

然后需要对`app.json`进行配置

```json
"permission": {
	"scope.userLocationBackground": {
		"desc": "后台获取用户位置"
	}
},
"requiredBackgroundModes": ["location"]
```

最后需要让用户设置授权

```html
<button open-type="openSetting">用户授权小程序在后台获取位置</button>
```

> 需要注意的是`wx.startLocationUpdateBackground` 只能启动一次, 所以必须在授权之后再启动