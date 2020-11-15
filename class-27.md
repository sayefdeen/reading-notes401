# Props and State

## Review, Research, and Discussion

- Does a deployed React application require a server?

No, we don't need Nodejs to run a react application , React is client side library, but what Nodejs offer is a series of tools that allows you to be able wo work with React more easily, such as

1. Webpack (gathers code into a single bundle and listens for file changes to reload this bundle to show the update code).

2. Babel (converts ES6 and JSX to plain JavaScript).

npx itself is a Node tool which allows you to run a package, in this case with Create React App, which allows you to easily start a new React project.

The server is simply to allow the reloading of the app is response to file changes in real time.

- Why do we prefer to test a React application at the behavior rather than the unit level?

* What does npm run build do?

  Builds the app for production to the build folder.
  It correctly bundles React in production mode and optimizes the build for the best performance.

* Describe the actual composition / architecture of a React application

## Vocabulary Terms

- **BDD** : Behavior Driven Development,is an Agile software development process that encourages collaboration among developers, QA and non-technical or business participants in a software project

- **Acceptance Tests** :formal description of the behavior of a software product, generally expressed as an example or a usage scenario. A number of different notations and approaches have been proposed for such examples or scenarios. In many cases the aim is that it should be possible to automate the execution of such tests by a software tool, either ad-hoc to the development team or off the shelf.

- **mounting** : is ehn React renders the components for the first time and actually builds the initial DOM for those instruction

- **build** :When you’re ready to deploy to production, running `npm run build ` will create an optimized build of your app in the build folder.

## Preparation Materials

### Status

React components, have state State can be anything, but think of things like whether a user is logged in or not and displaying the correct username based on which account is active.

React components with state render UI based on that state. When the state of components changes, so does the component UI.

`setState()` : is the only legitimate way to update state after the initial state setup.

```javascript
import React, { Component } from 'react';

class Search extends Component {
  constructor(props) {
    super(props);

    state = {
      searchTerm: ''
    };
  }
}
```

the state here is an object can contain properties, searchTerm is a property empty string, initial value of it.

To update the state we have to use `setState()` method, we are passing an object containing parts of the state we want to update, it works in this order.

1. adding an eventListener, listening on a user input for an example.
2. when the user enter some input this event will trigger a function that will take this input.
3. this input will update the state property that was used in `setStatus()` method

```javascript
setState({ searchTerm: event.target.value });
```

The rule of thumb is to never mutate state directly. Always use `setState()` to change state. Modifying state directly, like the snippet below will not cause the component to re-render.

```javascript
this.state = {
  searchTerm: event.target.value
};
```

### Passing a function to `getStatus()`.

```javascript
class App extends React.Component {
  state = { count: 0 };

  handleIncrement = () => {
    this.setState({ count: this.state.count + 1 });
  };

  handleDecrement = () => {
    this.setState({ count: this.state.count - 1 });
  };
  render() {
    return (
      <div>
        <div>{this.state.count}</div>
        <button onClick={this.handleIncrement}>Increment by 1</button>
        <button onClick={this.handleDecrement}>Decrement by 1</button>
      </div>
    );
  }
}
```

So far this code will increase and decrease by one each time you click one of the buttons, but what if we want to increase in 3 times?

This will not work because it is equitant to `Object.assign()`, it is used to copy the data from a source object, all the targets have the same key which means the last `this.setStatus()` will win and increase the number by one only.

```javascript
handleIncrement = () => {
  this.setState({ count: this.state.count + 1 });
  this.setState({ count: this.state.count + 1 });
  this.setState({ count: this.state.count + 1 });
};

// This will handle the previous error

handleIncrement = () => {
  this.setState((prevState) => ({ count: prevState.count + 1 }));
  this.setState((prevState) => ({ count: prevState.count + 1 }));
  this.setState((prevState) => ({ count: prevState.count + 1 }));
};

// The best way in to use an Updater

handleDecrement = () => {
  this.changeCount();
  this.changeCount();
  this.changeCount();
};

changeCount = () => {
  this.setState((prevState) => {
    return { count: prevState.count - 1 };
  });
};

//  Same goes for handleIncrement method
```

### Handle Events

```javascript
function ActionLink() {
  function handleClick(e) {
    e.preventDefault();
    console.log('The link was clicked.');
  }
  return (
    <a href='#' onClick={handleClick}>
      {' '}
      Click me
    </a>
  );
}

class LoggingButton extends React.Component {
  handleClick() {
    console.log('this is:', this);
  }

  render() {
    // This syntax ensures `this` is bound within handleClick
    return <button onClick={() => this.handleClick()}> Click me</button>;
  }
}
```

### Forms

```javascript
class NameForm extends React.Component {
  constructor(props) {
    super(props);
    this.state = { value: '' };
    this.handleChange = this.handleChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
  }

  handleChange(event) {
    this.setState({ value: event.target.value });
  }
  handleSubmit(event) {
    alert('A name was submitted: ' + this.state.value);
    event.preventDefault();
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <label>
          Name:
          <input
            type='text'
            value={this.state.value}
            onChange={this.handleChange}
          />{' '}
        </label>
        <input type='submit' value='Submit' />
      </form>
    );
  }
}
```

- Controlled Input Null Value

The following code demonstrates this. (The input is locked at first but becomes editable after a short delay.)

```javascript
ReactDOM.render(<input value='hi' />, mountNode);

setTimeout(function () {
  ReactDOM.render(<input value={null} />, mountNode);
}, 1000);
```

### State and Lifecycle

Clock component. It will set up its own timer and update itself every second.

```javascript
class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = { date: new Date() };
  }

  componentDidMount() {
    this.timerID = setInterval(() => this.tick(), 1000);
  }

  componentWillUnmount() {
    clearInterval(this.timerID);
  }

  tick() {
    this.setState({ date: new Date() });
  }
  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}

ReactDOM.render(<Clock />, document.getElementById('root'));
```
