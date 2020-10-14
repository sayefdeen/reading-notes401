# Advanced Mongo/Mongoose

## Why would a developer choose to make data models?

There are many benefits for data models:

- Faster performance, a well-constructed database typically runs faster.

- Clearer scope, A data model provides a focus for determining scope

- Fewer application errors, A data model causes participants to crisply define concepts and resolve confusion

- Fewer data errors, Data errors are worse than application errors. It is one thing to have an application crash, necessitating a restart

## What purpose do CRUD operations serve?

CRUD stands for:

- C : Create
- R : Read
- U : Update
- D : Delete

It is a system that allows you to Create content,data,user Read these data, Update them and also delete them.

## What kind of database is Postgres? What kind of database is MongoDB?

- PostgreSQL : it is database depending in tables, relations, and uses SQL language (SQL DataBase)

- MongoSQL : it is database depending in objects (JSON) documents , considered as (NoSQL) database

## What is Mongoose and why do we need it?

Mongoose is an Object Data Modeling (ODM) library for MongoDB and Node.js.

It manages relationships between data, provides schema validation, and is used to translate between objects in code and the representation of those objects in MongoDB.

---

## Vocabulary Terms

1. **database** : it is a data structure that stores organized information, typically stored and accessed from a computer system.

2. **data model** : is an abstract model that organizes elements of data standardizes how they relate to one another and to the properties of real-world entities.

3. **CRUD** : Its create,read,update,delete which are the four basic functions or any storage system.

4. **schema** : is the skeleton structure that represent the logical view of the entire database, it defines how the data is organized and how the relations among them are associated.

5. **sanitize** : removing any illegal character from the data, used for security purposes.

6. **Structured Query Language (SQL)** : It is a language used in programming designed for managing data held in relational database management system

7. **Non SQL (NoSQL)** : a database that store data in a format other than relational tables such as (JSON Objects).

8. **MongoDB** : is a cross-platform document-oriented database program, classified as a NoSQL database program, uses JSON-like documents with optional schemas.

9. **Mongoose** : it is an Object Data Modeling (ODM) library for MongoDB and Node.js.

10. **record** : is an object that can contain one or more values, group of records are saved in a table, each record is saved in a row.

11. **document** : it is an object that contain on or more values, this term refer to NoSQl database

12. **Object Relation Mapping (ORM)** : is a programming technique for converting data between incompatible type systems using object-oriented programming languages

---

## Preparation Materials

### The Repository Design Pattern

#### What is Design Pattern

design pattern is a reusable solution to a general problem occurring in a given context in software design. A design pattern is not a design which is directly transferred into code(source or machine).

Repository pattern separates the data access logic and maps it to the business entities in the business logic. Communication between the data access logic and the business logic is done through interfaces.

To put it simply, Repository pattern is a kind of container where data access logic is stored. It hides the details of data access logic from business logic. In other words, we allow business logic to access the data object without having knowledge of underlying data access architecture.

In most situations we want to have the following operations:

- Get all records
- Get paginated set of records
- Create a new record
- Get record by it’s primary key
- Get record by some other attribute
- Update a record
- Delete a record

If we implement these operations for each object, you can imagine that the number of duplicate code in the entire application. For small application it doesn’t matter, but for larger applications it is a bad news.

---

### in-memory database testing

an in-memory MongoDB process to test your mongoose logic without having to create any mocks.

1. Setup & Install dependencies

```cmd
npm install mongoose
npm install -D jest mongodb-memory-server
```

2. Write code to test

- Product schema

```javascript
// src/models/product.js

const mongoose = require('mongoose');

/**
 * Product model schema.
 */
const productSchema = new mongoose.Schema({
  name: { type: String, required: true },
  price: { type: Number, required: true },
  description: { type: String },
});

module.exports = mongoose.model('product', productSchema);
```

- Product service

```javascript
// src/services/ product.js;

const productModel = require('../models/product');

/**
 * Stores a new product into the database.
 * @param {Object} product product object to create.
 * @throws {Error} If the product is not provided.
 */
module.exports.create = async (product) => {
  if (!product) throw new Error('Missing product');

  await productModel.create(product);
};
```

3. Configure jest

add these to package.json

```json
"scripts": {
    "test": "jest --runInBand ./test"
}
"jest": {
    "testEnvironment": "node"
}
```

4. In-memory database handling

module that executes some basic operations that are used to handle the in-memory database.

```javascript
// tests/db-handler.js

const mongoose = require('mongoose');
const { MongoMemoryServer } = require('mongodb-memory-server');

const mongod = new MongoMemoryServer();

/**
 * Connect to the in-memory database.
 */
module.exports.connect = async () => {
  const uri = await mongod.getConnectionString();

  const mongooseOpts = {
    useNewUrlParser: true,
    autoReconnect: true,
    reconnectTries: Number.MAX_VALUE,
    reconnectInterval: 1000,
  };

  await mongoose.connect(uri, mongooseOpts);
};

/**
 * Drop database, close the connection and stop mongod.
 */
module.exports.closeDatabase = async () => {
  await mongoose.connection.dropDatabase();
  await mongoose.connection.close();
  await mongod.stop();
};

/**
 * Remove all the data for all db collections.
 */
module.exports.clearDatabase = async () => {
  const collections = mongoose.connection.collections;

  for (const key in collections) {
    const collection = collections[key];
    await collection.deleteMany();
  }
};
```

5. writing tests

```javascript
// tests/product.test.js

const mongoose = require('mongoose');

const dbHandler = require('./db-handler');
const productService = require('../src/services/product');
const productModel = require('../src/models/product');

/**
 * Connect to a new in-memory database before running any tests.
 */
beforeAll(async () => await dbHandler.connect());

/**
 * Clear all test data after every test.
 */
afterEach(async () => await dbHandler.clearDatabase());

/**
 * Remove and close the db and server.
 */
afterAll(async () => await dbHandler.closeDatabase());

/**
 * Product test suite.
 */
describe('product ', () => {
  /**
   * Tests that a valid product can be created through the productService without throwing any errors.
   */
  it('can be created correctly', async () => {
    expect(
      async () => await productService.create(productComplete)
    ).not.toThrow();
  });
});

/**
 * Complete product example.
 */
const productComplete = {
  name: 'iPhone 11',
  price: 699,
  description:
    'A new dual‑camera system captures more of what you see and love. ',
};
```

<p style="color:red; font-size:25px">All This code is taken from <a href="https://dev.to/paulasantamaria/testing-node-js-mongoose-with-an-in-memory-database-32np"> this </a> article</p>

---

## MongoDB In-Memory Server

This package spins up an actual/real MongoDB server programmatically from node, for testing or mocking during development. By default it holds the data in memory. A fresh spun up mongod process takes about 7Mb of memory. The server will allow you to connect your favorite ODM or client library to the MongoDB server and run integration tests isolated from each other.

<p style="color:green; font-size:20px">Follow  <a href="https://dev.to/paulasantamaria/testing-node-js-mongoose-with-an-in-memory-database-32np"> this </a> link to know how to implement this package</p>
