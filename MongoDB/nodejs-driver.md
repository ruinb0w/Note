## 基础用法

```js
const {MongoClient} = require("mongodb");
const url = "mongodb://admin:zero1024@192.168.56.101:27017";
const dbName = "itying";
const client = new MongoClient(url, { useUnifiedTopology: true} );

client.connect( async (err) => {
  if (err) {
    console.log('err', err);
  }
  console.log('connect success');
  let db = client.db(dbName);
  let result; 
  // result = await insertOne(db, "user", {name: "xiaolong", age: 1});
  // console.log(result);
  // result = await find(db, "user", {});
  // console.log(result);
  // result = await updateOne(db, "user", {name:"xiaolong"}, {$set: {age: 20}});
  // console.log(result);
  result = await deleteOne(db, "user", {name: "xiaobai", age: 30});
  console.log(result);
  result = await find(db, "user", {});
  console.log(result);
  client.close(); // 操作完后一定要关闭
})

async function find(db, collection, pattern){
  return new Promise( (resolve, reject) => {
    db.collection(collection).find(pattern).toArray( (err,data) => {
      if (err) {
        reject(err);
        return;
      }
      resolve(data);
    });
  })
}

async function updateOne(db, collection, filter, content){
  return new Promise( (resolve, reject) => {
    db.collection(collection).updateOne(filter, content, (err, result) => {
      if (err) {
        reject(err);
        return;
      }
      resolve(result);
    })
  })
}

async function insertOne(db, collection, content){
  return new Promise( (resolve, reject) => {
    db.collection(collection).insertOne(content, (err, result) => {
      if (err) {
        reject(err);
        return;
      }
      resolve(result);
    })
  })
}

async function deleteOne(db, collection, filter){
  return new Promise( (resolve, reject) => {
    db.collection(collection).deleteOne(filter, (err, result) => {
      if (err) {
        reject(err);
        return;
      }
      resolve(result);
    })
  })
}
```

