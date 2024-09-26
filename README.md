# MongoDB

## What is MongoDB?

MongoDB is a highly scalable, document-oriented database designed to store large amounts of data. The term "Mongo" comes from the word "humongous," which indicates its ability to handle massive datasets.

### Key Concepts

- **Collections**: Equivalent to tables in relational databases like MySQL. For example, collections can be named `food`, `employees`, or `students`.
- **Documents**: Similar to rows in SQL, documents are the actual records stored in collections. Documents in MongoDB are stored in **JSON (JavaScript Object Notation)** format. Here's an example document in an `employees` collection:

    ```json
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

- **Flexibility**: Unlike traditional relational databases, MongoDB allows you to insert documents with different structures. For example, you can add a new field to a document without altering the entire collection:

    ```json
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

  In MongoDB, you are not restricted by predefined columns, making it much more flexible than databases like MySQL.

- **Binary JSON (BSON)**: Data in MongoDB is stored in BSON format (Binary JSON), which allows for efficient storage and retrieval of documents.

---

## Installing MongoDB

To get started with MongoDB, you need to download and install it from the MongoDB community website. The installation provides a graphical user interface (GUI) to interact with your databases.

### Starting and Stopping MongoDB Services

You can control MongoDB services via the command line:

- To stop the MongoDB service:
    ```bash
    net stop mongodb
    ```

- To start the MongoDB service:
    ```bash
    net start mongodb
    ```

### MongoDB Shell

To interact with MongoDB databases through the command line, you need to download the MongoDB Shell. This allows you to run commands and queries directly.

---

## Creating a Database in MongoDB

Here are some basic commands to work with MongoDB databases and collections:

- Show all databases:
    ```bash
    show dbs
    ```

- Create and switch to a new database:
    ```bash
    use latestDB
    ```
    Note: If `latestDB` does not exist, MongoDB will create it automatically.

- Create a collection:
    ```bash
    db.createCollection("students")
    ```

- Insert a document into the collection:
    ```bash
    db.students.insertOne({ name: "Prathamesh", age: 12 })
    ```

- Retrieve all documents from the `students` collection:
    ```bash
    db.students.find()
    ```

- Drop (delete) the collection:
    ```bash
    db.students.drop()
    ```

---

## CRUD Operations in MongoDB

CRUD (Create, Read, Update, Delete) operations in MongoDB are performed through various commands:

### Create
- Insert a single document:
    ```bash
    db.collection.insertOne(document)
    ```

- Insert multiple documents:
    ```bash
    db.collection.insertMany(documents)
    ```

### Read
- Retrieve all documents from a collection:
    ```bash
    db.collection.find(filter, options)
    ```

- Retrieve a single document:
    ```bash
    db.collection.findOne(filter, options)
    ```

### Update
- Update one or more documents:
    ```bash
    db.collection.update(filter, update, options)
    ```

- Update a single document:
    ```bash
    db.collection.updateOne(filter, update, options)
    ```

- Replace a document entirely:
    ```bash
    db.collection.replaceOne(filter, replacement, options)
    ```

### Delete
- Delete all documents matching the filter:
    ```bash
    db.collection.deleteMany(filter, options)
    ```

- Delete a single document:
    ```bash
    db.collection.deleteOne(filter, options)
    ```

---

## Find vs FindOne in MongoDB

- **`find()`**: Retrieves all documents matching the filter. It's similar to `SELECT *` in SQL.
    ```bash
    db.students.find({ age: 21 })
    ```

    Example result:
    ```json
    [
      { "_id": ObjectId('66f2cff3037dc0d133c73bf9'), "name": "Gauri", "age": 21 }
    ]
    ```

- **`findOne()`**: Retrieves only one document that matches the filter.
    ```bash
    db.students.findOne({ age: 20 })
    ```

- To be more specific, you can pass multiple conditions, similar to the `WHERE` clause in SQL:
    ```bash
    db.students.findOne({ age: 20, name: "Aditya" })
    ```

---

## Working with Cursors

In MongoDB, the `find()` command returns a **cursor**, which acts like a pointer to the result set, allowing you to iterate over documents.

- **Limit the number of documents**:
    ```bash
    db.students.find().limit(2)
    ```

- **Counting documents**:
    ```bash
    db.students.find().count()
    ```

- **Iterate over documents with JavaScript**:
    ```bash
    db.students.find().forEach(function(document) {
        printjson(document)
    })
    ```

---

## Querying with Comparison Operators

MongoDB supports comparison operators like `$lt`, `$lte`, `$gt`, and `$gte` to filter documents based on numerical values.

- Example queries:
    ```bash
    db.students.find({ age: { $lt: 20 } }).count()    // Less than 20
    db.students.find({ age: { $lte: 20 } }).count()   // Less than or equal to 20
    db.students.find({ age: { $gte: 20 } }).count()   // Greater than or equal to 20
    db.students.find({ age: { $gte: 20, $lte: 21 } }).count()  // Between 20 and 21
    ```

---

By following these steps and commands, you can easily manage databases, collections, and documents in MongoDB. MongoDB's flexibility and scalability make it a great choice for modern web applications, especially those dealing with large amounts of unstructured data.