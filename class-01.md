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
