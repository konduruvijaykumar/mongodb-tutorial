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

### CRUD Operations

show all db's
```
show dbs
```

Creates DB automatically, when a collection is created with data.
```
use testdb

db.employee.insertOne({"empId": 546, "name": "Vjay", "age": 30, "active": true, "company": "ABC Tech", "rating": 4.35})

show dbs
```

Find all documents or records in a collection
```
db.employee.find()
```
