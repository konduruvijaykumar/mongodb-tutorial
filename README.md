# mongodb-tutorial
This repository consists of examples on working with mongodb

https://www.mongodb.com/

https://www.mongodb.com/what-is-mongodb

https://www.mongodb.com/download-center

https://docs.mongodb.com/manual/installation/

https://docs.mongodb.com/

https://docs.mongodb.com/manual/tutorial/getting-started/

https://docs.mongodb.com/manual/crud/

https://docs.mongodb.com/ecosystem/drivers/node/

https://docs.mongodb.com/ecosystem/drivers/java/

### Query Options
https://docs.mongodb.com/manual/reference/operator/query-comparison/

### CRUD Operations (below commands are run in mongodb shell)

#### Create Commands
```
insertOne(<data>, <options>)
insertMany(<data>, <options>)
```

#### Read Commands
```
find(<filter>, <options>)
findOne(<filter>, <options>)
```

#### Update Commands
```
updateOne(<filter>, <updateData>, <options>)
updateMany(<filter>, <updateData>, <options>)
replaceOne(<filter>, <updateData>, <options>)
```

#### Delete Commands
```
deleteOne(<filter>, <options>)
deletemany(<filter>, <options>)
```

##### show all db's
```
show dbs
```

##### Creates DB automatically, when a collection is created with data.
```
use testdb

db.employee.insertOne({"empId": 546, "name": "Vjay", "age": 30, "active": true, "company": "ABC Tech", "rating": 4.35})

show dbs

db.employee.insertOne({empId: 689, "name": "Pjay", "age": 24, "active": false, company: "ABC Tech", rating: 4.99})

db.employee.insertOne({empId: 588, name: "Eshjay", age: 27, active: false, company: "ABC Tech", rating: 4.00})
```
Note: shell will take care of double quote not added to key's in document

##### Find all documents/records in a collection
```
db.employee.find()
db.employee.find({})
db.employee.find().pretty()
db.employee.find({age: {$gt: 20}})
db.employee.findOne() // Shows only first record, if many records found
db.employee.findOne({age: {$gt: 20}}) // Shows only first record, if many records found
```

##### Delete one or many documents/records in a collection
```
db.employee.deleteOne({"name": "Pjay"})
db.employee.deleteMany({})

db.employee.insertMany([{"empId": 546, "name": "Vjay", "age": 30, "active": true, "company": "ABC Tech", "rating": 4.35}, {empId: 689, "name": "Pjay", "age": 24, "active": false, company: "ABC Tech", rating: 4.99}])
db.employee.find({age: {$gt: 20}})

db.employee.deleteMany({age: {$gt: 20}})
```

##### Insert one or many documents/records in a collection
```
db.employee.insertOne({empId: 588, name: "Eshjay", age: 27, active: false, company: "ABC Tech", rating: 4.00})
db.employee.insertMany([{"empId": 546, "name": "Vjay", "age": 30, "active": true, "company": "ABC Tech", "rating": 4.35}, {empId: 689, "name": "Pjay", "age": 24, "active": false, company: "ABC Tech", rating: 4.99}])
```
