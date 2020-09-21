# MyNote_MongoDB

https://docs.mongodb.com/manual/mongo/ 

https://www.runoob.com/mongodb/mongodb-tutorial.html

啟動 mongo Shell

```js
mongo
```

顯示您正在使用的數據庫

```js
db
```

切換/創建數據庫，如果數據庫不存在，則創建數據庫，否則切換到指定數據庫。

```js
use <datebase>
```

刪除數據庫

```js
db.dropDatabase()
```

列出用戶可用的數據庫

```js
show dbs
```

列出集合(Collection)

```js
show collections
```

創建集合

```js
db.createCollection(<name>)
```

刪除集合

```js
db.<collection>.drop()
```

存取集合

```js
db.<collection>
```

插入 document

```js
db.<collection>.insert(<document>)
db.<collection>.insertMany(<document>)
```

查看 all document

```js
db.<collection>.find()
db.<collection>.find(<query>)
db.<collection>.find(<query>, <projection>)
// return <Cursor>
```

| 操作       | 格式         |
| :--------- | :----------- |
| 等於       | `{:`}        |
| 小於       | `{:{$lt:}}`  |
| 小於或等於 | `{:{$lte:}}` |
| 大於       | `{:{$gt:}}`  |
| 大於或等於 | `{:{$gte:}}` |
| 不等於     | `{:{$ne:}}`  |

\<project>

```
db.collection.find(query, {title: 1, by: 1}) // inclusion模式 指定返回的键，不返回其他键
db.collection.find(query, {title: 0, by: 0}) // exclusion模式 指定不返回的键,返回其他键
```

更新 document

```js
db.<collection>.update(
   <query>,
   <update>,
   {
     upsert: <boolean>,
     multi: <boolean>,
     writeConcern: <document>
   }
)
```

修改並返回單個文檔。默認情況下，返回的文檔不包含對更新所做的修改。要返回對更新進行了修改的文檔，請使用`new`選項。

```js
db.collection.findAndModify({
    query: <document>,
    sort: <document>,
    remove: <boolean>,
    update: <document or aggregation pipeline>, // Changed in MongoDB 4.2
    new: <boolean>,
    fields: <document>,
    upsert: <boolean>,
    bypassDocumentValidation: <boolean>,
    writeConcern: <document>,
    collation: <document>,
    arrayFilters: [ <filterdocument1>, ... ]
});
```

替換已有文檔

```js
db.<collection>.save(
   <document>,
   {
     writeConcern: <document>
   }
)
```

刪除文檔

```js
db.<collection>.remove(
   <query>,
   <justOne>
)
// > MongoDB 2.6
db.collection.remove(
   <query>,
   {
     justOne: <boolean>,
     writeConcern: <document>
   }
)
```



