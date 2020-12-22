## path模块

path在nodejs中独立为一个模块, 可以通过`require("path")`引入

### 常用方法

| 方法                     | 说明                           | 返回值 |
| ------------------------ | ------------------------------ | ------ |
| path.normalize(path)     |                                |        |
| path.join(path[, path]*) | 将传入的多个路径拼接为标准路径 | String |
| path.extname(path)       | 获取文件扩展名                 | String |

`__dirname` 当前文件所在绝对路径