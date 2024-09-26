```plaintext
MongoDB
```

## What is MongoDB?

MongoDB is a highly scalable, document-oriented database designed to store large amounts of data. The term "Mongo" comes from the word "humongous," which indicates its ability to handle massive datasets.

### Key Concepts

**Collections**: Equivalent to tables in relational databases like MySQL. For example, collections can be named `food`, `employees`, or `students`.

**Documents**: Similar to rows in SQL, documents are the actual records stored in collections. Documents in MongoDB are stored in **JSON (JavaScript Object Notation)** format. Here's an example document in an `employees` collection:

**Flexibility**: Unlike traditional relational databases, MongoDB allows you to insert documents with different structures. For example, you can add a new field to a document without altering the entire collection:

In MongoDB, you are not restricted by predefined columns, making it much more flexible than databases like MySQL.

**Binary JSON (BSON)**: Data in MongoDB is stored in BSON format (Binary JSON), which allows for efficient storage and retrieval of documents.

## Installing MongoDB

To get started with MongoDB, you need to download and install it from the MongoDB community website. The installation provides a graphical user interface (GUI) to interact with your databases.

### Starting and Stopping MongoDB Services

You can control MongoDB services via the command line:

To stop the MongoDB service:

To start the MongoDB service:

### MongoDB Shell

To interact with MongoDB databases through the command line, you need to download the MongoDB Shell. This allows you to run commands and queries directly.

## Creating a Database in MongoDB

Here are some basic commands to work with MongoDB databases and collections:

Show all databases:

Create and switch to a new database:

Note: If `latestDB` does not exist, MongoDB will create it automatically.

Create a collection:

Insert a document into the collection:

Retrieve all documents from the `students` collection:

Drop (delete) the collection:

## CRUD Operations in MongoDB

CRUD (Create, Read, Update, Delete) operations in MongoDB are performed through various commands:

### Create

Insert a single document:

Insert multiple documents:

### Read

Retrieve all documents from a collection:

Retrieve a single document:

### Update

Update one or more documents:

Update a single document:

Replace a document entirely:

### Delete

Delete all documents matching the filter:

Delete a single document:

## Find vs FindOne in MongoDB

`**find()**`: Retrieves all documents matching the filter. It's similar to `SELECT *` in SQL.

Example result:

`**findOne()**`: Retrieves only one document that matches the filter.

To be more specific, you can pass multiple conditions, similar to the `WHERE` clause in SQL:

## Working with Cursors

In MongoDB, the `find()` command returns a **cursor**, which acts like a pointer to the result set, allowing you to iterate over documents.

**Limit the number of documents**:

**Counting documents**:

**Iterate over documents with JavaScript**:

## Querying with Comparison Operators

MongoDB supports comparison operators like `$lt`, `$lte`, `$gt`, and `$gte` to filter documents based on numerical values.

*   Example queries:

By following these steps and commands, you can easily manage databases, collections, and documents in MongoDB. MongoDB's flexibility and scalability make it a great choice for modern web applications, especially those dealing with large amounts of unstructured data.

```plaintext
db.students.find({ age: { $lt: 20 } }).count()    // Less than 20
db.students.find({ age: { $lte: 20 } }).count()   // Less than or equal to 20
db.students.find({ age: { $gte: 20 } }).count()   // Greater than or equal to 20
db.students.find({ age: { $gte: 20, $lte: 21 } }).count()  // Between 20 and 21
```

```plaintext
db.students.find().forEach(function(document) {
    printjson(document)
})
```

```plaintext
db.students.find().count()
```

```plaintext
db.students.find().limit(2)
```

```plaintext
db.students.findOne({ age: 20, name: "Aditya" })
```

```plaintext
db.students.findOne({ age: 20 })
```

```plaintext
[
  { "_id": ObjectId('66f2cff3037dc0d133c73bf9'), "name": "Gauri", "age": 21 }
]
```

```plaintext
db.students.find({ age: 21 })
```

```plaintext
db.collection.deleteOne(filter, options)
```

```plaintext
db.collection.deleteMany(filter, options)
```

```plaintext
db.collection.replaceOne(filter, replacement, options)
```

```plaintext
db.collection.updateOne(filter, update, options)
```

```plaintext
db.collection.update(filter, update, options)
```

```plaintext
db.collection.findOne(filter, options)
```

```plaintext
db.collection.find(filter, options)
```

```plaintext
db.collection.insertMany(documents)
```

```plaintext
db.collection.insertOne(document)
```

```plaintext
db.students.drop()
```

```plaintext
db.students.find()
```

```plaintext
db.students.insertOne({ name: "Prathamesh", age: 12 })
```

```plaintext
db.createCollection("students")
```

```plaintext
use latestDB
```

```plaintext
show dbs
```

```plaintext
net start mongodb
```

```plaintext
net stop mongodb
```

```plaintext
{
    "name": "Prathamesh",
    "age": 20,
    "city": "Karad",
    "ID": {
        "Aadhar": "80xxxxx",
        "PAN": "xxxxxx"
    },
    "previousJob": {
        "company": "Amazon",
        "package": "8 LPA"
    }
}
```

```plaintext
{
    "name": "Amit",
    "age": 27,
    "city": "Karad",
    "ID": {
        "Aadhar": "80xxxxx",
        "PAN": "xxxxxx"
    }
}
```