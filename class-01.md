# Node Ecosystem, TDD, CI/CD

## Review, Research, and Discussion

### 1. [Array.map()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map)

Its a prototype function (method) that can be used by arrays, it will return a new array without effecting the original one.

```javascript
Array.map();

// Example
const array1 = [1, 5, 9, 16];

const map1 = array.map((x) => x * 2);
console.log(map1);
// This output will be : Array [2,10,18,32];
```

---

### 2. [Array.reduce()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce)

Its a prototype function (method) that can be used by arrays, it will run in each element of the array and returning a single value of that array.

```javascript
Array.reduce();

// Example
const array1 = [1, 2, 3, 4];

const map1 = array.map((acc, num) => {
  return acc + num;
}, 0);
console.log(map1);
// This output will be : 10;
```

As you can see in the previous code there is two arguments in reduce method, the first one is the accumulator (the one which will be returned), and the num (each element in the array), by defualt the accumulator will take the first index value, but if we initilized it by 0 (after the curly bracets) it will begins with the value of **ZERO**.

---

### 3. [superagent](https://www.npmjs.com/package/superagent)

It is a client-side HTTP library for Node.js

- using .then()

```javascript
// url is the url of the API, or a folder
// data is the results from the calling
superagent.get(url).then((data) => {
  console.log(data);
});
```

- using async/await

```javascript
async function calling() {
  const res = await superagent.get(url);
  console.log(res);
}
```

---

### 4. [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise).

javaScript works in a single thread, that's mean each line should be finished in the stack so we can render all the code, but calling data from an outside sourse (API) may take some time (longer than rendering the code itself), so it will cause some problems in the website expecally if some of the code peices was depending in the data returning.

Here comes the promises job, whenever we want to get data from outside source, another thread will be created for that calling,working parallel to the main thread.

A Promise is on one of these states :

- Pending : initial state, neither fulfilled nor rejected.
- fulfilled: meaning that the operation was completed successfully.
- rejected: meaning that the operation failed.

---

## Preparation Materials

### Nodejs introduction

Nodejs is an open source server environment, which runs in different platforms, and uses JavaScript on the server

Nodejs can generate dynamic page content, create, open,read,write,delete,and close files on the server, collect form data, add delete, modify data in the database

Nodejs file contain tasks,that will be executed on certain events, like someone trying to access a port on the server, files must be initiated on the server before having any effect, files have extension ".js"

### What is Nodejs

It is a run-time environment includes everything you need to execute a program written in JavaScript.

Nodejs came into existence when the original developers of JavaScript extended it from something you could only run in the browser to something you could run on your machine as a standalone application.

Both your browser JavaScript and Node.js run on the V8 JavaScript runtime engine. This engine takes your JavaScript code and converts it into a faster machine code. Machine code is low-level code which the computer can run without needing to first interpret it.

- Node.js® is a JavaScript runtime built on Chrome’s V8 JavaScript engine.

- Node.js uses an event-driven, non-blocking I/O model that makes it lightweight and efficient.

- Node.js’ package ecosystem, npm, is the largest ecosystem of open source libraries in the world.

I/O refers to input/output. It can be anything ranging from reading/writing local files to making an HTTP request to an API.

I/O takes time and hence blocks other functions.

- Blocking I/O : in this method, if user want to get his data from the database for example, he should wait for user1 to get his data first.

- Non-Blocking I/O : On the other hand, using a non-blocking request, you can initiate a data request for user2 without waiting for the response to the request for user1. You can initiate both requests in parallel.

---

### What is npm

npm is the world’s largest software registry. Open source developers from every continent use npm to share and borrow packages, and many organizations use npm to manage private development as well.

Use npm to :

- Adapt packages of code for your apps, or incorporate packages as they are.
- Download standalone tools you can use right away.
- Run packages without downloading using npx.
- Share code with any npm user, anywhere.
- Restrict code to specific developers.
- Create Orgs (organizations) to coordinate package maintenance, coding, and developers.
- Form virtual teams by using Orgs.
- Manage multiple versions of code and code dependencies.
- Update applications easily when underlying code is updated.
- Discover multiple ways to solve the same puzzle.
- Find other developers who are working on similar problems and projects.
