# HTTP and REST

## Review, Research, and Discussion

1. Define three related pieces of data in a possible application.

Let's say that we have a company, which it contains a different types of departments, these department contains different types of teams, each team contain a specific type of specialized people working together to achieve a goal.

Company --> Departments --> Teams --> People

2. What is the advantage of an ORM, like Mongoose?

ORM (Object-Relation Mapping) : it helps take advantage of the object-oriented principles while managing relational databases, this allows you to set up objects and completely manage objects while the ORM library/framework takes care of translation all functionalities into database schema and queries.

3. How does the repository pattern compare with an ORM?

4. When making a repository/facade, what flexibility do you gain?

5. Name 3 cloud based NoSQL Databases

---

## Vocabulary Terms

- **lifecycle** : are the stages a computer program undergoes, from initial creating to deployment and execution, the phases are edit tme,compile time,link time,distribution time, installation time, load time, and run time.

- **collections** : is a concept application to abstract data types, and dose not prescribe a specific implemetation as a concrete data structure, though often there is a conventional choice, examples of collections include lists,sets,trees, and graphs

- **“Repository” design pattern** : Repository pattern is a kind of container where data access logic is stored. It hides the details of data access logic from business logic

- **mongoose middleware** : (also called pre and post hooks) are functions which are passed control during execution of asynchronous functions. Middleware is specified on the schema level and is useful for writing plugins.

- **Object Relation Mapping (ORM)** : programming technique for converting data between incompatible type systems using object-oriented programming languages.

---

## Preparation Materials.

HTTP stands for Hypertext Transfer Protocol, application-layer protocol for communicating between distributed system, and is the foundation of the modern web.

HTTP allows for communication between a variety of hosts and clients, and support a mixture of network configurations, the communication usually takes place over TCP/Ip, but any reliable transport can be used. The default port for TCP/IP is 80, but other ports can also be used.

**URLs** : At the heart of web communications is the request message, which are sent via Uniform Resource Locators (URLs).URLs have a simple structure that consists of the following components:

<img src="https://cdn.tutsplus.com/net/authors/jeremymcpeak/http1-url-structure.png" style="text-align:center; margin:50px auto; width=50%; display: block"/>

The protocol is typically `http`, but it can also be `https` for secure communications. The default port is 80, but one can be set explicitly, as illustrated in the above image. The resource path is the local path to the resource on the server.

URLs reveal the identity of the particular host with which we want to communicate, but the action that should be performed on the host is specified via HTTP verbs.

HTTP verbs :

- GET : fetch an existing resource. The URL contains all the necessary information the server needs to locate and return the resource.

- POST : create a new resource. POST requests usually carry a payload that specifies the data for the new resource.

- PUT : update an existing resource. The payload may contain the updated data for the resource.

- DELETE : delete an existing resource.

**[Status Codes](https://www.tutorialspoint.com/http/http_status_codes.htm)**

- 1XX : Informational Messages
- 2XX : Successful
- 3XX : Redirection
- 4XX : Client Error
- 5XX : Server Error

**Request and Response Message Formats**

generic structure of a response message

```xml
message = <start-line>
          *(<message-header>)
          CRLF
          [<message-body>]

<start-line> = Request-Line | Status-Line
<message-header> = Field-Name ':' Field-Value
```

It's mandatory to place a new line between the message headers and body. The message can contain one or more headers, of which are broadly classified into:

- General Headers : that are application for both request and response messages.
- request specific headers.
- response specific headers.
- entity headers.
