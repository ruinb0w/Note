# 终端命令行

### 导入数据库

mongoimport -d 数据库名 -c 集合名称 -file 要导入的数据文件

### 打开mongodb

`mongo [库名] [-u 用户名] [-p 密码]`

* 指定库名可以直接进到数据库
* 指定用户名和密码可以以某个用户的身份登录

# mongodb命令行

## 基本CRUD操作

### Create

| 语法                                        | 说明             |
| ------------------------------------------- | ---------------- |
| `use 数据库名`                              | 切换(创建)数据库 |
| `db.createCollection(集合名)`               | 创建集合         |
| `db.集合.insert({字段: 值})`                | 插入单个文档     |
| `db.集合.insertMany({字段: 值},{字段: 值})` | 插入多个文档     |

### Read

| 语法                                         | 说明                                           |
| -------------------------------------------- | ---------------------------------------------- |
| `show dbs`                                   | 显示已有的数据库                               |
| `db`                                         | 显示当前数据库                                 |
| `show collections`                           | 显示集合                                       |
| `db.集合.find()`                             | 查找集合条目                                   |
| `db.集合.find().count()`                     | 对查找到的条目计数c                            |
| `db.集合.find().skip(数值)`                  | 跳过条目数                                     |
| `db.集合.find().limit(数值)`                 | 限制查询条目,和skip结合可以实现分页查找        |
| `db.集合.find({查询条件}, {字段:1, 字段:0})` | 只显示规定字段, 值为1表示显示, 值为0表示不显示 |

### Update

| 语法                                                         | 说明                   |
| ------------------------------------------------------------ | ---------------------- |
| `db.表名.update({查询条件},{条目: 值})`                      | 覆盖更新文档           |
| `db.集合名.update({查询条件},{$set: {条目: 值}})`            | 更新某个条目           |
| `db.集合名.update({查询条件},{$set: {条目: 值}},{multi: true}` | 更新多个文档的相同条目 |
| `db.集合名字.update({查询条件},{$inc:{条目: 增长值}})`       | 列增长                 |

### Delete

| 语法                                          | 说明       |
| --------------------------------------------- | ---------- |
| `db.dropDatabase()`                           | 删除数据库 |
| `db.集合名.drop()`                            | 删除集合   |
| `db.集合.remove({查询条件})`                  | 删除文档   |
| `db.集合.remove({查询条件}, {justOne: true})` |            |

## 查询

### 统计查询

统计字段数

`db.集合.count()`

根据条件统计

`db.集合.count({查询条件})`

统计查询信息(如查询用时等)

`db.集合.find().explain("excutionStats")`

### 分页查询

限制获得的条目数

`db.集合.find().limit(3)`

跳过某些条目

`db.集合.find().skip(3).limit(3)`

> 这里就跳过了前三条获得第4-6条

### 查询排序

`db.集合.find().sort(1)`

> 1为升序, -1 为降序

### 正则查询

`db.集合.find({字段: /正则/})`

说明: 正则查询可以匹配到字段包含的条目

示例: 

```sql
/*有xiaobai, xiaohong, xiaolan*/
db.user.find({name: /xiao/}); /*得到 xiaobai, xiaohong, xiaolan*/
```

### 比较查询

`db.集合.find({字段: {$gt: 值}})` 大于

`db.集合.find({字段: {$lt: 值}})` 小于

`db.集合.find({字段: {$eq: 值}})` 等于

`db.集合.find({字段: {$gte: 值}})` 大于等于

`db.集合.find({字段: {$lte: 值}})` 小于等于

`db.集合.find({字段: {$ne: 值}})` 不等于

`db.集合.find({字段: {$gt: 值1, $lt: 值2}})` 组合

### 匹配查询

`db.集合.find({字段: {$in:[字段值, 字段值]}})` 匹配出与字段值相同的条目

`db.集合.find({字段: {$nin:[字段值, 字段值]}) ` 匹配出与字段值不相同的条目

说明: 匹配查询是完全匹配, 不是包含

示例: 

```sql
/*有xiaobai, xiaohong, xiaolan*/
db.user.find(name: {$in: ["xiao", "xiaobai"]}) /*得到 xiaobai*/
```

### 条件连接查询

`db.集合.find({$and:[{字段: 值}, {字段: 值}]})` 查询到两个条件都满足

`db.集合.find($or:[{字段: 值}, {字段: 值}])` 满足一个字段即可

`db.集合.find({字段:值, 字段:值})` 也可以起到$and的效果

### 指定查询结果

`db.集合.find({},{字段: 1})` 只会返回指定字段

说明: 第一个{}是查询条件, 没有条件也要占位

## 索引

设置索引后可以极大的增加查询效率, 但会降低插入效率

### 查看索引

`db.集合.getIndexes()` 用于查看集合中的索引

`db.集合.find().explain()` 用于查看索引是否生效

### 创建索引

`db.集合.createIndex({keys}, {options})`

* keys

  * `字段: 1|-1` 1表示升序, -1表示降序

* options

  * `unique: Boolean` 字段的值是否唯一, 当前有重复的值则设置失败, 设置后不能插入字段值重复的条目
  * `name: 索引名` 手动设置索引名

* 示例

  ```js
  // 展示以age字段升序建立索引
  db.collection1.createIndex({age:1})
  // 复合索引
  db.collection1.createIndex({age:1, name: 1})
  // 复合索引必须要包含第一个字段才生效
  db.collection1.find({age: 20, name: "小白"}) //生效
  db.collection1.find({age: 20})  //生效
  db.collection1.find({name: "小白"}) //不生效
  ```

### 删除索引

`db.集合.dropIndex(index)`

* index 可以是索引名称, 也可以条件删除

* 示例

  ````js
  // 名称删除
  db.colloction1.dropIndex("age_1_")
  // 条件删除
  db.collection1.dropIndex({age:1})
  // 删除所有索引, 默认的_id不会被删除
  db.collection1.dropIndexes()
  ````

## 用户管理

### 用户相关命令

> 执行命令都需要先切到某个数据库

`show users ` 显示数据库下的用户

`db.dropUser("用户名") ` 删除用户

`db.updateUser("用户名", {pwd: 密码, 等要修改的内容...})` 更新用户

`db.auth("用户名", "密码")` 用户登录

```js
// 1.切换到admin库, 不同的用户对应不同的库
use admin

// 2.创建账户
db.createUser({
    user: '用户名',
    pwd: '密码',
    roles: [{
        role: 'root', //root必须在admin库下
        db: 'admin'
    }]
})

// 3.通过配置文件(/etc/mongod.conf), 启用账户管理
security:
    authorization: enabled
```

> role
>
> * root
> * dbOwner

## 聚合管道

### 使用示例

```js
db.集合.aggregate([
	{$match: {age: '20'}}, //匹配到age为20的条目
    {$group: {_id: "$id", total: {$sum: "$amount"}}} //根据id来分组, 分组合并后的total为原先amount字段的和
])
```

#### 常用管道操作符

$match

* 说明: 条件匹配

* 语法: `$match: {字段: {匹配规则}}`

$group 

* 说明: 分组 ,统计结果
* 语法: `$group: {分组条件, 组合名: 组合的条目}`
  * 分组条件: _id(默认写法):$字段名

$project

* 说明: 增加, 删除, 重命名字段

* 语法: `$project: {字段: 1, ...}`
* 1 表示增序
* -1 表示减序

$limit

* 说明: 限制结果的数量

$skip

* 说明: 跳过文档的数量
* 语法: `$skip: 数量`

$sort

* 说明: 条件排序
* 语法: `$sort: {字段名: 1|-1}`

$lookup

* 说明: 用于引入其它集合

* 示例

  ```js
  db.order.aggregate([
  	{
  		$lookup: {
  			from: '要关联的集合',
  			localFiled: '当前集合关联的字段',
  			foreignFild: '关联集合关联的字段',
  			as: 'items' //把关联的数据放在当前集合条目的哪个字段
  		}
  	}
  ])
  ```

#### 常用管道表达式

$sum 求和

$max

$min

## 其他

### 错误处理

由于批量操作容易出错, 并且出错后并不会回滚数据, 所以需要知道哪里出错

```js
try{
    // 批量操作
}catch(err){
    print(err);
}
```

### mongodb 默认创建的数据库

admin:

local:

config: 

### 指令执行时间

指令.explain("executionStats")