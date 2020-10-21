# API Server

## Review, Research, and Discussion

- How does route prefixing work with an external routing module?

- When routing, what’s the difference between app.get('/data/:id') and app.get('/data/:name')?

The difference is the changing of the request params property

- Explain how Express handles routing conflicts?

Routes in express are processed in order, thus we can but an error handler as the last route which mean if any route throw an error in will automatically goes to the error handler route.

- What are the ways that a browser can send “data” or request variables to an HTTP server

  - Ajax
  - JQuery Methods
  - fetch
  - Forms

---

## Vocabulary Terms

- **Routing** : refers to how an application’s endpoints (URIs) respond to client requests.

- **Route Prefixing** : specify the common route prefix at the controller level to eliminate the need to repeat the common route.

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

### mongoose middleware

Middleware also called pre/post _hooks_ are functions which are passed control during execution of asynchronous functions, Middleware is specified on the schema level and is useful for writing plugins.

- Types of middleware

  - document middleware
  - model middleware
  - aggregate middleware
  - query middleware

Pre middle functions are executed one after another, when each middleware calls `next`.

```javascript
const schema = new Schema();
schema.pre('save',function(next)){
  // do anything
  next();
}

schema.pre('save',async function()){
  await func1();
  await func2();
}
```

it you use `next()` it dose not stop the rest of the code in your middleware function from executing using the early return pattern to prevent the rest of your middleware function from running when you call `next()`

```javascript
const schema = new Schema(..);
schema.pre('save', function(next) {
  if (foo()) {
    console.log('calling next!');
    // `return next();` will make sure the rest of this function doesn't run
    /*return*/ next();
  }
  // Unless you comment out the `return` above, 'after next' will print
  console.log('after next');
});
```

### Errors in pre Hooks

If any pre hook errors out, mongoose will not execute subsequent middleware or the hooked function. Mongoose will instead pass an error to the callback and/or reject the returned promise. There are several ways to report an error in middleware:

Calling next() multiple times is a no-op. If you call next() with an error err1 and then throw an error err2, mongoose will report err1.

```javascript
schema.pre('save', function (next) {
  const err = new Error('something went wrong');
  // If you call `next()` with an argument, that argument is assumed to be
  // an error.
  next(err);
});

schema.pre('save', function () {
  // You can also return a promise that rejects
  return new Promise((resolve, reject) => {
    reject(new Error('something went wrong'));
  });
});

schema.pre('save', function () {
  // You can also throw a synchronous error
  throw new Error('something went wrong');
});

schema.pre('save', async function () {
  await Promise.resolve();
  // You can also throw an error in an `async` function
  throw new Error('something went wrong');
});

// later...

// Changes will not be persisted to MongoDB because a pre hook errored out
myDoc.save(function (err) {
  console.log(err.message); // something went wrong
});
```

### Post middleware

post middleware are executed after the hooked method and all of its `pre` middleware have completed.

If your post hook function takes at least 2 parameters, mongoose will assume the second parameter is a next() function that you will call to trigger the next middleware in the sequence.

Calling `pre() `or `post()` after compiling a model does not work in Mongoose in general,This means that you must add all middleware and plugins before calling `mongoose.model()`.

### Sub documents

Sub documents are documents embedded in other documents. In Mongoose, this means you can nest schemas in other schemas. Mongoose has two distinct notions of sub documents: arrays of sub documents and single nested sub documents.

```javascript
const childSchema = new Schema({ name: 'string' });

const parentSchema = new Schema({
  // Array of subdocuments
  children: [childSchema],
  // Single nested subdocuments. Caveat: single nested subdocs only work
  // in mongoose >= 4.2.0
  child: childSchema,
});
```

Sub documents are similar to normal documents. Nested schemas can have middleware, custom validation logic, virtual, and any other feature top-level schemas can use. The major difference is that sub documents are not saved individually, they are saved whenever their top-level parent document is saved.

```javascript
const Parent = mongoose.model('Parent', parentSchema);
const parent = new Parent({ children: [{ name: 'Matt' }, { name: 'Sarah' }] });
parent.children[0].name = 'Matthew';

// `parent.children[0].save()` is a no-op, it triggers middleware but
// does **not** actually save the sub document. You need to save the parent
// doc.
parent.save(callback);
```

Sub documents have save and validate middleware just like top-level documents. Calling `save()` on the parent document triggers the `save()` middleware for all its sub documents, and the same for `validate()` middleware.
