## 包

说明: 一个包必须要有`package.json`来进行描述

作用: 将多个子模块放在一个目录下, 通过入口文件来使用.

引入包: require一个包的路径则会自动解析出入口文件

- 默认入口文件名是`index.js`, 可以使用`package.json`来指定入口文件, 示例:

```json
{
	"main": "入口文件路径"
}
```

## package.json

描述包的文件

### package.json常用属性

```json
{
	"name": "包名",  //不可省略
    "version": "版本", //不可省略
    "description": "描述信息",
    "main": "入口文件",
    "dependencies": {
    	"package": "version"    // 依赖的包
    },
    "devDependecies": {
    	"package": "version"  // 开发时用的包
    }
}
```

### package-lock.json

1. npm5新增用于加快安装第三方包
2. 锁定包的版本, 以免在下次下载时出现兼容问题

## node模块加载规则

不省略后缀和路径则直接根据路径来进行查找

省略后缀不省略路径的情况下

1. 先查找路径下同名文件
2. 查找同名文件夹, 并找到`index.js`文件
3. 同名文件夹下没有`index.js`则看`package.json`下`main`字段指定的文件

省略后缀和路径

1. 当作nodeAPI来查找
2. 不是nodeAPI则到node_modules中查找, 匹配规则同省略后缀不省略路径的情况相同