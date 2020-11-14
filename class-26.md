# Component Based UI.

## Review, Research, and Discussion

- Name 5 Javascript UI Frameworks (other than React)

  - [Angular](https://angular.io/)
  - [Vue](https://vuejs.org/)
  - [Ember](https://emberjs.com/)
  - [Meteor.js](https://www.meteor.com/)
  - [Aurelia.js](https://aurelia.io/)

- What’s the difference between a framework and a library?

Both frameworks and libraries are code written by someone else that, will provide the user with set of methods that will help the user to solve common problems.

The difference can be explained with something called **Inversion Of control**.

The library : The user code will call the library function/method in a specific location that the user choose. this means the user code is the caller and the library is the colly.

The framework : The previous relation is inverted, which means the framework is the caller, and the user code is the colly.

The main difference depending in the flow, frameworks control your application flow in the other hand library do not.

## Vocabulary Terms

- **Rendering** : is the creation of a visual representation, of any type of data
- **Templates** : refers to a sample document/code that has already some details in place, those can either by hand or through an automated iterative process
- **State** :the particular condition that someone or something is in at a specific time.

## Preparation Materials

### React

A JavaScript **library** for building user interfaces

JSX it is a syntax extension to JavaScript,it is used with React to describe what the UI should look like.

JSX produces React elements.

```JSX
const element = <h1>Hello, world!</h1>;
```

React embraces the fact that rendering logic is inherently coupled with other UI logic: how events are handled, how the state changes over time, and how the data is prepared for display.

Instead of artificially separating technologies by putting markup and logic in separate files, React separates concerns with loosely coupled units called “components” that contain both.

React doesn’t require using JSX, but most people find it helpful as a visual aid when working with UI inside the JavaScript code. It also allows React to show more useful error and warning messages.

### Embedding Expressions in JSX

```JSX
const name = 'Josh perez';
const element = <h1>Hello,{name}</h1>;

ReactDOM.render(
    element,
    document.getElementById('root')
);
```

```JSX
function formatName(user) {
  return user.firstName + ' ' + user.lastName;
}

const user = {
  firstName: 'Harper',
  lastName: 'Perez'
};

const element = (
  <h1>
    Hello, {formatName(user)}!  </h1>
);

ReactDOM.render(
  element,
  document.getElementById('root')
);
```

### Rendering Elements

```HTML
<div id="root"></div>
```

We call this a “root” DOM node because everything inside it will be managed by React DOM, Applications built with just React usually have a single root DOM node. If you are integrating React into an existing app, you may have as many isolated root DOM nodes as you like.

```JSX
const element = <h1>Hello, world</h1>;
ReactDOM.render(element, document.getElementById('root'));
```

### Updating the Rendered Element

React elements are immutable. Once you create an element, you can’t change its children or attributes. An element is like a single frame in a movie: it represents the UI at a certain point in time.

```JSX
function tick() {
  const element = (
    <div>
      <h1>Hello, world!</h1>
      <h2>It is {new Date().toLocaleTimeString()}.</h2>
    </div>
  );
  ReactDOM.render(element, document.getElementById('root'));}

setInterval(tick, 1000);
```

It calls ReactDOM.render() every second from a setInterval() callback.

React DOM **compares the element and its children to the previous one**, and only applies the DOM updates necessary to bring the DOM to the desired state.
