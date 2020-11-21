# Hooks API

## Review

- Why do we not need more .html pages in a multi-page React app?

React is based on the concept of Single Page Application, which means that we don't need multiple HTML pages to render, we can divide the page into components and only update the component it self instead of the whole page.

- If we wanted a component to show up on every page, where would we put it and why?
  - Outside the `<BrowserRouter/>`
  - Inside the `<BrowserRouter />`, outside a `<Route />`
  - Inside a `<Route />`

Since we are dealing with React routes, everything should be inside the `<BrowserRouter>` tag, so the first choice is wrong, and for the third choice any component that is inside the `<Router />` tag will be rendered if the route was called so this component will change from page to page, so the correct answer is the second one.

- What does props.children contain?

Contain whatever markdown tags we have inside the parent when the component is invoked, in the example below the `<h1>` tag consider a child for the `<Main>` component

```Javascript
<Main>
<h1>Hello</h1>
</Main>
```

## Vocabulary

- **Composition** : In React, composition is a natural pattern of the component model, it is how we build components from other components, of varying complexity and specialization through props.

- **Children / Child Components** : if a component was used that contain another component/nodes inside it these components/nodes called a children of that Parent component. `<Parent> <Child /> </Parent>`, `<Parent> <div></div> </Parent>`.

* **Hash Routing** : using the portion of the page’s URL starting with #, we will choose what to render based on the string stored on `window.location.hash`.

* **Link Routing** : Handle the redirection for the static pages.

## Hooks

Hooks are a new addition in React 16.8. They let you use state and other React features without writing a class.

The whole idea of the components is that to divide all the problems,UI static pages to a smaller components that will make it easy to handle and to be manipulated easily, but at some point we can divide the problem into smaller components because of the logic behind this component.

Hooks apply the React philosophy (explicit data flow and composition) inside a component, rather than just between the components.

Today, there are a lot of ways to reuse logic in React apps. We can write simple functions and call them to calculate something. We can also write components (which themselves could be functions or classes). Components are more powerful, but they have to render some UI. This makes them inconvenient for sharing non-visual logic. This is how we end up with complex patterns like render props and higher-order components.

Hooks let you use React features (like state) from a function — by doing a single function call. React provides a few built-in Hooks exposing the “building blocks” of React: state, lifecycle, and context.

Hooks are fully encapsulated — each time you call a Hook, it gets isolated local state within the currently executing component.

- State Hook

```javascript
class Example extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      count: 0
    };
  }
  render() {
    return (
      <div>
        <p>You clicked {this.state.count} times</p>
        <button onClick={() => this.setState({ count: this.state.count + 1 })}>
          Click me
        </button>
      </div>
    );
  }
}
```

This example is using the old way of React by using classes so it can access the `state`

```javascript
import React, { useState } from 'react';

function Example() {
  //   Declare a new state variable, which we'll call "count"
  const [count, setCount] = useState(0);
  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>Click me</button>
    </div>
  );
}
```

In React 16.8 we can use state without creating a class

**What is a Hook?** A Hook is a special function that lets you “hook into” React features. For example, useState is a Hook that lets you add React state to function components. We’ll learn other Hooks later.

**What does calling useState do?** It declares a “state variable”, This is a way to “preserve” some values between the function calls — useState is a new way to use the exact same capabilities that this.state provides in a class.

**What do we pass to useState as an argument?** The only argument to the useState() Hook is the initial state. Unlike with classes, the state doesn’t have to be an object. We can keep a number or a string if that’s all we need.

**What does useState return?** It returns a pair of values: the current state and a function that updates it.

- Effect Hook

The Effect Hook, useEffect, adds the ability to perform side effects from a function component. It serves the same purpose as `componentDidMount`, `componentDidUpdate`, and `componentWillUnmount` in React classes, but unified into a single API.

```javascript
import React, { useState, useEffect } from 'react';
function Example() {
  const [count, setCount] = useState(0);

  // Similar to componentDidMount and componentDidUpdate:
  useEffect(() => {
    // Update the document title using the browser API
    document.title = `You clicked ${count} times`;
  });
  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>Click me</button>
    </div>
  );
}
```
