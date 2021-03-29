### keys / allKeys/values

| 方法             | 说明                                          | 返回值 |
| ---------------- | --------------------------------------------- | ------ |
| `_.keys(obj)`    | 获取对象的所有key, 但不包含从原型链继承下来的 | Array  |
| `_.allKeys(obj)` | 获取对象的所有key, 包含从原型链继承下来的     | Array  |
| `_.values(obj)`  | 获取对象的所有值,不包含从原型链继承下来的     | Array  |

### invert

说明: 把object的每个key-value来个交换

语法: `_.invert(obj)`

### extend / extendOwn

| 方法                      | 说明                                            | 返回值 |
| ------------------------- | ----------------------------------------------- | ------ |
| `_.extend(obj[,obj]+) `   | 将多个对象组合, 如果key相同, 后面的会覆盖前面的 | obj    |
| `_.extendOwn(obj[,obj]+)` | 和extend类似, 但不会查看原型链                  | obj    |

### clone

说明: 复制一个object对象, 但两个对象相同的key所引用的value其实是同一对象

语法: `_.clone(source)`

### isEqual

说明: 对两个object进行比较，如果内容完全相同，则返回`true`. isEqual对Array也可以用

语法: `_.isEqual(obj1, obj2)`