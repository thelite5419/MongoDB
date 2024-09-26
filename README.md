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

## Insert Operations

In MongoDB, data can be inserted into collections using `insert()`, `insertOne()`, or `insertMany()` methods. Each has a specific use case depending on whether you're inserting one or multiple documents.

### 1. `insert()`
The `insert()` method is an older way of inserting documents. It can insert a single document but has largely been replaced by `insertOne()` and `insertMany()` for modern use.

- Example:
    ```bash
    db.students.insert({ name: "Ajinkya", age: 20 })
    ```
  This command inserts one document into the `students` collection.

### 2. `insertOne()`
The `insertOne()` method is used to insert a single document into a collection.

- Example:
    ```bash
    db.students.insertOne({ name: "Sumit", age: 22 })
    ```
  This is the preferred method for inserting a single document.

### 3. `insertMany()`
The `insertMany()` method is used to insert multiple documents into a collection. The documents are passed as an array of objects.

- Example:
    ```bash
    db.students.insertMany([
        { name: "Omkar", age: 25 },
        { name: "Arun", age: 52 },
        { name: "Anil", age: 30 }
    ])
    ```
  Here, multiple documents are inserted at once. The syntax `[{},{},{}]` is used to pass an array of documents.

---

## Update Operations

In MongoDB, documents can be updated using `updateOne()` and `updateMany()`. These methods are used to modify existing documents in a collection.

### 1. `updateOne()`
The `updateOne()` method is used to update a single document that matches the filter criteria. It follows the pattern where the first argument is the filter (criteria to identify the document), and the second argument specifies the changes to be made using `$set`.

- Example:
    ```bash
    db.students.updateOne({ name: "Prathamesh" }, { $set: { age: 20 } })
    ```
  This will update the `age` field to `20` for the document where `name` is `"Prathamesh"`.

- Syntax:
    ```bash
    db.collection.updateOne(filter, { $set: changes })
    ```

### 2. `updateMany()`
The `updateMany()` method is used when you need to update multiple documents that match the filter criteria. The syntax is similar to `updateOne()` but affects all documents that meet the criteria.

- Example:
    ```bash
    db.students.updateMany({ age: 21 }, { $set: { age: 20 } })
    ```
  This will update all documents where `age` is `21`, changing their `age` to `20`.

- Example with a new field:
    ```bash
    db.students.updateMany({ age: { $gte: 21 } }, { $set: { isEligible: true } })
    ```
  This adds a new field `isEligible: true` to all documents where `age` is greater than or equal to `21`.

---

## Delete Operations

MongoDB provides `deleteOne()` and `deleteMany()` methods to remove documents from a collection. These operations are used to delete one or more documents based on the specified criteria.

### 1. `deleteOne()`
The `deleteOne()` method is used to delete a single document that matches the filter criteria.

- Example:
    ```bash
    db.students.deleteOne({ isEligible: true })
    ```
  This will delete the first document that has `isEligible` set to `true`.

### 2. `deleteMany()`
The `deleteMany()` method is used to delete all documents that match the filter criteria.

- Example:
    ```bash
    db.students.deleteMany({ age: 21 })
    ```
  This will delete all documents where `age` is `21`.

### Deleting All Documents

You can also delete all documents from a collection by passing an empty filter `{}`:

- To delete one document:
    ```bash
    db.students.deleteOne({})
    ```

- To delete all documents:
    ```bash
    db.students.deleteMany({})
    ```

---
## Projection in MongoDB

Projection in MongoDB is similar to selecting specific columns in SQL. It allows you to retrieve only the fields you need from documents within a collection.

### Example:
If you want to retrieve only the `name` field from the `students` collection, you can use the following query:

```bash
db.students.find({}, { name: 1 })
```

Here, `name: 1` acts like a "true" value, meaning only the `name` field will be displayed. However, by default, the `_id` field is also included in the results:

```bash
[
  { _id: ObjectId('66f54345be80faf9a8c73c04'), name: 'Aakash' }
]
```

### Excluding the `_id` Field
If you don’t want the `_id` field to be displayed, you can explicitly exclude it by setting `_id: 0`:

```bash
db.students.find({}, { name: 1, _id: 0 })
```

#### Output:
```bash
[
  { name: 'Aakash' }, { name: 'Ananya' },
  { name: 'Dev' },    { name: 'Riya' },
  { name: 'Kunal' },  { name: 'Simran' },
  { name: 'Yash' },   { name: 'Tanya' },
  { name: 'Harsh' },  { name: 'Priya' },
  { name: 'Shivam' }, { name: 'Aditi' },
  { name: 'Manav' },  { name: 'Snehal' },
  { name: 'Kartik' }, { name: 'Sara' },
  { name: 'Nikhil' }, { name: 'Shreya' },
  { name: 'Rahul' },  { name: 'Ishika' }
]
```

---

## Schemaless Nature of MongoDB

MongoDB is a schemaless database, meaning it does not enforce a fixed structure for documents within a collection. This provides flexibility to insert documents with different fields.

### Example:
```bash
db.students.insertOne({ name: "Prathamesh" })
db.students.insertOne({ name: "Gauri", pan_Id: "xxxxx854" })
```

In the above example, `Prathamesh` has only a `name` field, while `Gauri` has both a `name` and `pan_Id` field.

### Flexibility with Caution
Although MongoDB allows you to add any fields dynamically, this can lead to inconsistencies if not managed carefully. For instance, if you mix data related to different entities (like students and teachers), your data structure could become confusing and harder to retrieve efficiently.

### Example:
```bash
db.teachers.insertOne({
    teacherID: 101,
    name: "Ramesh",
    salary: "8 LPA"
})
```

To avoid issues, it's a good practice to define a schema or structure at the application level, ensuring consistency for easier data retrieval and management.

---

## Data Types in MongoDB

MongoDB supports various data types, which allow flexibility in how you store data.

### Common Data Types:
1. **String** (`text`)
2. **Boolean** (`true` or `false`)
3. **Number** (`integer` or `float`)
4. **ObjectId** (unique ID assigned by MongoDB)
5. **ISODate** (date in ISO format)
6. **Timestamp** (unique time-stamped value)
7. **Array** (list of values)
8. **Embedded Documents** (nested documents within a document)

### Example of Document with Multiple Data Types:
```bash
db.amazon.insertOne({
    name: "Amazon",
    fund: 45842297,
    isAvailable: true,
    emp: [
        { name: "Ajinkya" },
        { name: "Nikhil" }
    ],
    foundOn: new Date(),
    timestamp: Timestamp()
})
```

#### Output:
```bash
[
  {
    _id: ObjectId('66f5491dbe80faf9a8c73c22'),
    name: 'Amazon',
    fund: 45842297,
    isAvailable: true,
    emp: [ { name: 'Ajinkya' }, { name: 'Nikhil' } ],
    foundOn: ISODate('2024-09-26T11:44:29.739Z'),
    timestamp: Timestamp({ t: 1727351069, i: 1 })
  }
]
```

In this example, you can see the use of different data types like `ObjectId`, `ISODate`, and `Timestamp`, as well as an array for the `emp` field, which stores a list of employees.

### Checking Data Types
You can check the data type of any field using the `typeof` operator:

#### Example Queries:
```bash
typeof db.amazon.findOne().name        // Returns: string
typeof db.amazon.findOne()._id         // Returns: object
typeof db.amazon.findOne().timestamp   // Returns: object
typeof db.amazon.findOne().emp         // Returns: object
typeof db.amazon.findOne().isAvailable // Returns: boolean
```

---
