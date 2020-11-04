# Message Queues

## Review, Research, and Discussion

- What does it mean that web sockets are bidirectional? Why is this useful?

it means the server and the client can send data to each other, and each connection between the server and any client works in a separate thread

- Does socket.io use HTTP? Why?.

the initial connection setup it done over HTTP. Also, a `socket.io` server will attach to an HTTP server so it can serve its own client code through /socket.io/socket.io.js.

- What happens when a client emits an event?

it will sent to the server, to see if there is a listener in that event

- What happens when a server emits an event?

it will be sent to all the clients, and see in each client if there is a listener to that event

- What happens if a client “misses” an event?

Nothing; It was not meant to the client to receive it.

- How can we mitigate this?

We can sent the event to a specific client, just reduce the response time.

---

## Vocabulary Terms

- **Web Socket** : is a computer communications protocol, providing full-duplex communication channels over a single TCP connection.

- **Socket.io** : is a JavaScript library for realtime web applications. It enables realtime, bi-directional communication between web clients and servers. It has two parts: a client-side library that runs in the browser, and a server-side library for Node.js

- **Client** : a client is a piece of computer hardware or software that accesses a service made available by a server as part of the client–server model of computer networks. The server is often on another computer system, in which case the client accesses the service by way of a network.

- **Server** : a server is a piece of computer hardware or software that provides functionality for other programs or devices, called "clients". This architecture is called the client–server model.

---
