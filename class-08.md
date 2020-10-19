# Express Routing & Connected API

## Review, Research, and Discussion

- Name 3 real world use cases where you’d want to change the request with custom middleware.

  - Make the Password decrypted before store it in the database.
  - Make sure that the data are validated before store it into database
  - Authentication, check if the user is trying to access a protion of the site that requires authentication

- True or false: The route handler is middleware?

False, a route handler in coe that is looking for a request to a specific incoming URL, and often a specific HTTP verb such as POST and has a specific code for handling that precise URL and verb.

- In what ways can a middleware function end the process and send data to the browser?

since middle ware takes 3 parameters which they are the `request`, `response` , and `next`, if the developer want for the middleware to handle the request, he have to send a response, if not required just pass it using `next()` method at the end of the middleware.

- At what point in the request lifecycle can you “inject” middleware?

- What can cause express to error with “Request headers sent twice, cannot start a second response”

---

## Vocabulary

- **Middleware** : functions that have access to the request object `(req)`, the response object `(res)`, and the next middleware function in the application’s request-response cycle. The next middleware function is commonly denoted by a variable named `next`.

- **Request Object** : The req object represents the HTTP request and has properties for the request query string, parameters, body, HTTP headers, and so on

- **Response Object** : The res object represents the HTTP response that an Express app sends when it gets an HTTP request.

- **Application Middleware** : Bind application-level middleware to an instance of the app object by using the app.use() and app.METHOD() functions, where METHOD is the HTTP method of the request that the middleware function handles (such as GET, PUT, or POST) in lowercase.

- **Routing Middleware** : Router-level middleware works in the same way as application-level middleware, except it is bound to an instance of `express.Router()`.

---

## Preparation Materials

### Routing

Routing refers to how an application’s endpoints (URIs) respond to client requests. For an introduction to routing, we define routing using methods of the Express `app` object that correspond to HTTP methods.

- `app.get()` : to handle GET requests
- `app.post()` : to handle POST requests
- `app.all()` : to handle ALL HTTP requests
- `app.use()` : to specify middleware as the callback function

Example.

```javascript
const express = require('express');
const app = express();
// respond with "hello world" when a GET request is made to the homepage
app.get('/', (req, res) => {
  res.send('hello world');
});
```

### Route Methods

A route method is derived from one of the HTTP methods, and is attached to an instance of the express class.

The following code is an example of routes that are defined for the GET and the POST methods to the root of the app.

```javascript
// GET method route
app.get('/', function (req, res) {
  res.send('GET request to the homepage');
});

// POST method route
app.post('/', function (req, res) {
  res.send('POST request to the homepage');
});
```

### Route paths

- This route path will match request to the root /about.

```javascript
app.get('/about', function (req, res) {
  res.send('about');
});
```

- This route path will match requests to /random.text..

```javascript
app.get('/random.text', function (req, res) {
  res.send('random.text');
});
```

- This route path will match acd and abcd.

```javascript
app.get('/ab?cd', function (req, res) {
  res.send('ab?cd');
});
```

- This route path will match abcd, abbcd, abbbcd, and so on.

```javascript
app.get('/ab+cd', function (req, res) {
  res.send('ab+cd');
});
```

- This route path will match abcd, abxcd, abRANDOMcd, ab123cd, and so on.

```javascript
app.get('/ab*cd', function (req, res) {
  res.send('ab*cd');
});
```

### Route parameters

Route parameters are named URL segments that are used to capture the values specified at their position in the URL. The captured values are populated in the req.params object, with the name of the route parameter specified in the path as their respective keys.

```text
Route path: /users/:userId/books/:bookId
Request URL: http://localhost:3000/users/34/books/8989
req.params: { "userId": "34", "bookId": "8989" }
```

```javascript
app.get('/users/:userId/books/:bookId', function (req, res) {
  res.send(req.params);
});
```

### Response Methods

- `res.download()` : prompt a file to be downloaded.
- `res.end()` : End the response process.
- `res.json()` : Send a JSON response.
- `res.jsonp()` : Send a JSON response with JSONP support.
- `res.redirect()` : Redirect a request.
- `res.render()` : Render a view template.
- `res.send()` : Send a response of various types.
- `res.sendFile()` : Send a file as an octet stream.
- `res.sendStatus()` : Set the response status code and send its string representation as the response body.

### app.route().

You can create chainable route handlers for a route path by using app.route(). Because the path is specified at a single location, creating modular routes is helpful, as is reducing redundancy and typos. For more information about routes.

```javascript
app
  .route('/book')
  .get(function (req, res) {
    res.send('Get a random book');
  })
  .post(function (req, res) {
    res.send('Add a book');
  })
  .put(function (req, res) {
    res.send('Update the book');
  });
```

### express.Router

Use the express.Router class to create modular, mountable route handlers. A Router instance is a complete middleware and routing system; for this reason, it is often referred to as a “mini-app”.

```javascript
let express = require('express');
let router = express.Router();

// middleware that is specific to this router
router.use(function timeLog(req, res, next) {
  console.log('Time: ', Date.now());
  next();
});
// define the home page route
router.get('/', function (req, res) {
  res.send('Birds home page');
});
// define the about route
router.get('/about', function (req, res) {
  res.send('About birds');
});

module.exports = router;
```

```javascript
var birds = require('./birds');

// ...

app.use('/birds', birds);
```
