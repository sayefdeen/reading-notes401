# API Server

## Review, Research, and Discussion

- How does route prefixing work with an external routing module?

- When routing, what’s the difference between app.get('/data/:id') and app.get('/data/:name')?

- Explain how Express handles routing conflicts?

- What are the ways that a browser can send “data” or request variables to an HTTP server

- The data can be send into the headers

- in the url itself using quey strings

---

## Vocabulary Terms

- **Routing** : refers to how an application’s endpoints (URIs) respond to client requests.

- **Route Prefixing** :

- **Request “Body”** : is the data sent by the client to the API

- **Request “Query”** : query string is a part of a uniform URL that assign values to specified parameters, this query string will be stored in the `query` property of the request Body _used in GET method_

- **Request “Params”** : the query string in _POST,PUT,and DELETE methods_ will be stored in the `params` property of the request body

---

## Preparation Materials

### router.param()

```javascript
router.param(name, callback);
```

Adds callback triggers to route parameters, where `name` is the name of the parameter and `callback` is the callback function.

For example, when :user is present in a route path, you may map user loading logic to automatically provide req.user to the route, or perform validations on the parameter input.

```javascript
router.param('user', function (req, res, next, id) {
  // try to get the user details from the User model and attach it to the request object
  User.find(id, function (err, user) {
    if (err) {
      next(err);
    } else if (user) {
      req.user = user;
      next();
    } else {
      next(new Error('failed to load user'));
    }
  });
});
```

Param callback functions are local to the router on which they are defined, they are not inherited by mounted apps or routers, hence, param callbacks define on `router` will be triggered only by route parameters define on `router` routes.

A param callback will be called only once in a request-response cycle, even if the parameter is matched in multiple routes, as shown in the following examples.
