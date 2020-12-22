### 使用

初始化项目

```
git init
```

设置签名

```
// 当前仓库设置
git config username
git config username
// 全局设置
git config --global	
```

显示项目信息

```
git status
```

添加跟踪

```
git add .
```

提交跟踪

```
git commit -m "update"
```

tags

```
git tag tag名
git checkout tag名
```

git reflog

git log --oneline

git reset --hard [HASH|HEAD\[^|~]]



## 版本管理

### 前进后退

### 分支管理

#### 查看分支列表

* 查看本地分支 `git branch -v `

* 查看本地和远程分支 `git branch -a`

#### 创建分支

* 语法: `git branch 分支名 `

#### 切换分支

* 语法: `git checkout 分支名`

#### 合并分支

> 合并分支时需要切换到接受修改(合并)的分支上

* 语法 `git merge`

#### 删除分支

* 删除本地分支: `git branch -d 分支`
* 删除远程分支: 	`git push 远程库别名 --delete 远程库分支`

**处理合并冲突**

### 远程库管理

#### 设置远程库别名

语法: `git remote add 远程库别名 仓库地址`

#### 查看远程库别名

语法: `git remote -v`

#### 切换远程库分支

语法: `git checkout -b 本地库别名 远程库别名(通常为origin)/远程分支名`

#### 获取/合并库远程库分支

可以使用 `fetch` 命令或者 `pull` 命令, `pull` 命令 = `fetch` + `merge`

* 语法: `git fetch 远程库别名 远程分支名 `
* `git merge 远程库别名/远程分支名`

`git pull 远程库别名 远程分支名`

## 其他

### ssh登录

## 配置文件

`.gitignore` 

说明: 忽略文件

示例:

```js
node_module
// 忽略 node_module
```

`READEME.md`

说明: 项目说明文件

