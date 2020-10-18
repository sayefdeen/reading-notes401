# Express

## Review, Research, and Discussion

1. What’s the difference between PUT and PATCH?

both of these methods used for updating a record, you have to specify something Unique (in general it will be the id) for the record you want to modify (update).

HowEver In PUT if you want to modify only one column/property you have to make sure that the rest of the columns/properties are sended too, to make sure that they didn't got overwrite, In PATCH you only send the specific column/property and it will be overwritten by itself only.

2. Provide links to 3 services or tools that allow you to “mock” an API for development like json-server.

- [Mirage JS](https://miragejs.com/)
- [Cypress](https://www.cypress.io/)
- [Mocky](https://designer.mocky.io/)

3. Compare and contrast Swagger and APIDoc.js 1 Which HTTP status codes should be sent with each type of (un)successful API call?

4. Compare and contrast SOAP and ReST

---

## Vocabulary Terms

- **SOAP** : is an acronym for Simple Object Access Protocol. It is an XML-based messaging protocol for exchanging information among computers. SOAP is an application of the XML specification.

- **ReST Verbs** : HTTP methods PUT,POST,GET,PATCH,DELETE,OPTIONS

- **CRUD Verbs** : CRUD operations Create:POST, Read:GET, Update:PUT/PATCH, Delete:DELETE

- **Swagger** : is in essence an Interface Description Language for describing RESTful APIs expressed using JSON, is used together with a set of open-source software tools to design, build, document, and use RESTful web services.

---

## Preparation Materials

### Using Middleware

Middleware functions are functions that have access to the request object (req), the response object (res), and the next middleware function in the application’s request-response cycle. The next middleware function is commonly denoted by a variable named next.

Middleware function can perform the following tasks:

- Execute any code.
- Make changes to the request and the response objects.
- End the request-response cycle.
- Call the next middleware function in the stack.

If the current middleware function does not end the request-response cycle, it must call `next()` to pass control to the next middleware function. Otherwise, the request will be left hanging.

Examples:

### **Application-level middleware**

1. This middleware function has no mount path, The function is executed every time the app receives a request.

```javascript
var express = require('express');
var app = express();

app.use(function (req, res, next) {
  console.log('Time:', Date.now());
  next();
});
```

2. This middleware mounted on the `/user/:id` path, the function is executed for ant type of HTTP request on the `/user/:id` path.

```javascript
app.use('/user/:id', function (req, res, next) {
  console.log('Request Type:', req.method);
  next();
});
```

3. Loading series of middleware functions at a mount point, It illustrates a middleware sub-stack that prints request info for any type of HTTP request to the `/user/:id` path.

```javascript
app.use(
  '/user/:id',
  function (req, res, next) {
    console.log('Request URL:', req.originalUrl);
    next();
  },
  function (req, res, next) {
    console.log('Request Type:', req.method);
    next();
  }
);
```

4. This example shows a middleware sub-stack that handles GET requests to the `/user/:id` path.

Note:

`next(route)` : will stop the next middleware to be called and in will go to the third middleware, so if user id equal to 0 the third middleware will be executed, if not the second middleware will be executed.

```javascript
app.get(
  '/user/:id',
  function (req, res, next) {
    if (req.params.id === '0') {
      next('route');
    } else {
      next();
    }
  },
  function (req, res, next) {
    // send a regular response
    res.send('regular');
  }
);
app.get('/user/:id', function (req, res, next) {
  res.send('special');
});
```

4. Middleware can also be declared in an array for reusability.

```javascript
function logOriginalUrl(req, res, next) {
  console.log('Request URL:', req.originalUrl);
  next();
}

function logMethod(req, res, next) {
  console.log('Request Type:', req.method);
  next();
}

var logStuff = [logOriginalUrl, logMethod];
app.get('/user/:id', logStuff, function (req, res, next) {
  res.send('User Info');
});
```

### **Router-level middleware**

Router-level middleware works in the same way as application-level middleware, except it is bound to an instance of `express.Router()`.

```javascript
var express = require('express');
var app = express();
var router = express.Router();

// a middleware function with no mount path. This code is executed for every request to the router
router.use(function (req, res, next) {
  console.log('Time:', Date.now());
  next();
});

// a middleware sub-stack shows request info for any type of HTTP request to the /user/:id path
router.use(
  '/user/:id',
  function (req, res, next) {
    console.log('Request URL:', req.originalUrl);
    next();
  },
  function (req, res, next) {
    console.log('Request Type:', req.method);
    next();
  }
);

// a middleware sub-stack that handles GET requests to the /user/:id path
router.get(
  '/user/:id',
  function (req, res, next) {
    // if the user ID is 0, skip to the next router
    if (req.params.id === '0') next('route');
    // otherwise pass control to the next middleware function in this stack
    else next();
  },
  function (req, res, next) {
    // render a regular page
    res.render('regular');
  }
);

// handler for the /user/:id path, which renders a special page
router.get('/user/:id', function (req, res, next) {
  console.log(req.params.id);
  res.render('special');
});

// mount the router on the app
app.use('/', router);
```

### Error-handling middleware

Define error-handling middleware functions in the same way as other middleware functions, except with four arguments instead of three, specifically with the signature `(err, req, res, next)`:

```javascript
app.use(function (err, req, res, next) {
  console.error(err.stack);
  res.status(500).send('Something broke!');
});
```

### Third-party middleware

Use third-party middleware to add functionality to Express apps.

Install the Node.js module for the required functionality, then load it in your app at the application level or at the router level.

The following example illustrates installing and loading the cookie-parsing middleware function cookie-parser.

```cmd
npm install cookie-parser
```

```javascript
var express = require('express');
var app = express();
var cookieParser = require('cookie-parser');

// load the cookie-parsing middleware
app.use(cookieParser());
```

### Response Methods

- **`res.download()`** : Prompt a file to be downloaded.
- **`res.end()`** : End the response process.
- **`res.json()`** : Send a JSON response.
- **`res.jsonp()`** : Send a JSON response with JSONP support.
- **`res.redirect()`** : Redirect a request.
- **`res.render()`** : Render a view template.
- **`res.send()`** : Send a response of various types.
- **`res.sendFile()`** : Send a file as an octet stream.
- **`res.sendStatus()`** : Set the response status code and send its string representation as the response body.
