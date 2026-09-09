# 🍃 Top 30 MongoDB Interview Questions & Answers

A collection of the **30 most important MongoDB interview questions with simple, interview-ready answers**, especially useful for **MERN Stack and Backend interviews**.

---

# 📌 MongoDB Basics

## 1. What is MongoDB?

**MongoDB** is a **NoSQL, document-oriented database** that stores data in flexible, JSON-like documents.

MongoDB internally stores documents in **BSON (Binary JSON)** format.

Example document:

```json
{
    "_id": 1,
    "name": "Anurag",
    "age": 22,
    "skills": ["Java", "React", "Node.js"]
}
```

### Key Features

* NoSQL database
* Document-oriented
* Flexible schema
* BSON format
* Horizontal scaling
* High availability
* Powerful aggregation framework

---

## 2. What is NoSQL?

**NoSQL** means databases that don't primarily use the traditional relational table-based model.

MongoDB is a **document database**.

Instead of:

```text
Database
 └── Tables
      └── Rows
```

MongoDB uses:

```text
Database
 └── Collections
      └── Documents
```

Example:

```json
{
    "name": "Anurag",
    "email": "anurag@example.com"
}
```

---

## 3. What is a Document in MongoDB?

A **document** is a record stored inside a MongoDB collection.

Example:

```json
{
    "_id": 101,
    "name": "Anurag",
    "age": 22,
    "city": "Varanasi"
}
```

A document is similar to a **row** in a relational database, but it can contain nested objects and arrays.

---

## 4. What is a Collection?

A **collection** is a group of MongoDB documents.

It is roughly similar to a **table** in SQL.

Example:

```text
Database
   |
   └── users
          |
          ├── document 1
          ├── document 2
          └── document 3
```

MongoDB does not require every document in a collection to have exactly the same fields.

---

## 5. Difference Between SQL and MongoDB?

| SQL                            | MongoDB                       |
| ------------------------------ | ----------------------------- |
| Relational database            | NoSQL document database       |
| Tables                         | Collections                   |
| Rows                           | Documents                     |
| Columns                        | Fields                        |
| JOIN                           | `$lookup`                     |
| SQL queries                    | MongoDB query/document syntax |
| Fixed/defined schema is common | Flexible schema               |

Example SQL:

```sql
SELECT * FROM users;
```

MongoDB:

```javascript
db.users.find();
```

---

## 6. What is BSON?

**BSON** stands for **Binary JSON**.

MongoDB stores documents in BSON rather than plain JSON.

BSON supports additional data types such as:

* Date
* Decimal128
* Binary data
* ObjectId
* 64-bit integers

Example:

```javascript
{
    name: "Anurag",
    createdAt: new Date()
}
```

---

## 7. What is `_id` in MongoDB?

`_id` is the unique identifier for a document within a collection.

Example:

```json
{
    "_id": ObjectId("..."),
    "name": "Anurag"
}
```

If you don't provide `_id`, MongoDB drivers normally generate an **ObjectId** automatically.

---

## 8. What is ObjectId?

`ObjectId` is a BSON type commonly used for MongoDB document IDs.

Example:

```javascript
ObjectId("507f1f77bcf86cd799439011")
```

An ObjectId contains information derived from its generation time along with other bytes, making it useful as a unique identifier.

You can create one in Node.js:

```javascript
const { ObjectId } = require("mongodb");

const id = new ObjectId();
```

---

# 🔍 MongoDB CRUD

## 9. What is CRUD?

CRUD stands for:

```text
C → Create
R → Read
U → Update
D → Delete
```

### Create

```javascript
db.users.insertOne({
    name: "Anurag",
    age: 22
});
```

### Read

```javascript
db.users.find();
```

### Update

```javascript
db.users.updateOne(
    { name: "Anurag" },
    { $set: { age: 23 } }
);
```

### Delete

```javascript
db.users.deleteOne({
    name: "Anurag"
});
```

---

## 10. Difference Between `find()` and `findOne()`?

### `find()`

Returns a cursor for matching documents.

```javascript
db.users.find({
    age: 22
});
```

It can return multiple documents.

### `findOne()`

Returns the first matching document.

```javascript
db.users.findOne({
    age: 22
});
```

### Interview Answer

> `find()` is used to retrieve multiple matching documents, while `findOne()` returns the first matching document.

---

## 11. Difference Between `insertOne()` and `insertMany()`?

### insertOne()

Inserts one document.

```javascript
db.users.insertOne({
    name: "Anurag"
});
```

### insertMany()

Inserts multiple documents.

```javascript
db.users.insertMany([
    { name: "Anurag" },
    { name: "Rahul" },
    { name: "Aman" }
]);
```

---

## 12. Difference Between `updateOne()` and `updateMany()`?

### updateOne()

Updates the first matching document.

```javascript
db.users.updateOne(
    { city: "Varanasi" },
    { $set: { city: "Delhi" } }
);
```

### updateMany()

Updates all matching documents.

```javascript
db.users.updateMany(
    { city: "Varanasi" },
    { $set: { city: "Delhi" } }
);
```

---

## 13. What is `$set`?

`$set` updates or creates a field without replacing the entire document.

Example:

```javascript
db.users.updateOne(
    { name: "Anurag" },
    {
        $set: {
            age: 22
        }
    }
);
```

Only the `age` field is modified.

---

## 14. What are MongoDB Query Operators?

Query operators allow us to perform conditions and comparisons.

Common operators:

```text
$eq
$ne
$gt
$gte
$lt
$lte
$in
$nin
$and
$or
$exists
```

Example:

```javascript
db.users.find({
    age: {
        $gte: 18
    }
});
```

This finds users whose age is at least 18.

---

# 📊 Indexing & Performance

## 15. What is an Index in MongoDB?

An index is a data structure that helps MongoDB find documents more efficiently.

Without an appropriate index, MongoDB may need to scan many documents.

Example:

```javascript
db.users.createIndex({
    email: 1
});
```

Here:

```text
1 → ascending
-1 → descending
```

### Benefit

Indexes can significantly improve query performance.

### Cost

Indexes also:

* Consume storage
* Add write/update overhead

---

## 16. What is a Compound Index?

A compound index contains multiple fields.

Example:

```javascript
db.users.createIndex({
    age: 1,
    city: 1
});
```

This can help queries that use these fields in ways supported by the index.

### Important

The **field order matters**.

MongoDB can efficiently use the index for the **prefix** of the indexed fields.

---

## 17. What is a Unique Index?

A unique index prevents duplicate values for the indexed key.

Example:

```javascript
db.users.createIndex(
    { email: 1 },
    { unique: true }
);
```

Now two documents cannot have the same indexed `email` value, subject to MongoDB's handling of missing/null values and index options.

### Common Use Cases

* Email
* Username
* Employee ID
* Product SKU

---

## 18. What is `explain()` in MongoDB?

`explain()` helps analyze how MongoDB executes a query.

Example:

```javascript
db.users
    .find({ email: "a@example.com" })
    .explain("executionStats");
```

It can provide information such as:

* Query plan
* Index usage
* Documents examined
* Keys examined
* Execution statistics

It is useful for finding slow queries.

---

# 🔄 Aggregation

## 19. What is Aggregation in MongoDB?

Aggregation processes documents and produces computed results.

It is commonly used for:

* Grouping
* Filtering
* Calculations
* Reporting
* Data transformation

Example:

```javascript
db.orders.aggregate([
    {
        $group: {
            _id: "$customerId",
            total: {
                $sum: "$amount"
            }
        }
    }
]);
```

This calculates the total order amount for each customer.

---

## 20. What is an Aggregation Pipeline?

An aggregation pipeline processes documents through a sequence of stages.

Example:

```javascript
db.orders.aggregate([
    {
        $match: {
            status: "completed"
        }
    },
    {
        $group: {
            _id: "$userId",
            total: {
                $sum: "$amount"
            }
        }
    }
]);
```

Pipeline:

```text
Documents
    ↓
$match
    ↓
$group
    ↓
Result
```

---

## 21. What is `$match`?

`$match` filters documents in an aggregation pipeline.

Example:

```javascript
db.users.aggregate([
    {
        $match: {
            age: {
                $gte: 18
            }
        }
    }
]);
```

It is similar to SQL's `WHERE`.

---

## 22. What is `$group`?

`$group` groups documents based on a specified expression.

Example:

```javascript
db.orders.aggregate([
    {
        $group: {
            _id: "$category",
            totalSales: {
                $sum: "$amount"
            }
        }
    }
]);
```

It is similar to SQL's `GROUP BY`.

---

## 23. What is `$lookup`?

`$lookup` performs a join-like operation between collections.

Example:

```javascript
db.orders.aggregate([
    {
        $lookup: {
            from: "users",
            localField: "userId",
            foreignField: "_id",
            as: "user"
        }
    }
]);
```

Conceptually:

```text
orders
   +
users
   ↓
combined result
```

### Interview Answer

> `$lookup` allows us to combine documents from another collection in an aggregation pipeline.

---

# 🏗️ Schema & Data Modeling

## 24. What is Schema Design in MongoDB?

Schema design means deciding how data should be structured and related in MongoDB.

Two common approaches are:

### Embedded Documents

```json
{
    "name": "Anurag",
    "address": {
        "city": "Varanasi",
        "state": "UP"
    }
}
```

### References

```json
{
    "name": "Anurag",
    "addressId": ObjectId("...")
}
```

The choice depends on how the application reads and writes the data.

---

## 25. What is Embedding vs Referencing?

### Embedding

Store related data inside the same document.

```json
{
    "name": "Anurag",
    "address": {
        "city": "Varanasi"
    }
}
```

### Referencing

Store a reference to another document.

```json
{
    "name": "Anurag",
    "addressId": ObjectId("...")
}
```

### When to Embed?

Use embedding when:

* Data is frequently accessed together
* Related data is relatively small
* The relationship is naturally contained within the parent

### When to Reference?

Use references when:

* Related data is large
* Data is shared by many documents
* The related data changes independently
* Embedding would create unbounded document growth

---

## 26. What is Mongoose?

**Mongoose** is an ODM (**Object Data Modeling**) library commonly used with MongoDB and Node.js.

It provides features such as:

* Schemas
* Models
* Validation
* Middleware
* Query helpers
* Population

Example:

```javascript
const mongoose = require("mongoose");

const userSchema = new mongoose.Schema({
    name: String,
    email: String,
    age: Number
});

const User = mongoose.model("User", userSchema);
```

---

## 27. Difference Between MongoDB and Mongoose?

### MongoDB

The actual **database system**.

### Mongoose

A **Node.js ODM library** that provides a higher-level way to work with MongoDB.

```text
Node.js
   ↓
Mongoose
   ↓
MongoDB
```

### Interview Answer

> MongoDB is the database, while Mongoose is a Node.js ODM used to model and interact with MongoDB.

---

# 🔐 Advanced MongoDB

## 28. What is a Transaction in MongoDB?

A transaction allows multiple database operations to be treated as one logical unit.

If the transaction commits:

```text
Operation 1 ✓
Operation 2 ✓
Operation 3 ✓
```

If it aborts:

```text
Operation 1 ✗
Operation 2 ✗
Operation 3 ✗
```

This is useful when multiple related operations must succeed or fail together.

Example use case:

```text
Transfer ₹100
    ↓
Decrease Account A
    ↓
Increase Account B
```

Both operations should be handled consistently.

---

## 29. What is Replication in MongoDB?

Replication maintains multiple copies of data across MongoDB nodes using a **replica set**.

A typical replica set contains:

```text
Primary
   ↓
Secondary
   ↓
Secondary
```

The primary handles writes, while secondaries replicate data from the primary.

### Benefits

* High availability
* Failover
* Data redundancy
* Read scaling in appropriate configurations

If the primary fails, an eligible secondary can be elected as the new primary.

---

## 30. What is Sharding in MongoDB?

**Sharding** is MongoDB's method of distributing data across multiple machines.

It is used for **horizontal scaling**.

Example:

```text
              Application
                   |
              MongoDB Cluster
             /       |       \
          Shard 1  Shard 2  Shard 3
```

Each shard stores a portion of the data.

### Why use Sharding?

* Handle very large datasets
* Scale storage
* Scale throughput
* Distribute workload across machines

---

# ⭐ Most Important MongoDB Questions for MERN Interviews

If you have limited preparation time, prioritize these:

```text
1. What is MongoDB?
2. MongoDB vs SQL
3. Document
4. Collection
5. BSON
6. ObjectId
7. CRUD
8. find() vs findOne()
9. Query operators
10. updateOne() vs updateMany()
11. $set
12. Indexing
13. Compound index
14. Unique index
15. explain()
16. Aggregation
17. Aggregation pipeline
18. $match
19. $group
20. $lookup
21. Embedding vs Referencing
22. Schema design
23. Mongoose
24. MongoDB vs Mongoose
25. Transactions
26. Replication
27. Replica set
28. Sharding
```

---

# 🎯 MongoDB Interview Strategy

For every MongoDB question, try to answer using this structure:

```text
1. Definition
2. Why it is used
3. Small example
4. Real-world use case
```

### Example

**Interviewer:** What is an Index?

**Good Answer:**

> An index is a data structure that helps MongoDB find documents more efficiently without scanning every document. For example, if I frequently search users by email, I can create an index on the email field. However, indexes consume storage and add some overhead to writes, so I wouldn't create indexes for every field.

This is much stronger than:

> "Index makes queries faster."

---

# 🚀 Recommended MERN Backend Preparation

After MongoDB, prepare these topics:

```text
HTML + CSS
      ↓
JavaScript
      ↓
React
      ↓
Node.js
      ↓
Express.js
      ↓
MongoDB
      ↓
Mongoose
      ↓
REST API
      ↓
JWT Authentication
      ↓
Redis
      ↓
Docker
      ↓
Git & GitHub
      ↓
DSA
```

**For a MERN interview, don't only learn MongoDB commands. Practice explaining how you used MongoDB/Mongoose in your own projects—schemas, relationships, indexes, aggregation, authentication data, and API queries.**
