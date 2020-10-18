# HTTP and REST

## Review, Research, and Discussion

1. Define three related pieces of data in a possible application.

Let's say that we have a company, which it contains a different types of departments, these department contains different types of teams, each team contain a specific type of specialized people working together to achieve a goal.

Company --> Departments --> Teams --> People

2. What is the advantage of an ORM, like Mongoose?

ORM (Object-Relation Mapping) : it helps take advantage of the object-oriented principles while managing relational databases, this allows you to set up objects and completely manage objects while the ORM library/framework takes care of translation all functionalities into database schema and queries.

3. How does the repository pattern compare with an ORM?

4. When making a repository/facade, what flexibility do you gain?

- provide a simple interface to a complex subsystem. The application of design patterns often results in a lot of small classes which makes subsystems more flexible and customizable

5. Name 3 cloud based NoSQL Databases

- Amazon
- DynamoDB
- MongoDB

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

---

## Rest

REST is acronym for REpresentational State Transfer. It is architectural style for distributed hypermedia systems.

### Guiding Principles of REST

1. **Client–server** : By separating the user interface concerns from the data storage concerns, we improve the portability of the user interface across multiple platforms and improve scalability by simplifying the server components.

2. **Stateless** : Each request from client to server must contain all of the information necessary to understand the request, and cannot take advantage of any stored context on the server. Session state is therefore kept entirely on the client.

3. **Cacheable** : Cache constraints require that the data within a response to a request be implicitly or explicitly labeled as cacheable or non-cacheable

4. **Uniform interface** : By applying the software engineering principle of generality to the component interface, the overall system architecture is simplified and the visibility of interactions is improved

5. **Layered system** : The layered system style allows an architecture to be composed of hierarchical layers by constraining component behavior

6. **Code on demand (optional)** : REST allows client functionality to be extended by downloading and executing code in the form of applets or scripts. This simplifies clients by reducing the number of features required to be pre-implemented.

### Resource

The key abstraction of information in REST is a resource. Any information that can be named can be a resource: a document or image, a temporal service, a collection of other resources, a non-virtual object (e.g. a person), and so on. REST uses a resource identifier to identify the particular resource involved in an interaction between components.
