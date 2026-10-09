# MongoDB Basics and Library System Use Case

## 1. What is MongoDB?

MongoDB is a NoSQL, document-oriented database. Instead of storing data in rows and columns like a SQL database, it stores data as flexible, JSON-like documents (internally BSON). This makes it easy to store data whose structure changes over time.

## 2. Key Concepts

| Concept | Meaning | SQL comparison |
|---|---|---|
| Database | A container for collections (e.g. `studentDB`) | Database |
| Collection | A group of documents (e.g. `students`) | Table |
| Document | One record, written as key-value pairs | Row |
| Field | A key-value pair inside a document (e.g. `name: "Arun"`) | Column |
| `_id` | A unique ID MongoDB adds to every document automatically | Primary key |

Sample document:

```js
{ name: "Arun", age: 21, course: "MERN Stack", status: "active", email: "arun@example.com" }
```

## 3. Setup Done

1. Installed MongoDB Community Server and MongoDB Compass on Windows.
2. Started the MongoDB service (`net start MongoDB`).
3. Connected with `mongosh` and used the `studentDB` and `libraryDB` databases.

## 4. CRUD Operations (studentDB.students)

| Operation | Command | Purpose |
|---|---|---|
| Create database/collection | `use studentDB`, `db.createCollection("students")` | Set up storage |
| Insert one | `db.students.insertOne({...})` | Add one document |
| Insert many | `db.students.insertMany([{...}, {...}])` | Add several documents |
| Read all | `db.students.find()` | Fetch every document |
| Read with filter | `db.students.find({ course: "MERN Stack" })` | Fetch matching documents |
| Update one | `db.students.updateOne({ name: "Arun" }, { $set: { status: "completed" } })` | Change one document |
| Update many | `db.students.updateMany({ course: "Python" }, { $set: { status: "completed" } })` | Change all matches |
| Delete one | `db.students.deleteOne({ name: "Suresh" })` | Remove one document |
| Delete all | `db.students.deleteMany({})` | Empty the collection (practice only) |

## 5. Query Operators

| Operator | Meaning | Example |
|---|---|---|
| `$gt` | Greater than | `db.students.find({ age: { $gt: 20 } })` |
| `$lt` | Less than | `db.students.find({ age: { $lt: 23 } })` |
| `$in` | Matches any value in a list | `db.students.find({ course: { $in: ["Python", "Java"] } })` |
| `$and` | All conditions must be true | `db.students.find({ $and: [{ course: "MERN Stack" }, { status: "active" }] })` |
| `$or` | At least one condition is true | `db.students.find({ $or: [{ course: "Java" }, { age: { $gt: 22 } }] })` |
| `$exists` | Field is present (or missing) | `db.students.find({ email: { $exists: true } })` |

## 6. Real-World Use Case: Library System

A library needs to store books, search them, track how many copies are left, and remove lost books. Database: `libraryDB`, collection: `books`.

Sample document:

```js
{ title: "Clean Code", author: "Robert C. Martin", category: "Programming", copies: 3, available: true }
```

| Task | Command |
|---|---|
| Add books | `db.books.insertMany([...])` |
| Search by category | `db.books.find({ category: "Programming" })` |
| Show available books | `db.books.find({ available: true })` |
| Search by title text | `db.books.find({ title: { $regex: "habits", $options: "i" } })` |
| Borrow a book | `db.books.updateOne({ title: "Clean Code" }, { $inc: { copies: -1 } })` |
| Return a book | `db.books.updateOne({ title: "Atomic Habits" }, { $inc: { copies: 1 }, $set: { available: true } })` |
| Remove a lost book | `db.books.deleteOne({ title: "Ponniyin Selvan" })` |

`$inc` increases or decreases a number, which suits tracking copies when books are borrowed and returned.

## 7. Why MongoDB?

- **Flexible schema:** documents in one collection can have different fields (only Arun had an `email`).
- **Fast development:** data looks like JSON, the same format JavaScript uses.
- **Scalable:** handles large and growing data well.
- **MERN friendly:** works naturally with Node.js, Express and React.

## 8. Screenshots

Add your screenshots in a `screenshots` folder and link them here:

![Insert operations](screenshots/insert.png)
![Read and filter](screenshots/read.png)
![Update operations](screenshots/update.png)
![Query operators](screenshots/operators.png)
![Delete operations](screenshots/delete.png)
![Library system](screenshots/library.png)

## 9. Conclusion

I practised creating a database and collection, and performing insert, read, update and delete operations. I used the operators `$gt`, `$lt`, `$in`, `$and`, `$or` and `$exists`, and applied everything in a Library System. MongoDB's document model makes storing and searching data simple and flexible.