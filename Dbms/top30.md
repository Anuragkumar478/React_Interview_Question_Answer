# 📚 DBMS Interview Questions & Answers

Top **30 DBMS interview questions** with short, interview-ready answers for fresher/software developer interviews.

---

## 1. What is DBMS?

**Answer:**

DBMS stands for **Database Management System**. It is software used to create, store, retrieve, update, and manage data in a database.

**Examples:**

* MySQL
* PostgreSQL
* Oracle
* SQL Server

---

## 2. What is the difference between DBMS and RDBMS?

| DBMS                                       | RDBMS                                 |
| ------------------------------------------ | ------------------------------------- |
| General database management system         | Relational database management system |
| May not organize data using related tables | Stores data in tables                 |
| Relationships may not be enforced          | Supports relationships using keys     |
| Example depends on the model               | MySQL, PostgreSQL, Oracle             |

**Interview Answer:**

> DBMS is a general system for managing databases, while RDBMS specifically follows the relational model and stores data in related tables.

---

## 3. What is a Database?

A **database** is an organized collection of data that can be easily stored, accessed, updated, and managed.

Example:

```text
Users
-------------------------
id | name   | age
-------------------------
1  | Anurag | 22
2  | Rahul  | 23
```

---

## 4. What is a Table?

A **table** stores data in the form of **rows and columns**.

Example:

```text
Students
-------------------------
id | name   | age
-------------------------
1  | Anurag | 22
2  | Rahul  | 21
```

* **Row** → Record
* **Column** → Attribute

---

## 5. What is a Primary Key?

A **primary key** uniquely identifies every record in a table.

Example:

```sql
CREATE TABLE users (
    id INT PRIMARY KEY,
    name VARCHAR(50)
);
```

### Properties:

* Unique
* Cannot contain `NULL`
* A table has one primary-key constraint

---

## 6. What is a Foreign Key?

A **foreign key** is a column that references a key in another table.

Example:

```sql
CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    user_id INT,
    FOREIGN KEY (user_id) REFERENCES users(id)
);
```

Here, `user_id` creates a relationship between `orders` and `users`.

---

## 7. What is a Candidate Key?

A **candidate key** is a column or combination of columns that can uniquely identify a record.

Example:

```text
Users
-------------------------
id
email
phone
```

If `id`, `email`, and `phone` are all unique, each can potentially be a candidate key.

One candidate key is selected as the **primary key**.

---

## 8. What is a Super Key?

A **super key** is any set of one or more attributes that can uniquely identify a record.

Example:

```text
id
```

can be a super key.

Also:

```text
id + name
```

can be a super key if `id` is already unique.

### Difference:

> Every candidate key is a super key, but every super key is not necessarily a candidate key.

---

## 9. What is Normalization?

**Normalization** is the process of organizing data into tables to:

* Reduce data redundancy
* Improve data consistency
* Avoid insertion, deletion, and update anomalies

Common normal forms:

```text
1NF
2NF
3NF
BCNF
```

---

## 10. What is 1NF?

**1NF (First Normal Form)** means:

* Every column contains atomic/single values.
* There are no repeating groups.

### Bad:

```text
id | name   | phone
-------------------------
1  | Anurag | 9999, 8888
```

### Better:

```text
id | name   | phone
-------------------------
1  | Anurag | 9999
1  | Anurag | 8888
```

---

## 11. What is 2NF?

A table is in **2NF** when:

1. It is already in 1NF.
2. There is no **partial dependency** on a part of a composite candidate key.

### Simple meaning:

A non-key attribute should depend on the **whole composite key**, not just a part of it.

---

## 12. What is 3NF?

A table is in **3NF** when:

1. It is in 2NF.
2. It has no **transitive dependency**.

Example:

```text
Student_ID → Department_ID → Department_Name
```

Here `Department_Name` depends indirectly on `Student_ID`.

This can be separated into different tables.

---

## 13. What is Denormalization?

**Denormalization** means intentionally adding some redundant data to improve read performance.

### Example:

Instead of performing multiple joins:

```text
Users
Orders
Addresses
```

some frequently accessed information can be stored directly with the order.

### Advantage:

Faster reads.

### Disadvantage:

More storage and possible data consistency problems.

---

## 14. What is SQL?

**SQL (Structured Query Language)** is used to communicate with relational databases.

Example:

```sql
SELECT * FROM users;
```

SQL commands are commonly categorized as:

* DDL
* DML
* DQL
* DCL
* TCL

---

## 15. What is DDL?

**DDL = Data Definition Language**

It is used to define or modify database structure.

### Commands:

```sql
CREATE
ALTER
DROP
TRUNCATE
```

Example:

```sql
CREATE TABLE users (
    id INT,
    name VARCHAR(50)
);
```

---

## 16. What is DML?

**DML = Data Manipulation Language**

It is used to modify data stored in tables.

### Commands:

```sql
INSERT
UPDATE
DELETE
```

Example:

```sql
INSERT INTO users VALUES (1, 'Anurag');
```

---

## 17. What is DQL?

**DQL = Data Query Language**

It is used to retrieve data.

Main command:

```sql
SELECT
```

Example:

```sql
SELECT * FROM users;
```

---

## 18. What is DCL?

**DCL = Data Control Language**

It is used to control database permissions.

Main commands:

```sql
GRANT
REVOKE
```

Example:

```sql
GRANT SELECT ON users TO developer;
```

---

## 19. What is TCL?

**TCL = Transaction Control Language**

It manages database transactions.

Main commands:

```sql
COMMIT
ROLLBACK
SAVEPOINT
```

Example:

```sql
BEGIN;

UPDATE users
SET age = 23
WHERE id = 1;

COMMIT;
```

---

## 20. What is a Transaction?

A **transaction** is a sequence of database operations treated as a single logical unit of work.

Example:

```text
Transfer ₹1000

1. Deduct ₹1000 from Account A
2. Add ₹1000 to Account B
```

Both operations should succeed together.

---

# 🔥 ACID Properties

## 21. What are ACID Properties?

ACID properties ensure reliable database transactions.

### A — Atomicity

Either **all operations succeed or none of them do**.

### C — Consistency

The database moves from one valid state to another valid state.

### I — Isolation

Concurrent transactions should not incorrectly interfere with each other.

### D — Durability

Once a transaction is committed, its changes should persist even after a failure.

### Easy Trick:

```text
A → All or Nothing
C → Correct State
I → Independent Transactions
D → Data Persists
```

---

## 22. What is a JOIN?

A **JOIN** combines rows from two or more tables based on a related column.

Example:

```sql
SELECT users.name, orders.order_id
FROM users
JOIN orders
ON users.id = orders.user_id;
```

Common JOIN types:

```text
INNER JOIN
LEFT JOIN
RIGHT JOIN
FULL OUTER JOIN
CROSS JOIN
SELF JOIN
```

---

## 23. What is INNER JOIN?

`INNER JOIN` returns only the records that have matching values in both tables.

Example:

```sql
SELECT users.name, orders.order_id
FROM users
INNER JOIN orders
ON users.id = orders.user_id;
```

### Simple idea:

```text
Table A ∩ Table B
```

Only matching records are returned.

---

## 24. What is LEFT JOIN?

`LEFT JOIN` returns:

* All records from the left table
* Matching records from the right table
* `NULL` when there is no match

Example:

```sql
SELECT users.name, orders.order_id
FROM users
LEFT JOIN orders
ON users.id = orders.user_id;
```

This can be used to find users who **have or don't have orders**.

---

## 25. What is the difference between DELETE, TRUNCATE, and DROP?

| Command    | Purpose                  |
| ---------- | ------------------------ |
| `DELETE`   | Removes rows             |
| `TRUNCATE` | Removes all rows         |
| `DROP`     | Removes the entire table |

### DELETE

```sql
DELETE FROM users
WHERE id = 5;
```

Can remove selected rows using `WHERE`.

### TRUNCATE

```sql
TRUNCATE TABLE users;
```

Removes all rows while keeping the table structure.

### DROP

```sql
DROP TABLE users;
```

Removes the table itself.

---

## 26. What is an Index?

An **index** is a data structure that helps the database find rows faster.

Example:

```sql
CREATE INDEX idx_users_email
ON users(email);
```

Without an appropriate index, the database may need to scan many rows.

### Advantage:

Faster reads/searches.

### Disadvantage:

* Requires additional storage
* Can make `INSERT`, `UPDATE`, and `DELETE` more expensive

---

## 27. What is a View?

A **view** is a virtual table based on a SQL query.

Example:

```sql
CREATE VIEW active_users AS
SELECT id, name
FROM users
WHERE status = 'active';
```

Then:

```sql
SELECT * FROM active_users;
```

A view generally stores the query definition rather than a separate copy of the underlying data.

---

## 28. What is a Stored Procedure?

A **stored procedure** is a set of SQL statements stored in the database and executed when called.

Example:

```sql
CREATE PROCEDURE getUsers()
BEGIN
    SELECT * FROM users;
END;
```

It can be useful for reusable database-side operations.

---

## 29. What is a Deadlock?

A **deadlock** occurs when two or more transactions wait for each other indefinitely.

Example:

```text
Transaction A locks Resource 1
        ↓
waits for Resource 2

Transaction B locks Resource 2
        ↓
waits for Resource 1
```

```text
A → waiting for B
B → waiting for A
```

The database needs a mechanism to detect and resolve such situations, often by aborting/rolling back one transaction.

---

## 30. What is the difference between SQL and NoSQL?

| SQL                            | NoSQL                                               |
| ------------------------------ | --------------------------------------------------- |
| Relational                     | Non-relational                                      |
| Usually table-based            | Document/key-value/column/graph models              |
| Schema is typically structured | Often supports flexible schemas                     |
| Uses SQL                       | Query method depends on database                    |
| Strong relational capabilities | Designed for different scalability/data-model needs |
| MySQL, PostgreSQL              | MongoDB, Redis, Cassandra                           |

### Example:

SQL:

```text
Users Table
------------------
id | name | age
```

MongoDB:

```javascript
{
    "_id": 1,
    "name": "Anurag",
    "age": 22
}
```

---

# ⭐ Bonus: MongoDB Interview Questions

Since MERN interviews often include MongoDB, also prepare these:

### Find one user

```javascript
db.users.findOne({
    age: { $gt: 22 }
});
```

### Find all users

```javascript
db.users.find();
```

### Find users whose age is greater than 22

```javascript
db.users.find({
    age: { $gt: 22 }
});
```

### Find users whose age is between 20 and 25

```javascript
db.users.find({
    age: {
        $gte: 20,
        $lte: 25
    }
});
```

### Update a user

```javascript
db.users.updateOne(
    { name: "Anurag" },
    { $set: { age: 23 } }
);
```

### Delete a user

```javascript
db.users.deleteOne({
    name: "Anurag"
});
```

---

# 🎯 Quick Revision

Before your interview, make sure you can explain these without looking at notes:

```text
1. DBMS vs RDBMS
2. Primary Key
3. Foreign Key
4. Candidate Key
5. Super Key
6. Normalization
7. 1NF, 2NF, 3NF
8. Joins
9. Indexing
10. Transactions
11. ACID
12. DELETE vs TRUNCATE vs DROP
13. SQL vs NoSQL
14. Deadlock
15. Views
16. Stored Procedures
17. MongoDB queries
```

> **Interview tip:** For every DBMS concept, try to give **definition + simple example + one advantage/disadvantage**. This makes your answer much stronger than giving only a definition.
