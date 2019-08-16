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
```sql
insertOne(<data>, <options>)
insertMany(<data>, <options>)
```

#### Read Commands
```sql
find(<filter>, <options>)
findOne(<filter>, <options>)
```

#### Update Commands
```sql
updateOne(<filter>, <updateData>, <options>)
updateMany(<filter>, <updateData>, <options>)
replaceOne(<filter>, <updateData>, <options>)
```

#### Delete Commands
```sql
deleteOne(<filter>, <options>)
deletemany(<filter>, <options>)
```

##### show all db's, collections
```sql
show dbs
use testdb
show collections
```

##### Creates DB automatically, when a collection is created with data.
```sql
use testdb

db.employee.insertOne({"empId": 546, "name": "Vjay", "age": 30, "active": true, "company": "ABC Tech", "rating": 4.35})

show dbs

db.employee.insertOne({empId: 689, "name": "Pjay", "age": 24, "active": false, company: "ABC Tech", rating: 4.99})

db.employee.insertOne({empId: 588, name: "Eshjay", age: 27, active: false, company: "ABC Tech", rating: 4.00})
```
Note: shell will take care of double quote not added to key's in document

##### Find all documents/records in a collection
```sql
db.employee.find()
db.employee.find({})
db.employee.find().pretty()
db.employee.find({age: {$gt: 20}})
db.employee.findOne() // Shows only first record, if many records found
db.employee.findOne({age: {$gt: 20}}) // Shows only first record, if many records found
```

##### Delete one or many documents/records in a collection
```sql
db.employee.deleteOne({"name": "Pjay"})
db.employee.deleteMany({})

db.employee.insertMany([{"empId": 546, "name": "Vjay", "age": 30, "active": true, "company": "ABC Tech", "rating": 4.35}, {empId: 689, "name": "Pjay", "age": 24, "active": false, company: "ABC Tech", rating: 4.99}])
db.employee.find({age: {$gt: 20}})

db.employee.deleteMany({age: {$gt: 20}})
```

##### Insert one or many documents/records in a collection
```sql
db.employee.insertOne({empId: 588, name: "Eshjay", age: 27, active: false, company: "ABC Tech", rating: 4.00})
db.employee.insertMany([{"empId": 546, "name": "Vjay", "age": 30, "active": true, "company": "ABC Tech", "rating": 4.35}, {empId: 689, "name": "Pjay", "age": 24, "active": false, company: "ABC Tech", rating: 4.99}])
```

##### Update one or many documents/records in a collection
```sql
db.employee.updateOne({name: "Eshjay"}, {$set: {active: true}})
db.employee.updateMany({age: {$gt: 25}}, {$set: {active: true}})
db.employee.updateMany({age: {$gt: 20}}, {$set: {active: true}})
db.employee.updateMany({}, {$set: {active: true}})
db.employee.updateMany({age: {$gt: 25}}, {$set: {designation: "professional 2"}}) // adds new attribute, if not existing or else update
db.employee.updateMany({}, {$set: {designation: "developer"}}) // adds new attribute, if not existing or else update
```


https://docs.mongodb.com/manual/reference/method/db.collection.replaceOne/#db.collection.replaceOne

##### Replace one
```sql
db.employee.replaceOne({name: "Eshjay"}, { "empId" : 588, "name" : "E-jay", "age" : 26, "active" : true, "company" : "ABC Tech Inc", "rating" : 4.1, "designation" : "developer" })
db.employee.replaceOne({name: "Eshjay"}, { "empId" : 666, "name" : "Eshjay", "age" : 27, "active" : true, "company" : "ABC Tech", "rating" : 4.12, "designation" : "developer" }) // will not replace as name: "Eshjay" was already updated above and no record found for the condition
db.employee.replaceOne({name: "Eshjay"}, { "empId" : 666, "name" : "Eshjay", "age" : 27, "active" : true, "company" : "ABC Tech", "rating" : 4.12, "designation" : "developer" }, { upsert: true }) // will insert new record when matching record is not found as upsert: true is passed
```


find() function in mongodb will not return total results, instead it returns a Cursor.
Which can be used for iterating through result set, by default shell will print first 20 records and then use it command for more results. Let's see this with an example below, creating a collection of passengers json available in db-data folder.

```sql
db.passengers.find().pretty() // Gives Cursor and need to run it command for more results
db.passengers.find().toArray() // Will traverse trough the result set and print all results as array
db.passengers.find().forEach(passengersData => printjson(passengersData)) // prints all by traversing result set. Lambda funtions written here is javascript, as mongo DB shell runs on javascript
```

##### drop db's, collections
```sql
show dbs
use testdb
show collections

db.employee.drop()
db.passengers.drop()
db.dropDatabase()
```

### Projection
https://docs.mongodb.com/manual/tutorial/project-fields-from-query-results/


We will take inventory collection from mongodb tutorial, inventory.json added in db-data. We will also add corresponding SQL statement for better understanding
##### projection examples
```sql
show dbs
use testdb
show collections

db.inventory.insertMany(<use inventory.json data>)

db.inventory.find( { status: "A" } )
SELECT * from inventory WHERE status = "A"

db.inventory.find({ status: "A" } , {item: 1, status: 1}) // Return the specified fields as "1" in options and the _id field Only
SELECT _id, item, status from inventory WHERE status = "A"

db.inventory.find({ status: "A" } , {item: 1, status: 1, _id: 0}) // Suppresses the _id field as it is passed with "0" in options
SELECT item, status from inventory WHERE status = "A"
// Note: With the exception of the _id field, you cannot combine inclusion and exclusion statements in projection documents.

db.inventory.find({ status: "A" } , {item: 0, status: 0}) // Return all fields excluding fields mentioned in options as "0"
db.inventory.find({ status: "A" } , {item: 0, status: 0, _id: 0})
db.inventory.find({ status: "A" } , {item: 1, status: 1, "size.uom": 1}) // return specific fields in an embedded document
db.inventory.find({ status: "A" } , {"size.uom": 0}) // suppress specific fields in an embedded document
db.inventory.find({ status: "A" } , {item: 1, status: 1, "instock": 1})
db.inventory.find({ status: "A" } , {item: 1, status: 1, "instock.qty": 1}) // project specific fields inside documents embedded in an array

https://docs.mongodb.com/manual/reference/operator/projection/slice/#proj._S_slice

db.inventory.find({ status: "A" } , {item: 1, status: 1, instock: {$slice: -1}})
db.inventory.find({ status: "A" } , {item: 1, status: 1, instock: {$slice: -2}})
db.inventory.find({ status: "A" } , {item: 1, status: 1, instock: {$slice: -3}})
db.inventory.find({ status: "A" } , {item: 1, status: 1, instock: {$slice: 0}})
db.inventory.find({ status: "A" } , {item: 1, status: 1, instock: {$slice: 1}})
db.inventory.find({ status: "A" } , {item: 1, status: 1, instock: {$slice: 2}})
db.inventory.find({ status: "A" } , {item: 1, status: 1, instock: {$slice: 3}})
db.inventory.find({ status: "A" } , {item: 1, status: 1, instock: {$slice: [1, 1]}})
```
