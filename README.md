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
---

## Evaluation Operators in MongoDB

Evaluation operators in MongoDB allow you to perform complex operations, comparisons, and expressions directly within your queries. These operators are particularly useful for running calculations and conditional checks during data retrieval. Below are some commonly used evaluation operators:

### `$expr` - Expression Evaluation

The `$expr` operator enables the use of MongoDB expressions to evaluate conditions within queries. You can perform comparisons, arithmetic operations, and other expressions within query pipelines.

#### Example:

```bash
db.collection.find({
  $expr: {
    $gt: ["$field1", "$field2"]
  }
})
```

This query finds all documents where `field1` is greater than `field2`.

#### Arithmetic Example:

```bash
db.collection.find({
  $expr: {
    $gt: ["$price", { $avg: "$price" }]
  }
})
```

This query retrieves all documents where the value of `price` is greater than the average `price` value of all documents in the collection.

> **Note:** The `$expr` operator was introduced in MongoDB 3.6 and is very versatile, supporting all aggregation expressions.

---

### `$regex` - Regular Expression Pattern Matching

The `$regex` operator is used to search for documents by matching fields against regular expression patterns. It's useful for string pattern searches, like finding documents where a string starts or ends with a certain character.

#### Example:

```bash
db.students.find({ name: { $regex: /^p/ } })
```

This query finds all documents where the `name` field starts with the letter "P".

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

---

### `$text` - Text Search

The `$text` operator enables text-based search within documents. MongoDB uses a text index to search for matching text in specified fields.

#### Example:

```bash
db.students.find({
  $text: {
    $search: "writing"
  }
})
```

This query will return documents where the text field contains the word "writing".

> **Note:** To use `$text`, you must first create a text index on the fields where you want to perform the search.

---

### `$mod` - Modulo Operation

The `$mod` operator performs a modulo operation, which returns documents where the field's value divided by a specified number has a remainder that matches a given value.

#### Example:

```bash
db.students.find({
  age: {
    $mod: [3, 0]
  }
})
```

This query returns documents where the `age` field divided by 3 has a remainder of 0, meaning the age is a multiple of 3.

#### Example Output:

```json
[
  {
    "_id": ObjectId('66fff8844fd0854591c73bfc'),
    "name": "David Johnson",
    "age": 30,
    "hobbies": ["coding", "playing guitar"],
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
    "_id": ObjectId('66fff8844fd0854591c73bff'),
    "name": "Sophia Miller",
    "age": 24,
    "hobbies": ["writing", "rock climbing"],
    "hasAadharCard": false
  }
]
```

In this example, the query returns students whose age is divisible by 3.

---

## Querying Arrays in MongoDB

MongoDB allows querying arrays in documents efficiently, whether the array contains simple values (like strings) or complex objects. Below are common use cases and how to handle them.

### Querying Arrays with Objects

Suppose you have a document like the following:

```json
{
  name: 'Gauri',
  age: 21,
  hobbies: ['talking', 'dancing'],
  hasAadharCard: true,
  experience: [
    {
      companyName: 'Company XYZ',
      duration: '2 years'
    },
    {
      companyName: 'Amazon',
      duration: '2 years'
    }
  ]
}
```

### Query to Find Documents with a Specific Array Element

To find people who have worked at **Amazon**, you can query an object within an array:

```bash
db.students.find({ "experience.companyName": "Amazon" })
```

#### Example Output:

```json
[
  {
    "_id": ObjectId('67010fa8b3f83f2a05c73bfb'),
    "name": "Gauri",
    "age": 21,
    "hobbies": ["talking", "dancing"],
    "hasAadharCard": true,
    "experience": [
      { "companyName": "Company XYZ", "duration": "2 years" },
      { "companyName": "Amazon", "duration": "2 years" }
    ]
  }
]
```

### Querying Simple Arrays

If the array contains simple values like strings, such as in the `hobbies` field, you can search for an array element as follows:

```bash
db.students.find({ hobbies: "talking" })
```

This query will return all documents where the `hobbies` array contains the string "talking."

### Query to Count Documents

To find the number of people who have worked at **Amazon**, use:

```bash
db.students.find({ "experience.companyName": "Amazon" }).size()
```

This query will return the count of documents that match the condition.

### Querying Arrays Based on Length

You can query documents based on the length of an array field using the `$size` operator:

- To find students who have **only one company** in their `experience` array:

```bash
db.students.find({ experience: { $size: 1 } })
```

> **Note:** MongoDB does not support conditional operators (like `$gte`, `$lte`) directly with `$size`. For complex size-based queries, you can use the `$expr` operator.

### Conditional Array Length Queries

If you want to find documents where the `experience` array has **two or more companies**, you can use `$expr`:

```bash
db.students.find({
  $expr: { $gte: [{ $size: "$experience" }, 2] }
})
```

This query returns documents where the size of the `experience` array is greater than or equal to 2.

---

## Sorting Documents in MongoDB

MongoDB allows sorting documents based on one or more fields. You can specify the sort order using:

- `1` for **ascending** order
- `-1` for **descending** order

### Sorting by One Field

To sort the documents based on the `age` field in **ascending order**:

```bash
db.students.find().sort({ age: 1 })
```

To sort documents by `age` in **descending order**:

```bash
db.students.find().sort({ age: -1 })
```

### Sorting by Multiple Fields

You can also sort by multiple fields. If sorting by `age` in ascending order, but if two documents have the same `age`, they are then sorted by `name` in **descending order**:

```bash
db.students.find().sort({ age: 1, name: -1 })
```

### Getting Sorted Documents as an Array

By default, MongoDB returns a cursor for the `find()` query. If you want all documents returned at once and sorted, you can use the `.forEach()` function or chaining like `.toArray()` for further operations. Additionally, you can use `.limit()` or `.skip()` to control the number of documents returned or offset the results.

---

## Advanced Update Operations in MongoDB

MongoDB provides several advanced update operators that allow you to modify documents in various ways. Below are the most commonly used operators, with practical examples.

### 1. `$inc`: Increment or Decrement Field Values

The `$inc` operator increments or decrements the value of a field by a specified amount. It is commonly used to adjust numerical fields, such as counters or ages.

- To **increment** the age by 1 for all documents:

```bash
db.students.updateMany({}, { $inc: { age: 1 } })
```

- To **decrement** the age by 1 for all documents:

```bash
db.students.updateMany({}, { $inc: { age: -1 } })
```

---

### 2. `$min` and `$max`: Setting Minimum and Maximum Values

- The `$max` operator **increases** the value of a field if the new value is greater than the current value.
  
- The `$min` operator **decreases** the value of a field if the new value is smaller than the current value.

#### Example:

- To set the `age` of **Gauri** to a **maximum** value of 25 (if it's lower than 25, it will be updated to 25):

```bash
db.students.updateMany({ name: "gauri" }, { $max: { age: 25 } })
```

- To set the `age` of **Gauri** to a **minimum** value of 20 (if it's higher than 20, it will be updated to 20):

```bash
db.students.updateMany({ name: "gauri" }, { $min: { age: 20 } })
```

---

### 3. `$mul`: Multiply Field Values

The `$mul` operator multiplies the value of a field by a specified factor. It is useful when you need to apply a scaling factor to numeric fields.

- To **double** the age of **Gauri** (multiply by 2):

```bash
db.students.updateMany({ name: "gauri" }, { $mul: { age: 2 } })
```

#### Example Output:

After multiplying Gauri's age by 2, the document will look like this:

```json
{
  "_id": ObjectId('67010fa8b3f83f2a05c73bfb'),
  "name": "gauri",
  "age": 40,
  "hobbies": ["talking", "dancing"],
  "hasAadharCard": true,
  "experience": [
    { "companyName": "Company XYZ", "duration": "2 years" },
    { "companyName": "Amazon", "duration": "2 years" }
  ]
}
```

---

### 4. `$unset`: Remove a Field

The `$unset` operator removes a field from a document. This is useful if you no longer need a particular field in your documents.

- To remove the `experience` field from all documents:

```bash
db.students.updateMany({}, { $unset: { experience: "" } })
```

---

### 5. `$rename`: Rename a Field

The `$rename` operator changes the name of a field. It is helpful when you want to modify the schema without losing data.

- To rename the field `value` to `age`:

```bash
db.students.updateMany({}, { $rename: { value: "age" } })
```

---

### 6. `$upsert`: Insert a Document if No Match is Found

The `$upsert` option is used with the `update` operation. If the query does not match any documents, it **inserts** a new document with the specified update fields.

- To **insert** a document for **Prathamesh** with an `age` of 20 if no such document exists:

```bash
db.students.updateMany({ name: "prathamesh" }, { $set: { age: 20 } }, { upsert: true })
```

#### Example Output:

If no document with the name **Prathamesh** exists, the query will insert a new document:

```json
{
  "_id": ObjectId('670123540600953f5b38d7d7'),
  "name": "prathamesh",
  "age": 20
}
```

---
## MongoDB Array Update Operations

MongoDB allows you to update arrays in documents using various operators. These operators make it easy to add, remove, or modify elements in an array field.

### 1. Updating Nested Arrays

To update specific elements within a nested array, we can use `$elemMatch` to match the condition and then apply the update. For example, consider the following document:

```json
{
  _id: ObjectId('67010fa8b3f83f2a05c73bfb'),
  name: 'gauri',
  hobbies: [ 'talking', 'dancing' ],
  hasAadharCard: true,
  experience: [
    { companyName: 'Company XYZ', duration: '2 years' },
    { companyName: 'Amazon', duration: '2 years' }
  ],
  age: 20
}
```

#### Scenario: Add a field `experienced: true` to the company where the `duration` is '2 years'.

```bash
db.students.updateMany(
  { "experience": { $elemMatch: { duration: "2 years" } } },
  { $set: { "experience.$.experienced": true } }
)
```

#### Example Output:

```json
[
  {
    _id: ObjectId('67010fa8b3f83f2a05c73bfb'),
    name: 'gauri',
    hobbies: [ 'talking', 'dancing' ],
    hasAadharCard: true,
    experience: [
      {
        companyName: 'Company XYZ',
        duration: '2 years',
        experienced: true
      },
      {
        companyName: 'Amazon',
        duration: '2 years'
      }
    ],
    age: 20
  }
]
```

This update adds the field `experienced: true` to the company with `duration: '2 years'`.

---

### 2. `$push`: Add an Element to an Array

The `$push` operator allows you to **add an element** to the end of an array. If the field is not an array, `$push` creates it.

- To add a new company to Gauri's `experience` array:

```bash
db.students.updateOne(
  { name: 'gauri' },
  { $push: { experience: { companyName: 'Meta', duration: '3 years' } } }
)
```

---

### 3. `$pull`: Remove an Element from an Array

The `$pull` operator removes all elements from an array that match a specified condition.

- To **remove** the company `Meta` from Gauri's `experience` array:

```bash
db.students.updateOne(
  { name: 'gauri' },
  { $pull: { experience: { companyName: 'Meta', duration: '3 years' } } }
)
```

---

### 4. `$addToSet`: Add an Element to an Array (No Duplicates)

The `$addToSet` operator adds a value to an array **only if it does not already exist**. This prevents duplicates.

- To add a company to Gauri's `experience` array only if it doesn't already exist:

```bash
db.students.updateOne(
  { name: 'gauri' },
  { $addToSet: { experience: { companyName: 'Meta', duration: '3 years' } } }
)
```

If `Meta` with `3 years` already exists in the `experience` array, this operation will not add it again.

---

### 5. `$pop`: Remove the First or Last Element of an Array

The `$pop` operator removes an element from the beginning or end of an array.

- To remove the **last** element from Gauri's `experience` array:

```bash
db.students.updateOne(
  { name: 'gauri' },
  { $pop: { experience: 1 } }
)
```

- To remove the **first** element from Gauri's `experience` array:

```bash
db.students.updateOne(
  { name: 'gauri' },
  { $pop: { experience: -1 } }
)
```

---

### Example Document Before and After Updates:

#### Original Document:

```json
{
  _id: ObjectId('67010fa8b3f83f2a05c73bfb'),
  name: 'gauri',
  hobbies: [ 'talking', 'dancing' ],
  hasAadharCard: true,
  experience: [
    { companyName: 'Company XYZ', duration: '2 years' },
    { companyName: 'Amazon', duration: '2 years' }
  ],
  age: 20
}
```

#### After Adding `experienced: true`:

```json
{
  _id: ObjectId('67010fa8b3f83f2a05c73bfb'),
  name: 'gauri',
  hobbies: [ 'talking', 'dancing' ],
  hasAadharCard: true,
  experience: [
    { companyName: 'Company XYZ', duration: '2 years', experienced: true },
    { companyName: 'Amazon', duration: '2 years' }
  ],
  age: 20
}
```

#### After Pushing `Meta` to the Array:

```json
{
  _id: ObjectId('67010fa8b3f83f2a05c73bfb'),
  name: 'gauri',
  hobbies: [ 'talking', 'dancing' ],
  hasAadharCard: true,
  experience: [
    { companyName: 'Company XYZ', duration: '2 years', experienced: true },
    { companyName: 'Amazon', duration: '2 years' },
    { companyName: 'Meta', duration: '3 years' }
  ],
  age: 20
}
```

---
## MongoDB Indexing
### **1. Collection Scan (Collscan)**:
- A **collection scan** (`collscan`) is similar to a **linear search**, where MongoDB searches through each document in the collection one by one, in the order they are stored.
- This method is slow and inefficient for large collections.
  
#### Example:
```bash
db.collectionName.find();
```
- This query performs a full scan of the collection, which can take longer as the size of the collection increases.



### **2. Indexing Scan**:
- An **indexing scan** is a faster, more efficient search technique that uses indexing, similar to a **binary search**.
- **Indexes** are applied on specific fields like `age`, `name`, or `salary` and are stored separately in a **sorted** structure.
  
When querying an indexed field:
- MongoDB first searches the index (which is sorted) using a **binary search**, speeding up the data retrieval process.
- Once the correct entry is found in the index, it uses the **pointer** to quickly locate the actual document in the collection.


### **How Indexing Works**:
- **Indexes** are stored in a **B-tree data structure**, which contains **index keys** and **pointers** to the original documents.
- Indexing helps MongoDB avoid scanning the entire collection and instead, allows it to navigate through a smaller, sorted set of keys.
  
### **Space and Performance Considerations**:
- While indexing significantly improves read performance, it comes with trade-offs:
  - **Space**: Indexes take up additional disk space to store sorted structures.
  - **Write Performance**: When indexed values are updated, the corresponding index tree needs to adjust, which can slow down write operations.
  
Due to this, not all fields should be indexed, especially in cases like:
- Frequently updated collections.
- Complex queries.
- Large collections where too many indexes may lead to overhead.



### **1. Single Field Index**

A **single field index** is created on a specific field in the collection to improve query performance. It allows MongoDB to quickly search, sort, or retrieve documents based on the indexed field.

#### Example:
```bash
db.collectionName.find().explain("executionStats");
```
- This command provides insight into the query execution plan, including whether a **collection scan (collscan)** or an **index scan (indexscan)** is being used.

```bash
db.collectionName.createIndex({age: 1});
```
- Creates an ascending index on the `age` field.

```bash
db.collectionName.getIndexes();
```
- Lists all available indexes in the collection:
  ```json
  [
    { v: 2, key: { _id: 1 }, name: '_id_' },
    { v: 2, key: { age: 1 }, name: 'age_1' }
  ]
  ```

- You can also create a **descending order** index:
  ```bash
  db.collectionName.createIndex({age: -1});
  ```

#### When Not to Use Indexing:
- When the **collection is small**.
- When queries are **complex** (using multiple fields).
- When the **collection is frequently updated**, as indexing can slow down write operations.
- When the **collection is large** (too many indexes can degrade performance).

---

### **2. Compound Index**

A **compound index** is an index on multiple fields. It allows MongoDB to efficiently query on combinations of fields, improving performance for more complex queries.

#### Example:
```bash
db.collectionName.createIndex({age: 1, gender: 1});
```
- This creates a compound index on `age` and `gender`. If multiple documents have the same `age`, MongoDB will further sort them by `gender` (alphabetically, so females appear first).

```bash
db.collectionName.getIndexes();
```
- Lists the compound index:
  ```json
  [
    { v: 2, key: { _id: 1 }, name: '_id_' },
    { v: 2, key: { age: 1, gender: 1 }, name: 'age_1_gender_1' }
  ]
  ```

#### Example Query with Compound Index:
```bash
db.collectionName.find({age: {$gte: 25}, gender: "male"}).explain("executionStats");
```
- This query will use the **index scan** for both `age` and `gender`.

- **Note**: If you only query on `age`, the **index scan** will be used. But if you only query on `gender`, a **collection scan** may happen, as `gender` is sorted based on `age`.

#### Partial Index:
You can create partial indexes for specific subsets of data.
```bash
db.teachers.createIndex({age: 1}, {partialFilterExpression: {age: {$gte: 22}}});
```
- This index applies only to documents where `age` is greater than or equal to 22.

---

### **3. Covered Query**

A **covered query** is a query where all the fields are part of the same index. MongoDB can retrieve the data directly from the index without fetching the actual documents, which is faster.

#### Example:
```bash
db.collectionName.find({name: "alex"}, {_id: 0, name: 1});
```
- If `name` is indexed, this query will retrieve the data directly from the index, resulting in a fast execution.

---

### **Multiple Index Selection**

When a query could use multiple indexes, MongoDB performs **performance analysis** before execution to determine the most efficient index to use. This result is cached, but the cache is reset after:
- 1000 writes.
- MongoDB restart.
- Index modification.

---

### **4. Text Index**

A **text index** is used for **full-text search**, allowing you to search for documents based on keywords, similar to a search engine. You can only create one text index per collection.

#### Example:
```bash
db.collectionName.createIndex({bio: "text"});
```
- Creates a text index on the `bio` field.

```bash
db.collectionName.createIndex({name: 'text', bio: 'text'});
```
- Creates a text index on both the `name` and `bio` fields.

```bash
db.collectionName.find({$text: {$search: "experience"}});
```
- Searches the `bio` field for the keyword "experience".

#### Text Index Features:
- **Stop Words**: MongoDB removes common words (like "and", "the", etc.), and applies **stemming**, which reduces words to their root form (e.g., "walking" → "walk").
- **Relevance Score**: Text searches return documents based on their relevance to the search term, with higher-matching documents appearing first.

#### Excluding Keywords:
```bash
db.collectionName.find({$text: {$search: "experience -manage"}});
```
- This query searches for documents containing "experience" but excludes those with the word "manage".

#### Creating Index in the Background:
```bash
db.collectionName.createIndex({name: "text"}, {background: true});
```
- Creating a text index locks the collection, preventing other queries from running until the index is created. Using the `background: true` option avoids locking the collection but delays text-based queries until the index is fully built.

---

## Aggregation Pipeline:
The aggregation pipeline in MongoDB works similarly to Unix pipelines, where the output of one operation is fed as input to the next operation. This allows for complex data transformation and analysis in a flexible manner.

#### Syntax:
```js
db.collection.aggregate(pipeline, options)
```

### Example Queries:

1. **Simple Match:**
   To filter documents where `gender` is "Male":
   ```js
   db.emp.aggregate([{$match: {gender: "Male"}}])
   ```
   The `$match` stage filters documents based on specified conditions.

2. **Group by Age:**
   To group documents by the `age` field:
   ```js
   db.emp.aggregate([{$group: {_id:"$age"}}])
   ```
   This groups the documents by `age`, returning unique values of `age` with `_id` being the group identifier.

3. **Push Data into Groups:**
   To group by `age` and push the employee names into the groups:
   ```js
   db.emp.aggregate([{$group: {_id:"$age", name:{$push: "$name"}}}])
   ```
   This results in an array of names grouped by their age.

4. **Push Full Documents into Groups:**
   Using `$$ROOT` to push the entire document into the group:
   ```js
   db.emp.aggregate([{$group: {_id:"$age", name:{$push: "$$ROOT"}}}])
   ```
   Here, `$$ROOT` refers to the entire document being grouped, not just a single field.

5. **Count Per Age Group for Male Employees:**
   To count the number of male employees in each age group:
   ```js
   db.emp.aggregate([
      {$match:{gender: "Male"}},
      {$group:{_id:"$age", countOfEmpAgeGroup:{$sum:1}}}
   ])
   ```
   `$sum: 1` adds 1 for each document in the group, providing the count.

6. **Sorting by Count in Descending Order:**
   To count male employees by age group and sort them by count:
   ```js
   db.emp.aggregate([
      {$match:{gender: "Male"}},
      {$group:{_id:"$age", countOfEmpAgeGroup:{$sum:1}}},
      {$sort: {countOfEmpAgeGroup: -1}}
   ])
   ```

### $filter:
MongoDB also provides the `$filter` stage for more complex conditions inside pipelines. This stage allows you to apply custom filtering to arrays within documents.

---
## $bucket
The `$bucket` operator in MongoDB is used to categorize documents into different groups based on specified boundaries. It is especially useful when you want to divide documents into ranges or "buckets" of data, based on numerical fields.

### When to Use `$bucket`:
You use the `$bucket` operator when you want to create discrete groups (or buckets) based on the values of a field. For example, you might want to group students by age ranges, sales by price ranges, or products by ratings.

### Example:

#### Task: 
You want to group students by age:
- Group 1: Ages 20 to 30.
- Group 2: Ages 30 to 40.
- Group 3: Ages 40 and above.

Here’s how you can do it using the `$bucket` operator.

### Basic Example:

```js
db.emp.aggregate([
  { $match: { gender: "Female" } }, 
  { 
    $bucket: {
      groupBy: "$age", // Field to group by
      boundaries: [0, 30, 40], // Define the boundaries for grouping
      default: "greater than 40 group", // Name for values outside boundaries
      output: { count: { $sum: 1 } } // Count number of documents in each bucket
    } 
  }
])
```

#### Explanation:
- `groupBy: "$age"`: We are grouping by the `age` field.
- `boundaries: [0, 30, 40]`: This creates two main groups:
  - One for ages 0 to 30.
  - Another for ages 30 to 40.
- `default: "greater than 40 group"`: This is the bucket for ages greater than 40.
- `output: { count: { $sum: 1 } }`: We are calculating the count of students in each bucket.

#### Output:
```json
[
  { "_id": 0, "count": 2 },  // 2 students between ages 0-30
  { "_id": 30, "count": 1 }  // 1 student between ages 30-40
]
```

### Example with Student Names:

```js
db.emp.aggregate([
  { $match: { gender: "Female" } },
  { 
    $bucket: {
      groupBy: "$age",
      boundaries: [0, 30, 40],
      default: "greater than 40 group",
      output: { 
        count: { $sum: 1 }, // Count of students in each group
        name: { $push: "$name" } // Push names into each group
      }
    }
  }
])
```

#### Explanation:
In addition to counting the students in each age group, this query also pushes the `name` field into each bucket, so we can see which students belong to each age range.

#### Output:
```json
[
  { "_id": 0, "count": 2, "name": [ "Emma Johnson", "Olivia Brown" ] },
  { "_id": 30, "count": 1, "name": [ "Sophia Rodriguez" ] }
]
```

### Key Points:
- **`groupBy`**: Field by which documents are categorized.
- **`boundaries`**: Specify the boundaries for bucket ranges.
- **`default`**: Catches values outside the specified boundary ranges.
- **`output`**: Define what fields to include in the result (e.g., counts, lists, etc.).

The `$bucket` operator helps you categorize and analyze documents based on value ranges, making it a useful tool for data analysis and reporting.

---
# $lookup
The `$lookup` operator in MongoDB is used to perform a left outer join between two collections, similar to SQL joins. It allows you to bring together related data from different collections by specifying the fields from both collections that should match.

### Steps to Use `$lookup` in MongoDB:

1. **Source Collection**: The collection where the `$lookup` operation is initiated (e.g., `customers`).
2. **Foreign Collection**: The collection to be joined (e.g., `orders`).
3. **Fields to Match**: Specify the field in both collections that should match.
4. **Output Field**: The results of the join are stored in an array within the source collection document.

### Example: Joining `customers` and `orders`

#### 1. Insert Customers:

```js
db.customers.insertMany([
  { _id: 1, name: "John Smith", age: 30, gender: "Male", email: "john.smith@example.com" },
  { _id: 2, name: "Emma Johnson", age: 28, gender: "Female", email: "emma.johnson@example.com" },
  { _id: 3, name: "Alex Patel", age: 35, gender: "Non-binary", email: "alex.patel@example.com" }
]);
```

#### 2. Insert Orders:

```js
db.orders.insertMany([
  { _id: 101, customer_id: 1, product: "Laptop", quantity: 1, price: 1200 },
  { _id: 102, customer_id: 1, product: "Smartphone", quantity: 2, price: 800 },
  { _id: 103, customer_id: 2, product: "Headphones", quantity: 1, price: 150 },
  { _id: 104, customer_id: 3, product: "Monitor", quantity: 1, price: 300 }
]);
```

#### 3. Perform the `$lookup`:

```js
db.customers.aggregate([
  {
    $lookup: {
      from: "orders",            // Collection to join
      localField: "_id",          // Field from 'customers'
      foreignField: "customer_id", // Field from 'orders'
      as: "order_details"         // Field to store the joined documents
    }
  }
]).pretty();
```

### Example Output:

```json
[
  {
    "_id": 1,
    "name": "John Smith",
    "age": 30,
    "gender": "Male",
    "email": "john.smith@example.com",
    "order_details": [
      {
        "_id": 101,
        "customer_id": 1,
        "product": "Laptop",
        "quantity": 1,
        "price": 1200
      },
      {
        "_id": 102,
        "customer_id": 1,
        "product": "Smartphone",
        "quantity": 2,
        "price": 800
      }
    ]
  },
  {
    "_id": 2,
    "name": "Emma Johnson",
    "age": 28,
    "gender": "Female",
    "email": "emma.johnson@example.com",
    "order_details": [
      {
        "_id": 103,
        "customer_id": 2,
        "product": "Headphones",
        "quantity": 1,
        "price": 150
      }
    ]
  },
  {
    "_id": 3,
    "name": "Alex Patel",
    "age": 35,
    "gender": "Non-binary",
    "email": "alex.patel@example.com",
    "order_details": [
      {
        "_id": 104,
        "customer_id": 3,
        "product": "Monitor",
        "quantity": 1,
        "price": 300
      }
    ]
  }
]
```

### Explanation:
- **`localField`**: The field from the `customers` collection (`_id`).
- **`foreignField`**: The field from the `orders` collection (`customer_id`).
- **`as`**: The result of the join is stored as an array called `order_details`.

This join will show each customer along with their respective orders in the `order_details` field. If a customer does not have any orders, the `order_details` array will be empty, reflecting the nature of a **left outer join**.
---
## $project
The `$project` stage in MongoDB aggregation allows you to reshape documents by including or excluding specific fields, creating computed fields, and renaming fields to customize the output of your aggregation query.

### Syntax and Usage

- **Include/Exclude Fields**: Specify `1` to include a field and `0` to exclude it.
- **Computed Fields**: Use expressions to perform calculations or transformations on existing fields.
- **Rename Fields**: Rename a field by assigning it a new name in the output.

### Examples

#### 1. Including Only the `name` Field:

```javascript
db.customers.aggregate([
  { $project: { name: 1, _id: 0 } }
]);
```

**Output**:

```json
[
  { "name": "John Smith" },
  { "name": "Emma Johnson" },
  { "name": "Alex Patel" }
]
```

Explanation: This includes only the `name` field and excludes the `_id` field.

#### 2. Projecting Fields with Different Names:

```javascript
db.customers.aggregate([
  { $project: { mail: "$email" } }
]);
```

**Output**:

```json
[
  { "_id": 1, "mail": "john.smith@example.com" },
  { "_id": 2, "mail": "emma.johnson@example.com" },
  { "_id": 3, "mail": "alex.patel@example.com" }
]
```

Explanation: This renames the `email` field to `mail` in the output.

#### 3. Using Arithmetic Expressions in Projection:

```javascript
db.customers.aggregate([
  { $project: { _id: 0, name: 1, age: { $multiply: [2, "$age"] } } }
]);
```

**Output**:

```json
[
  { "name": "John Smith", "age": 60 },
  { "name": "Emma Johnson", "age": 56 },
  { "name": "Alex Patel", "age": 70 }
]
```

Explanation: This doubles the `age` value for each document and includes only the `name` and computed `age` fields in the output.

---

## Capped Collection
In MongoDB, a **capped collection** is a special type of collection with a fixed size that works like a circular queue. Once the specified size limit is reached, the oldest documents are automatically removed as new documents are inserted, ensuring the collection does not exceed the defined size or maximum document count.

### Example:
```javascript
db.createCollection("myCappedCollection", { capped: true, size: 5000, max: 5 })
```
Here, `size: 5000` limits the collection's size in bytes, and `max: 5` restricts it to 5 documents.

### Insertion and Behavior:
When we insert a new document after reaching the cap (5 documents), MongoDB removes the oldest document automatically:

1. Initial state after inserting five documents:
   ```json
   [
     { "_id": 1, "message": "Message 1" },
     { "_id": 2, "message": "Message 2" },
     { "_id": 3, "message": "Message 3" },
     { "_id": 4, "message": "Message 4" },
     { "_id": 5, "message": "Message 5" }
   ]
   ```

2. After inserting a new document `{ "message": "Message 6" }`, the first document is removed:
   ```json
   [
     { "_id": 2, "message": "Message 2" },
     { "_id": 3, "message": "Message 3" },
     { "_id": 4, "message": "Message 4" },
     { "_id": 5, "message": "Message 5" },
     { "_id": 6, "message": "Message 6" }
   ]
   ```

This functionality is especially useful for logging, real-time data tracking, and applications where only the most recent records are needed.

---

## Replication & Sharding
### Replication
Replication in MongoDB involves creating multiple copies of data across different servers to increase data availability, enhance fault tolerance, and support disaster recovery. MongoDB uses **replica sets** to manage this process. A replica set contains multiple **nodes**:

- **Primary Node**: The main server that handles all write operations.
- **Secondary Nodes**: Servers that replicate the data from the primary node. They are available to handle read operations and serve as backups.

If the primary node fails, MongoDB initiates an **election** to promote a secondary node to primary, ensuring **automatic failover** and maintaining database availability without downtime.

#### Why Replication?
1. **Data Safety**: Multiple copies safeguard against data loss.
2. **24/7 Availability**: Redundant servers provide uninterrupted data access.
3. **Disaster Recovery**: Backup nodes enable quick recovery after hardware or service failures.
4. **Maintenance without Downtime**: Allows updates and maintenance activities like indexing and backup without interrupting the application.
5. **Read Scaling**: Additional copies enable faster read operations by distributing queries.

### How Replication Works in MongoDB
1. The **primary node** accepts all write operations.
2. **Secondary nodes** replicate the primary’s data to maintain an identical dataset.
3. If the primary node fails, an **election** occurs among secondary nodes to select a new primary, ensuring continuous availability.
4. When a failed primary node recovers, it rejoins as a secondary node.

#### Example of Replica Set Architecture:
A basic setup involves at least three nodes:
- **Primary Node**: Receives all write requests and maintains current data.
- **Two Secondary Nodes**: Replicate data from the primary for redundancy and disaster recovery.

### Sharding
**Sharding** is a method of distributing data across multiple servers to handle high traffic and large datasets. Instead of adding more hardware to a single server (vertical scaling), sharding **horizontally scales** by splitting data across multiple servers, or **shards**.

#### How Sharding Works
1. **Data Partitioning**: Sharding divides the data across multiple servers, each handling a portion of the overall dataset.
2. **Increased Storage and Throughput**: Each new shard increases both storage capacity and query-handling capability.
3. **Improved Performance**: By distributing data and query loads, sharding reduces the performance bottlenecks associated with single-server limits.

#### Benefits of Sharding:
- **Infinite Scalability**: In theory, data and traffic distribution can keep pace with demand as more shards are added.
- **Cost Efficiency**: Horizontal scaling through sharding is often more cost-effective than continually upgrading a single server.
- **Higher Throughput**: Queries and data updates are distributed across shards, enhancing performance and enabling the database to handle more simultaneous operations.

Sharding is ideal for large-scale applications requiring high read/write throughput and large data storage that surpasses the capacity of a single server. Together, **replication** and **sharding** enable MongoDB to maintain high availability, resilience, and scalability for demanding, data-intensive applications.

---