## 模块

### nrm

源管理模块

### nvm

版本管理模块

> 如果你修改过module的全局安装位置, nvm会提示你不兼容, 只要照做修改就好, 它会根据版本来放你的全局module, 以免版引发兼容问题.当然依据提示修改好后, 你最好把你自定义的全局位置的文件夹给删了.

## 其它

### electron加速

> 需先通过 `nrm use taobao` 将源改为淘宝

```bash
export ELECTRON_MIRROR="https://npm.taobao.org/mirrors/electron/"
export ELECTRON_CUSTOM_DIR="8.1.1" # 你要安装的electron版本
```

