---
title: MongoDB Cli
date: 2017-08-10 00:04:50
tags: MongoDB
---

## Mongodb operation

1. show all the dbs

  ```sql
  show dbs
  ```
2. show all the collections in db

  ```sql
  show collections
  ```
<!-- more -->
3. show all data in specific db

  ```sql
  db.DATABASE_NAME.find().pretty()
  ```

4. create a databse

  ```sql
  use DATABASE_NAME
  ```

5. drop a database

  ```sql
  db.dropDatabase()
  ```

6. create collection

  ```sql
  db.createCollection(name, options)
  ```

7. drop collection

  ```sql
  db.COLLECTION_NAME.drop()
  ```

8. insert data

  ```sql
  db.COLLECTION_NAME.insert(document)
  db.collection.insertMany([documents])
  ```

  ```sql
  db.mycol.insert({
     _id: ObjectId(7df78ad8902c),
     title: 'MongoDB Overview',
     description: 'MongoDB is no sql database',
     by: 'tutorials point',
     url: 'http://www.tutorialspoint.com',
     tags: ['mongodb', 'database', 'NoSQL'],
     likes: 100
  })
  ```
9. query data

  ```sql
  db.mycol.find().pretty()

  db.mycol.find({"by":"tutorials point"}).pretty()
  db.mycol.find({"likes":{$lt:50}}).pretty()
  db.mycol.find({"likes":{$lte:50}}).pretty()
  db.mycol.find({"likes":{$gt:50}}).pretty()
  db.mycol.find({"likes":{$gte:50}}).pretty()
  db.mycol.find({"likes":{$ne:50}}).pretty()

  b.mycol.find(
     {
        $and: [
           {key1: value1}, {key2:value2}
        ]
     }
  ).pretty()

  db.mycol.find(
     {
        $or: [
           {key1: value1}, {key2:value2}
        ]
     }
  ).pretty()
  ```
10. update data

  ```sql
  db.COLLECTION_NAME.update(SELECTION_CRITERIA, UPDATED_DATA)

  db.mycol.update({'title':'MongoDB Overview'},{$set:{'title':'New MongoDB Tutorial'}})

  db.mycol.save(
     {
        "_id" : ObjectId(5983548781331adf45ec7), "title":"Tutorials Point New Topic",
           "by":"Tutorials Point"
     }
  )
  ```

11. delete document
  remove one

  ```sql
  db.COLLECTION_NAME.remove(DELETION_CRITERIA,1)
  ```
  remove all

  ```sql
  db.mycol.drop()
  ```
12. projection

  ```sql
  db.COLLECTION_NAME.find({},{KEY:1})
  ```

13. limit

  ```
  db.COLLECTION_NAME.find().limit(NUMBER)
  db.COLLECTION_NAME.find().limit(NUMBER).skip(NUMBER)
  ```

14. sort

  ```sql
  db.COLLECTION_NAME.find().sort({KEY:1})
  ```

15. index

  ```sql
  db.COLLECTION_NAME.ensureIndex({KEY:1})
  ```

  ```sql
  db.users.insertMany([
    {item: "lamp", qty: 50, type: "desk" },
    {item: "lamp", qty: 20, type: "floor" },
    {item: "bulk", qty: 100 }
  ])
  ```

  ```sql
  db.userLocal.insertMany([
      {username: "nilge", email: "gexiangy@usc.edu", password: "123456"},
      {username: "sophie", email: "huiwenzhe@usc.edu", password: "654321"}
  ])
  ```
