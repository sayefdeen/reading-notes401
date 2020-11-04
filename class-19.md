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

### The web framework

```cmd
npm install express
```

Once it’s installed we can create an index.js file that will set up our application.

```javascript
var app = require('express')();
var http = require('http').createServer(app);

app.get('/', (req, res) => {
  res.send('<h1>Hello world</h1>');
});

http.listen(3000, () => {
  console.log('listening on *:3000');
});
```

- We define a route handler / that gets called when we hit our website home.
- We make the http server listen on port 3000.

## Integrating `Socket.IO`

Socket.IO is composed of two parts:

- A server that integrates with (or mounts on) the Node.JS HTTP Server `socket.io`
- A client library that loads on the browser side socket.io-client

```cmd
npm install socket.io
```

That will install the module and add the dependency to package.json

```javascript
var app = require('express')();
var http = require('http').createServer(app);
var io = require('socket.io')(http);

app.get('/', (req, res) => {
  res.sendFile(__dirname + '/index.html');
});

io.on('connection', (socket) => {
  console.log('a user connected');
});

http.listen(3000, () => {
  console.log('listening on *:3000');
});
```

Now in index.html add the following snippet before the </body> (end body tag):

```html
<script src="/socket.io/socket.io.js"></script>
<script>
  var socket = io();
</script>
```

## Emitting events

The main idea behind `Socket.IO` is that you can send and receive any events you want, with any data you want. Any objects that can be encoded as JSON will do, and binary data is supported too.

```html
<script src="/socket.io/socket.io.js"></script>
<script src="https://code.jquery.com/jquery-3.4.1.min.js"></script>
<script>
  $(function () {
    var socket = io();
    $('form').submit(function (e) {
      e.preventDefault(); // prevents page reloading
      socket.emit('chat message', $('#m').val());
      $('#m').val('');
      return false;
    });
  });
</script>
```

```javascript
io.on('connection', (socket) => {
  socket.on('chat message', (msg) => {
    console.log('message: ' + msg);
  });
});
```

## Broadcasting

In order to send an event to everyone, `Socket.IO` gives us the io.emit() method.

```javascript
io.emit('some event', {
  someProperty: 'some value',
  otherProperty: 'other value',
}); // This will emit the event to all connected sockets
```

If you want to send a message to everyone except for a certain emitting socket, we have the broadcast flag for emitting from that socket:

```javascript
io.on('connection', (socket) => {
  socket.broadcast.emit('hi');
});
```

In this case, for the sake of simplicity we’ll send the message to everyone, including the sender.

```javascript
io.on('connection', (socket) => {
  socket.on('chat message', (msg) => {
    io.emit('chat message', msg);
  });
});
```

And on the client side when we capture a chat message event we’ll include it in the page. The total client-side JavaScript code now amounts to:

```html
<script>
  $(function () {
    var socket = io();
    $('form').submit(function (e) {
      e.preventDefault(); // prevents page reloading
      socket.emit('chat message', $('#m').val());
      $('#m').val('');
      return false;
    });
    socket.on('chat message', function (msg) {
      $('#messages').append($('<li>').text(msg));
    });
  });
</script>
```
