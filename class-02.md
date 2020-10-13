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

---

## Preparation Materials

### TDD in Js

Test-driven development (TDD) is a technique for ensuring that your code does what you think it does.

TDD is a great way of catching the majority of programming errors. It’s not perfect, of course—in particular, it can’t tell you when your assumptions are wrong—but it’s very good at catching the kinds of bugs JavaScript is prone to.

### Context

Context is what the value of `this` keyword in your code when it is running.

### Inheritance

JavaScript is a bit confusing for developers experienced in class-based languages (like Java or C++), as it is dynamic and does not provide a class implementation per se (the class keyword is introduced in ES2015, but is syntactical sugar, JavaScript remains prototype-based).

When it comes to inheritance, JavaScript only has one construct: objects. Each object has a private property which holds a link to another object called its prototype. That prototype object has a prototype of its own, and so on until an object is reached with null as its prototype. By definition, null has no prototype, and acts as the final link in this prototype chain.

Nearly all objects in JavaScript are instances of Object which sits on the top of a prototype chain.

### Classes

Classes are a template for creating objects. They encapsulate data with code to work on that data. Classes in JS are built on prototypes but also have some syntax and semantics that are not shared with ES5 classalike semantics.

```javascript
class Rectangle {
  constructor(height, width) {
    this.height = height;
    this.width = width;
  }
  // This method could be used by the class name directly
  static area(height, width) {
    return height * width;
  }
}
```

### this

A function's this keyword behaves a little differently in JavaScript compared to other languages. It also has some differences between strict mode and non-strict mode.

A property of an execution context (global, function or eval) that, in non–strict mode, is always a reference to an object and in strict mode can be any value.

1. Global context

In the global execution context (outside of any function), this refers to the global object whether in strict mode or not.

```javascript
console.log(this === window); // true
a = 37;
console.log(window.a); // 37
this.b = 'MDN';
console.log(window.b); // "MDN"
console.log(b); // "MDN"
```

2. Function context

Inside a function, the value of this depends on how the function is called.

non-strict mode : this will default to the global object, which is window in a browser.

```javascript
function f1() {
  return this;
}
// In a browser:
f1() === window; // true
// In Node:
f1() === globalThis; // true
```

strict mode : if the value of this is not set when entering an execution context, it remains as undefined

```javascript
function f2() {
  'use strict'; // see strict mode
  return this;
}
f2() === undefined; // true
```

3. Class context

The behavior of this in classes and functions is similar, since classes are functions under the hood. But there are some differences and caveats.

Within a class constructor, this is a regular object. All non-static methods within the class are added to the prototype of this:

```javascript
function f2() {
  class Example {
    constructor() {
      const proto = Object.getPrototypeOf(this);
      console.log(Object.getOwnPropertyNames(proto));
    }
    first() {}
    second() {}
    static third() {}
  }
  new Example(); // ['constructor', 'first', 'second']
}
```
