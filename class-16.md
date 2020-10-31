# Event Driven Applications

## Review, Research, and Discussion

- Why is access control important?

To Prevent any unauthorized access for the application/web site, and for giving these privileges to specific users (Admins) for the application/web site.

- Describe an application that would need access control.

CRUD system at some point in any web application needs access control, I mean you don't want an ordinary user can have access to modify some products in your web application.

- What is a role used for?

An organization assigns a role-based access control role to every employee; the role determines which permissions the system grants to the user.

- Why is role based access control more scalable than discretionary or mandatory access control.

In any company, network users must be both authenticated and authorized before they can access parts of the system capable of leading to security breaches. The process of gaining authorization is called access control.

MAC stands for Mandatory Access Control (MAC). its a security model where users are given permissions to resources by an admin or root. These permissions can ONLY be granted by the root user or administrator.Only an administrator can grant permissions or right to objects and resources.

RBAC stands for Role-Based Access Control (RBAC). access to system resources are based on the role given to a user by the administrator. If an administrator assigns a user to a role that contains certain predetermined system rights and privileges, the user's association with the role, then the user can access only certain system resources and can perform specific tasks assigned by the rules.

---

## Vocabulary Terms

- **Authorization** : is a security mechanism to determine access levels or user/client privileges related to system resources including files, services, computer programs, data and application features. This is the process of granting or denying access to a network resource which allows the user access to various resources based on the user's identity.

- **Role Based Access Control** : refers to the idea of assigning permissions to users based on their role within an organization. It offers a simple, manageable approach to access management that is less prone to error than assigning permissions to users individually.

- **Capabilities** : represents performing or achieving certain actions/outcomes in terms of the intersection of capacity and ability.

---

## Event-Driven Programming in Node.js

Event-Driven Programming is a logical pattern that we can choose to confine our programming within to avoid issues of complexity and collision.

Event-Driven Programming makes use of the following concepts:

- An Event Handler is a callback function that will be called when an event is triggered.

- A Main Loop listens for event triggers and calls the associated event handler for that event.

### Event Emitter.

Node.js natively provides us with a useful module called [EventEmitter](https://nodejs.org/api/events.html#events_class_eventemitter) that allows us to get started incorporating Event-Driven Programming in our project right away, there are several modules published on npm such as [EventEmitter2](https://github.com/EventEmitter2/EventEmitter2) and (EventEmitter3)[https://github.com/primus/eventemitter3] which promise a faster performance that the native EventEmitter.

```javascript
const EventEmitter = require('events').EventEmitter;
const myEventEmitter = new EventEmitter();
```

### Removing Listeners

There will likely come a time when you want to remove an event listener from an event. This could be for performance reasons (the event is no longer needed) or to avoid memory leaks (if an event listener references an object that is no longer needed, it won’t be able to be garbage-collected. This can lead to a build up of unnecessary objects).

To remove event listeners in EventEmitter we can use the `removeListener` or `removeAllListeners` method. It’s important to note that in the EventEmitter that comes built-in with Node you must pass a reference to the exact function you wish to remove when using the `removeListener` method.

### Object Oriented Programming + Event-Driven Programming.

The Object Oriented approach promotes the idea that all behavior of an individual unit (or object) be handled from code within that unit. Using this approach, applications are built with many different units that all speak to and interact with each other.
