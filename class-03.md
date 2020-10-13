# Data Modeling & NoSQL Databases

## Review, Research, and Discussion

1. Name 3 advantages to Test Driven Development.

[Article About TDD](https://www.codica.com/blog/test-driven-development-benefits/)

- Reducing time for coding since all the errors were predicted before event start with coding.

- Increase the code flexibility for maintenance in the long term.

- Help Build a detailed documentation for the entire project

2. In what case would you need to use beforeEach() or afterEach() in a test suite?

- beforeEach() is run before each test in the description and used to map the data before sending it to the test.

- afterEach() is run after each test in a descriptive and used to clean up stuff like a close opened file.

3. What is one downside of Test Driven Development?

[Article About TDD](https://leantesting.com/test-driven-development/)

- it costs a lot of time and effort up front.

- Focusing on the simplest design now and not thinking ahead can mean major refactoring requirements.

- It may cause over coding, since it is very difficult to write good test that cover essential.

4. What’s the primary difference between ES6 Classes and Constructor/Prototype Classes?

- Classes can extend more types than constructors can (like functions and arrays)

- Non-classes can’t extend classes ,because they can’t call the parent constructor

- Classes are much cleaner and easier to code and refactor in the future.

5. Name a use case for a static method

static methods can be called form the class name itself, without the need to inherits an object from that class,

for Example : If you want to get the number of objects that was created form this class, you can create a static variable/method which each time a new object is created it will be increased

6. Write an example of a Higher Order function and describe the use case it solves.

All Arrays functions are high order function, Arrays.prototype.map() => this method will return another array without effecting the original array.

## Document the following Vocabulary Terms

1. **functional programming** : is the process of building software by composing pure functions, avoiding shared state, mutable data, and side-effects

1. **Pure Function** : is a function which given tha same input, will always return tha same output, and produces no side effects.
1. **High Order Functions** : Functions that operate on other functions, either by taking them as arguments or by returning them
1. **Immutable State** : It's a term in OOP which means it can't be modified after creating.
1. **Object** : It's is a data type created by a developer, it can include multiple properties and methods and may even contain other objects as well
1. **Object-oriented programming (OOP)** : is a programming paradigm based on the concept of objects rather than functions and login, which can contain data and code (properties/methods) Java is consider a OOP language
1. **Class** : is an extensible program-code-template for creating objects, providing initial values, in OOP it is the basic building blocks.
1. **Prototype** : A type of object, which connect functions/method to constructors, and all these methods are inherited to all the created instances from that constructor
1. **Super** : keyword used in classes, represent the parent class which was extended by another class.
1. **Inheritance** : is the mechanism of basing an object or class upon another object (prototype-based inheritance) or class (class-based inheritance), retaining similar implementation, an inherited class called a subclass of its parent class of super class
1. **Constructor** : A method for class for creating and initializing an objects from a class.
1. **Instance** : An Object that was created from a class
1. **Context** : basically a structure or instance or object that contains minimal set of attributes or properties or states that allows to execute or manage defined set of operations or tasks.
1. **this** : a keyword in OOP refers to the same object that was created, or that class properties
1. **Test Driven Development (TDD)** : is a development technique where you must first write a test that fails before you write new functional code
1. **jest** : is a JavaScript testing framework designed to ensure correctness of any JavaScript codebase
1. **Continuos Integrating** : is a development practice where developers integrate code into a shared repository frequently, preferably several times a day. Each integration can then be verified by an automated build and automated tests. While automated testing is not strictly part of CI it is typically implied.
1. **Unit Test** : is a type of software testing where individual units or components of a software are tested. The purpose is to validate that each unit of the software code performs as expected. Unit Testing is done during the development (coding phase) of an application by the developers

---

## Preparation Materials

### nosql Vs sql

|                                   SQL                                    |                                                  noSQL                                                  |
| :----------------------------------------------------------------------: | :-----------------------------------------------------------------------------------------------------: |
|                      Called as Relational Databases                      |                                as non-relational or distributed database                                |
|                          table based databases                           |                                     document based, key-value pairs                                     |
|                          have predefined schema                          |                                  dynamic schema for unstructured data.                                  |
|                           vertically scalable                            |                                          horizontally scalable                                          |
|                  uses SQL ( structured query language )                  |                                 uses UnQL (Unstructured Query Language)                                 |
|         are good fit for the complex query intensive environment         |                                  are not good fit for complex queries                                   |
| increasing load by increasing the CPU, RAM, SSD, etc, on a single server | can just add few more servers easily in your NoSQL database infrastructure to handle the large traffic. |
| increasing load by increasing the CPU, RAM, SSD, etc, on a single server | can just add few more servers easily in your NoSQL database infrastructure to handle the large traffic. |

---

## NoSQL Data Modeling Techniques

This section is devoted to the basic principles of NoSQL data modeling.

1. Denormalization.

defined as the copying of the same data into multiple documents or tables in order to simplify/optimize query processing or to fit the user’s data into a particular data model

2. Aggregates.

3. Application Side Joins.

joins are often handled at design time as opposed to relational models where joins are handled at query execution time. Query time joins almost always mean a performance penalty, but in many cases one can avoid joins using Denormalization and Aggregates, i.e. embedding nested entities.

4. Atomic Aggregates

NoSQL solutions have limited transaction support. In some cases one can achieve transactional behavior using distributed locks or application-managed MVCC, but it is common to model data using an Aggregates technique to guarantee some of the ACID properties.

5. Enumerable Keys

6. Dimensionality Reduction

Dimensionality Reduction is a technique that allows one to map multidimensional data to a Key-Value model or to other non-multidimensional models.

7. Index Table

Index Table is a very straightforward technique that allows one to take advantage of indexes in stores that do not support indexes internally

8. Composite Key Index

Composite key is a very generic technique, but it is extremely beneficial when a store with ordered keys is used. Composite keys in conjunction with secondary sorting allows one to build a kind of multidimensional index which is fundamentally similar to the previously described Dimensionality Reduction technique.

9. Aggregation with Composite Keys.

Composite keys may be used not only for indexing, but for different types of grouping.

10. Inverted Search – Direct Aggregation

This technique is more a data processing pattern, rather than data modeling. Nevertheless, data models are also impacted by usage of this pattern

11. Tree Aggregation

Trees or even arbitrary graphs (with the aid of denormalization) can be modeled as a single record or document.

12. Adjacency Lists

Adjacency Lists are a straightforward way of graph modeling – each node is modeled as an independent record that contains arrays of direct ancestors or descendants.

13. Materialized Paths

Materialized Paths is a technique that helps to avoid recursive traversals of tree-like structures. This technique can be considered as a kind of denormalization.

14. Nested Sets

Nested sets is a standard technique for modeling tree-like structures.

15. Nested Documents Flattening: Numbered Field Names

Search Engines typically work with flat documents, i.e. each document is a flat list of fields and values

16. Nested Documents Flattening: Proximity Queries

use proximity queries that limit the acceptable distance between words in the document

17. Batch Graph Processing

Graph databases like neo4j are exceptionally good for exploring the neighborhood of a given node or exploring relationships between two or a few nodes
