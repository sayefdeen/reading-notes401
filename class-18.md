# Socket.io

- What is the benefit of transforming data into packets?

- UDP is often refereed to as a connectionless protocol. Why is this?

UDP is a connectionless protocol. No connection needs to be established between the source and destination before you transmit data. UDP does not have a mechanism to make sure that the payload is not corrupted. As a result, the application must take care of data integrity all by itself.

- Can a socket server application have multiple socket connections?

Multiple connections on the same server can share the same server-side IP/Port pair as long as they are associated with different client-side IP/Port pairs, and the server would be able to handle as many clients as available system resources allow it to.

- Can a socket connection application be connected to multiple socket servers?

- Can an application be both a socket server and a socket connection?

---

## Vocabulary Terms

- **OSI Model** : (Open Systems Interconnection Model) is a conceptual framework used to describe the functions of a networking system.

- **TCP Model** : The Internet protocol suite is the conceptual model and set of communications protocols used in the Internet and similar computer networks. It is commonly known as TCP/IP because the foundational protocols in the suite are the Transmission Control Protocol (TCP) and the Internet Protocol (IP).

- **TCP** : (Transmission Control Protocol) is a standard that defines how to establish and maintain a network conversation through which application programs can exchange data. TCP works with the Internet Protocol (IP), which defines how computers send packets of data to each other.

- **UDP** : User Datagram Protocol) is a communications protocol that is primarily used for establishing low-latency and loss-tolerating connections between applications on the internet. It speeds up transmissions by enabling the transfer of data before an agreement is provided by the receiving party.

- **Packets** : a network packet is a formatted unit of data carried by a packet-switched network. A packet consists of control information and user data; the latter is also known as the payload.

- **Socket** : A network socket is a software structure within a network node of a computer network that serves as an endpoint for sending and receiving data across the network.

---

## WebSocket

WebSocket is a computer communications protocol, providing full-duplex communication channels over a single TCP connection. The WebSocket protocol was standardized by the IETF as RFC 6455 in 2011, and the WebSocket API in Web IDL is being standardized by the W3C.

Unlike HTTP, WebSocket provides full-duplex communication,WebSocket enables streams of messages on top of TCP. TCP alone deals with streams of bytes with no inherent concept of a message.

The WebSocket protocol specification defines ws (WebSocket) and wss (WebSocket Secure) as two new uniform resource identifier (URI) schemes that are used for un-encrypted and encrypted connections, respectively. Apart from the scheme name and fragment (i.e. # is not supported), the rest of the URI components are defined to use URI generic syntax.
