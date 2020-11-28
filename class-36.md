# Application State with Redux.

## Review, Research, and Discussion

- What are the advantages of storing tokens in “Cookies” vs “Local Storage”

Cookies can be access from the server-side and the client-side either, but local storage it can only be accessed from the client-side.

- Explain 3rd party cookies.

created by domains other than the one you are visiting directly, hence the name third-party. They are used for cross-site tracking, re-targeting and ad-serving.

- How do pixel tags work?

A tracking pixel (also called 1x1 pixel or pixel tag) is a graphic with dimensions of 1x1 pixels that is loaded when a user visits a webpage or opens an email. Because it is so small, it can hardly be seen by visitors of a website or email recipients.

```html
<img style="“position: absolute;" src="“Tracking" />
<img style="“display: none”;" src="“Tracking" />
<img src="“Tracking" width="“0”" height="“0”" />
```

The website operator or sender of an email adds the tracking pixel using a code in the website’s HTML code or email. This code contains an external link to the pixel server. If a user visits the destination website, the HTML code is processed by the client – usually the user’s browser. The browser follows the link and opens the (invisible) graphic. This is registered and noted in the server’s log files.

## Vocabulary Terms

- **cookies** : it is a small amount of data that is stored in the user's computer by the web browser while browsing a website.

- **authorization** : is a security mechanism to determine access levels or user/client privileges related to system resources including files, services, computer programs, data and application features.

- **access control** : is a method of guaranteeing that users are who they say they are and that they have the appropriate access to company data.

- **conditional rendering** :the ability to render different UI markup based on certain conditions.

## Preparation Materials

### Redux

Redux is a predictable state container for JavaScript apps.

### Installation

```cmd
# NPM
npm install @reduxjs/toolkit

# Yarn
yarn add @reduxjs/toolkit
```

### Create a REact Redux App

```cmd
npx create-react-app my-app --template redux
```

### Redux Core

The Redux core library is available as a package on NPM for use with a module bundler or in a Node application:

```cmd
# NPM
npm install redux

# Yarn
yarn add redux
```

The whole global state of your app is stored in an object tree inside a single store. The only way to change the state tree is to create an action, an object describing what happened, and dispatch it to the store. To specify how state gets updated in response to an action, you write pure reducer functions that calculate a new state based on the old state and the action.

```javascript
import { createStore } from 'redux';

function counterReducer(state = { value: 0 }, action) {
  switch (action.type) {
    case 'counter/incremented':
      return { value: state.value + 1 };
    case 'counter/decremented':
      return { value: state.value - 1 };
    default:
      return state;
  }
}

let store = createStore(counterReducer);

store.subscribe(() => console.log(store.getState()));

store.dispatch({ type: 'counter/incremented' });
// {value: 1}
store.dispatch({ type: 'counter/incremented' });
// {value: 2}
store.dispatch({ type: 'counter/decremented' });
// {value: 1}
```

Instead of mutating the state directly, you specify the mutations you want to happen with plain objects called actions. Then you write a special function called a reducer to decide how every action transforms the entire application's state.

### Principles of Redux.

1. Represent the whole state of the application with a single JavaScript Object called the state tree

2. The state tree is reeducate you can't write on it or modify it, each change should be a dispatching action that represented with a JavaScript object that at least have type:'String' property.

3. each state should be represented with a pure function that holds the previous state condition, the dispatching action, and the next state
