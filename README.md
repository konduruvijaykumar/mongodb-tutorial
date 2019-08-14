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

### CRUD Operations (below commands are run in mongodb shell)

#### Create Commands
```
insertOne(data, options)
insertMany(data, options)
```

#### Read Commands
```
find(filter, options)
findOne(filter, options)
```

#### Update Commands
```
updateOne(filter, data, options)
updateMany(filter, data, options)
replaceOne(filter, data, options)
```

#### Delete Commands
```
deleteOne(filter, options)
deletemany(filter, options)
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

##### Find all documents or records in a collection
```
db.employee.find()
db.employee.find().pretty()
```
