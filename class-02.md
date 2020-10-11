# Classes, Inheritance, Functional Programming

## Why would you want to run JavaScript code outside of a browser?

JaaScript is a ront-end language which can minipulate the DOM, create events and such more thing, but all these things are happening in the browser.

So what if we want to call an API and get a specific data from it, or connect a data base to get some information about a user for example using JavaScript language, here come the need for **Node.js** which it was designed to build scalable network aplications.

## What is the difference between a module and a package?

- A module is a single javaScript file that has some funciton on it.

- A package is a directory with one or more modules inside of it and a pacakge.json file which has metadata about the package.

## What does the node package manager do?

Node Package Manager [(npm)](https://www.npmjs.com/), it is an online repository for the publishing of open-source Node.js projects, and it is a commind-line utility for package installation.

```cmd
npm install <pacakge name>
```

## Provide code snippets showing 3 different ways to export a function from a node module

exports is an object, So it exposes whatever you assigned to it as a module.

1. Export Literals:

```javascript
// Exporting this from message.js
module.exports = 'Any String'
// import message.js into another file
const message = require('path to message.js');
console.log(message) => 'Any String'
```

2. Exporting Objects

The exports is an object. So, you can attach properties or methods to it

```javascript
// Exporting this from message.js
module.exports.SimpleText = 'Hello world!';
module.exports.print = function(msg){
    console..log(msg);
}
// import message.js into another file
const message = require('path to message.js');
console.log(message.SimpleText);
message.print('this is a test')  // this will console log => this is a test
// So message is an object and SimpleText is a property of that object
```

3. Export Function as a Class

In JavaScript, a function can be treated like a class.

<p>Exporting from message.js</p>

```javascript
module.exports = function (firstName, lastName) {
  this.firstName = firstName;
  this.lastName = lastName;
  this.fullName = function () {
    return this.firstName + ' ' + this.lastName;
  };
};
```

<p>Importing to app.js</p>

```javascript
var person = require('./Person.js');

var person1 = new person('James', 'Bond');

console.log(person1.fullName());
```

---

## Document the following Vocabulary Terms

1. **ecosystem** : is a collection of software packages, libraries, and other resources that facilitate development as they integrate with each other. Those tools are created by different developers and providers

1. **Node.js** : is an asynchronous event-driven JavaScript runtime, that execute JavaScript code outside the browser
1. **V8 engine** : V8 is Google’s open source high-performance JavaScript and WebAssembly engine, written in C++. It is used in Chrome and in Node.js
1. **module** : is a simple or complex functionality organized in single or multiple JavaScript files which can be reused throughout the Node.js application.
1. **package** : is a file or directory that is described by a package.json file. contains a multiple modules, you can download them using npm
1. **node package manager (npm)** : it is an online repository for the publishing of open-source Node.js projects, and it is a commind-line utility for package installation.

1. **server** : It's a computer that provides data for other computers.
1. **environment** : group of tools, that you have to install to develope any kind of code or programe,
1. **interpreter** : is a computer program that directly executes instructions written in a programming or scripting language, without requiring them previously to have been compiled into a machine language program.
1. **compiler** : is a computer program that translates computer code written in one programming language into another language
