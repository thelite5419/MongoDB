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
## Ordered Inserts in MongoDB

When using the `insertMany()` method in MongoDB, you can insert multiple documents at once. By default, MongoDB executes these inserts in order, which means that if an error occurs, the process will stop at that point and no further documents will be inserted.

### Example:
```bash
db.students.insertMany([
    { _id: "C", name: "C", price: 250 },
    { _id: "b", name: "D", price: 350 },
    { _id: "E", name: "E", price: 350 }
])
```

In this case, if a document with `_id: "b"` already exists, the insert will stop at that point and return an error. Any documents after the one that caused the error will **not** be inserted.

### Using the `ordered` Option:
To avoid stopping the insertion when an error occurs, you can use the `ordered: false` option. This allows MongoDB to continue inserting the remaining documents, even if some inserts fail.

```bash
db.students.insertMany([
    { _id: "C", name: "C", price: 250 },
    { _id: "b", name: "D", price: 350 },
    { _id: "E", name: "E", price: 350 }
], { ordered: false })
```

Here, MongoDB will attempt to insert all documents. Even though `_id: "b"` already exists and will raise an error, documents `C` and `E` will still be inserted.

---

## Schema Validation in MongoDB

MongoDB allows you to define validation rules for your collections to ensure that data meets certain criteria before being inserted. This is done using `$jsonSchema` in the collection creation process.

### Example of Schema Validation:
```bash
db.createCollection("nonFiction", {
    validator: {
        $jsonSchema: {
            required: ['name', 'price'],
            properties: {
                name: {
                    bsonType: 'string',
                    description: "must be a string"
                },
                price: {
                    bsonType: 'number',
                    description: "must be a number"
                }
            }
        }
    }
})
```

- **Validator**: Adds validation rules to the collection.
- **$jsonSchema**: Defines the validation schema.
- **Required**: Ensures that certain fields (`name`, `price`) are mandatory when inserting documents.
- **bsonType**: Specifies the data type for each field.
- **Description**: Provides an error message when validation fails.

### Example of Validation Error:
```bash
db.nonFiction.insertOne({ name: "agnipath" })
```

**Error**:
```bash
{
  "failingDocumentId": ObjectId('66feb87b0c0fdfe946c73bfa'),
  "details": {
    "operatorName": "$jsonSchema",
    "schemaRulesNotSatisfied": [
      {
        "operatorName": "required",
        "specifiedAs": { "required": [ 'name', 'price' ] },
        "missingProperties": [ 'price' ]
      }
    ]
  }
}
```

In this case, the document is missing the required `price` field, so MongoDB returns an error.

### Correct Insert:
```bash
db.nonFiction.insertOne({ name: "agnipath", price: 100 })
```

**Result**:
```bash
{
  "acknowledged": true,
  "insertedId": ObjectId('66feb8c60c0fdfe946c73bfb')
}
```

---

## Updating Validation Rules

You can modify the schema validation rules of an existing collection using the `collMod` command.

### Example of Adding a New Field Validation:
```bash
db.runCommand({
    collMod: 'nonFiction',
    validator: {
        $jsonSchema: {
            required: ['name', 'price', 'author'],
            properties: {
                name: {
                    bsonType: 'string',
                    description: "must be a string"
                },
                price: {
                    bsonType: 'number',
                    description: "must be a number"
                },
                author: {
                    bsonType: 'array',
                    description: 'required info not filled',
                    items: {
                        bsonType: 'object',
                        required: ['name', 'email'],
                        properties: {
                            name: { bsonType: 'string' },
                            email: { bsonType: 'string' }
                        }
                    }
                }
            }
        }
    }
})
```

### Example of Insert with New Validation:
```bash
db.nonFiction.insertOne({
    name: "light",
    price: 200,
    author: [{ name: "Prathamesh", email: "" }]
})
```

**Result**:
```bash
{
  "acknowledged": true,
  "insertedId": ObjectId('66febdc28f11758d13c73bf9')
}
```

In this case, the `author` field is required to be an array of objects, each containing `name` and `email`.

### Validation Error Example:
```bash
db.nonFiction.insertOne({
    name: "light",
    price: 200,
    author: ""
})
```

**Error**:
```bash
{
  "failingDocumentId": ObjectId('66febd988f11758d13c73bf8'),
  "details": {
    "operatorName": "$jsonSchema",
    "schemaRulesNotSatisfied": [
      {
        "operatorName": "properties",
        "propertiesNotSatisfied": [
          {
            "propertyName": "author",
            "description": "required info not filled",
            "details": [
              {
                "operatorName": "bsonType",
                "specifiedAs": { "bsonType": "array" },
                "reason": "type did not match",
                "consideredValue": "",
                "consideredType": "string"
              }
            ]
          }
        ]
      }
    ]
  }
}
```

This error occurs because the `author` field is expected to be an array, but a string was provided.
---


## Atomicity in MongoDB

MongoDB provides atomicity at the document level by default. This means that a document is either fully inserted, updated, or not at all. There are no partial updates or inserts, ensuring data integrity for individual operations.

automicity is only done at the documents level

---

## MongoImport in MongoDB

`mongoimport` is a utility used to import JSON documents into MongoDB. Here's how you can use it:

### Installation Steps (Post MongoDB 4.0):

1. Download **MongoDB Command Line Database Tools** (.msi) from the official MongoDB website.
2. Copy the bin path after installation.
3. Open **Environment Variables** (System Settings).
4. Edit the **Path** variable and add the bin path.
5. Open the command prompt and run the following command:

```bash
mongoimport "[file_path]" -d [database_name] -c [collection_name] --jsonArray --drop
```

- `-d`: Specifies the database. If it doesn't exist, MongoDB will create it.
- `-c`: Specifies the collection. If it doesn't exist, MongoDB will create it.
- `--jsonArray`: Informs MongoDB that the input file contains an array of JSON documents.
- `--drop`: Drops the existing collection before importing the new data.

---

## Comparison Operators in MongoDB

MongoDB supports various comparison operators for querying documents.

### `$eq` - Equal
```bash
db.students.find({age: {$eq: 30}})
```
Returns documents where `age` is equal to 30.

### `$ne` - Not Equal
```bash
db.students.find({age: {$ne: 30}})
```
Returns documents where `age` is not equal to 30.

### `$lt` - Less Than
```bash
db.students.find({age: {$lt: 30}})
```
Returns documents where `age` is less than 30.

### `$gt` - Greater Than
```bash
db.students.find({age: {$gt: 30}})
```
Returns documents where `age` is greater than 30.

### `$gte` - Greater Than or Equal
```bash
db.students.find({age: {$gte: 30}})
```
Returns documents where `age` is greater than or equal to 30.

### `$lte` - Less Than or Equal
```bash
db.students.find({age: {$lte: 30}})
```
Returns documents where `age` is less than or equal to 30.

### `$in` - Matches Any Value in Array
```bash
db.students.find({age: {$in: [30, 32]}})
```
Returns documents where `age` is either 30 or 32.

### Example Output:
```json
[
  {
    "_id": ObjectId('66fff8844fd0854591c73bf9'),
    "name": "Jane Smith",
    "age": 32,
    "hobbies": ["painting", "traveling"],
    "hasAadharCard": true
  },
  {
    "_id": ObjectId('66fff8844fd0854591c73bfc'),
    "name": "David Johnson",
    "age": 30,
    "hobbies": ["coding", "playing guitar"],
    "hasAadharCard": true
  }
]
```

### `$nin` - Not in Array
```bash
db.students.find({age: {$nin: [30, 32]}})
```
Returns documents where `age` is neither 30 nor 32.

### Example Output:
```json
[
  {
    "_id": ObjectId('66fff8844fd0854591c73bf8'),
    "name": "John Doe",
    "age": 28,
    "hobbies": ["reading", "cycling", "hiking"],
    "hasAadharCard": true
  },
  {
    "_id": ObjectId('66fff8844fd0854591c73bfb'),
    "name": "Lucy Brown",
    "age": 25,
    "hobbies": ["dancing", "sketching"],
    "hasAadharCard": true
  },
  {
    "_id": ObjectId('66fff8844fd0854591c73c01'),
    "name": "Olivia Martin",
    "age": 26,
    "hobbies": ["gardening", "knitting"],
    "hasAadharCard": true
  }
]
```

---

## Logical Operators in MongoDB

MongoDB also supports a variety of logical operators that allow you to combine multiple conditions in a query. Here’s an overview of the most common logical operators:

- `$and`: Matches documents that satisfy all the specified conditions.
- `$or`: Matches documents that satisfy at least one of the specified conditions.
- `$not`: Inverts the effect of a query expression.
- `$nor`: Matches documents that fail all the specified conditions.

### `$or` - Logical OR

The `$or` operator selects documents where at least one condition is met.

```bash
db.students.find({ $or: [{ age: { $lt: 25 } }, { age: { $gt: 32 } }] })
```

This query retrieves documents where `age` is either less than 25 or greater than 32.

#### Example Output:
```json
[
  {
    "_id": ObjectId('66fff8844fd0854591c73bfa'),
    "name": "Sam Wilson",
    "age": 22,
    "hobbies": ["gaming", "swimming", "photography"],
    "hasAadharCard": false
  },
  {
    "_id": ObjectId('66fff8844fd0854591c73bfe'),
    "name": "Michael Clark",
    "age": 35,
    "hobbies": ["cooking", "woodworking"],
    "hasAadharCard": true
  },
  {
    "_id": ObjectId('66fff8844fd0854591c73bff'),
    "name": "Sophia Miller",
    "age": 24,
    "hobbies": ["writing", "rock climbing"],
    "hasAadharCard": false
  }
]
```

### `$nor` - Logical NOR

The `$nor` operator selects documents that do not match any of the given conditions. It behaves like the opposite of `$or`.

```bash
db.students.find({ $nor: [{ age: { $lt: 25 } }, { age: { $gt: 32 } }] })
```

This query retrieves documents where `age` is neither less than 25 nor greater than 32 (i.e., between 25 and 32).

#### Example Output:
```json
[
  {
    "_id": ObjectId('66fff8844fd0854591c73bf8'),
    "name": "John Doe",
    "age": 28,
    "hobbies": ["reading", "cycling", "hiking"],
    "hasAadharCard": true
  },
  {
    "_id": ObjectId('66fff8844fd0854591c73bf9'),
    "name": "Jane Smith",
    "age": 32,
    "hobbies": ["painting", "traveling"],
    "hasAadharCard": true
  },
  {
    "_id": ObjectId('66fff8844fd0854591c73bfb'),
    "name": "Lucy Brown",
    "age": 25,
    "hobbies": ["dancing", "sketching"],
    "hasAadharCard": true
  }
]
```

### `$and` - Logical AND

The `$and` operator selects documents that meet **all** the specified conditions.

```bash
db.students.find({ $and: [{ age: { $gt: 25 } }, { age: { $lt: 30 } }] })
```

This query retrieves documents where `age` is greater than 25 **and** less than 30.

#### Example Output:
```json
[
  {
    "_id": ObjectId('66fff8844fd0854591c73bf8'),
    "name": "John Doe",
    "age": 28,
    "hobbies": ["reading", "cycling", "hiking"],
    "hasAadharCard": true
  },
  {
    "_id": ObjectId('66fff8844fd0854591c73bfd'),
    "name": "Emma Davis",
    "age": 27,
    "hobbies": ["blogging", "running", "yoga"],
    "hasAadharCard": false
  },
  {
    "_id": ObjectId('66fff8844fd0854591c73c01'),
    "name": "Olivia Martin",
    "age": 26,
    "hobbies": ["gardening", "knitting"],
    "hasAadharCard": true
  }
]
```

**Note:** Without `$and`, MongoDB will interpret the query conditions independently, potentially ignoring the first condition and using only the second one. To enforce both conditions, the `$and` operator is necessary.

```db.students.find({{age: {$gt:25}}, {age:{$lt: 30} } } )```


it ignores the ```{age: {$gt:25}}``` this condition and moves forward to give the answer relatex to the  ```{age:{$lt: 30}}``` this condition 

to avoid this we use the and operator


### `$not` - Logical NOT

The `$not` operator inverts the effect of a query expression. It returns documents that do not match the specified condition.

```bash
db.products.find({
  inStock: { $not: { $eq: true } }
})
```

This query retrieves products where `inStock` is **not true** (i.e., where `inStock` is `false`).

#### Example Output:
```json
[
  { "_id": 2, "name": "Mouse", "price": 25, "inStock": false },
  { "_id": 4, "name": "Keyboard", "price": 100, "inStock": false }
]
```
---
## Element Query Operators in MongoDB

Element query operators in MongoDB help in filtering documents based on whether a field exists or its data type. Two important operators in this category are `$exists` and `$type`.

### `$exists` - Field Existence Check

The `$exists` operator checks if a field exists in a document or not. It can be used to filter documents based on the presence or absence of a specific field.

#### Example:

```bash
db.students.find({ hasLaptop: { $exists: true } })
```

This query retrieves all documents where the `hasLaptop` field exists, regardless of its value.

#### Example Output:
```json
[
  {
    "_id": ObjectId('670008404fd0854591c73c02'),
    "name": "Prathamesh",
    "age": 20,
    "hobbies": ["watching movies", "editing"],
    "hasLaptop": true
  }
]
```

You can combine `$exists` with additional conditions to filter documents more precisely.

#### Example with `$eq`:

```bash
db.students.find({ hasLaptop: { $exists: true, $eq: true } })
```

This query retrieves documents where the `hasLaptop` field exists **and** its value is `true`.

#### Example Output:
```json
[
  {
    "_id": ObjectId('670008404fd0854591c73c02'),
    "name": "Prathamesh",
    "age": 20,
    "hobbies": ["watching movies", "editing"],
    "hasLaptop": true
  }
]
```

### `$type` - Field Type Check

The `$type` operator allows you to filter documents based on the type of the value in a specific field. It is useful when you want to check for fields with specific data types.

#### Example:

```bash
db.students.find({ hasLaptop: { $type: "bool" } })
```

This query retrieves documents where the `hasLaptop` field is of the Boolean (`bool`) type.

#### Example Output:
```json
[
  {
    "_id": ObjectId('670008404fd0854591c73c02'),
    "name": "Prathamesh",
    "age": 20,
    "hobbies": ["watching movies", "editing"],
    "hasLaptop": true
  }
]
```