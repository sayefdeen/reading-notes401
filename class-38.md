# Redux - Asynchronous Actions

## Review, Research, and Discussion

- How granular should your reducers be?

It depends, since we can separate the reducers for each component if we want to apply an action on that component i don't think that we need to make general for all components

- Pro or Con – multiple reducers can “fire” when a commonly named action is dispatched

Well, it is a Pro more than a Con since we have to change multiple states in multiple components, the fact that all the reducers can listen when the action is dispatched can reduce a lot of work, each reducer can provide a different logic to the same dispatcher.

- Name a strategy for preventing the above

Make a reducer for each component that will be affected by the dispatcher, only effecting a specific amount of the state it self.

## Vocabulary Terms

- **store** : a store holds the whole state tree of the application, the only way to change the state inside it is to dispatch an action on it, it is not a class , just an object with few methods on it.

- **combined reducers** : it is a helper function turns an object whose values are different reducing functions into a single reducing function we can pass to createStore.

## Preparation Materials

### Async Logic and Data Fetching

we can use React-Redux library to let our React components interact with a Redux store, including calling `useSelector` to read Redux state, calling `useDispatch` to give us access to the `dispatch` function, and wrapping our app in a `<Provider>` component to give those hooks access to the store.

By itself, a Redux store doesn't know anything about async logic. It only knows how to synchronously dispatch actions, update the state by calling the root reducer function, and notify the UI that something has changed. Any asynchronicity has to happen outside the store.

### Using Middleware to Enable Async Logic

One possibility is writing a middleware that looks for specific action types, and runs async logic when it sees those actions, like these examples:

```javascript
import { client } from '../api/client';

const delayedActionMiddleware = (storeAPI) => (next) => (action) => {
  if (action.type === 'todos/todoAdded') {
    setTimeout(() => {
      // Delay this action by one second
      next(action);
    }, 1000);
    return;
  }

  return next(action);
};

const fetchTodosMiddleware = (storeAPI) => (next) => (action) => {
  if (action.type === 'todos/fetchTodos') {
    // Make an API call to fetch todos from the server
    client.get('todos').then((todos) => {
      // Dispatch an action with the todos we received
      dispatch({ type: 'todos/todosLoaded', payload: todos });
    });
  }

  return next(action);
};
```

We could have our middleware check to see if the "action" is actually a function instead, and if it's a function, call the function right away. That would let us write async logic in separate functions, outside of the middleware definition.

```javascript
const asyncFunctionMiddleware = (storeAPI) => (next) => (action) => {
  // If the "action" is actually a function instead...
  if (typeof action === 'function') {
    // then call the function and pass `dispatch` and `getState` as arguments
    return action(storeAPI.dispatch, storeAPI.getState);
  }

  // Otherwise, it's a normal action - send it onwards
  return next(action);
};
```

The Middleware is used like this

```javascript
const middlewareEnhancer = applyMiddleware(asyncFunctionMiddleware);
const store = createStore(rootReducer, middlewareEnhancer);

// Write a function that has `dispatch` and `getState` as arguments
const fetchSomeData = (dispatch, getState) => {
  // Make an async HTTP request
  client.get('todos').then((todos) => {
    // Dispatch an action with the todos we received
    dispatch({ type: 'todos/todosLoaded', payload: todos });
    // Check the updated store state after dispatching
    const allTodos = getState().todos;
    console.log('Number of todos after loading: ', allTodos.length);
  });
};

// Pass the _function_ we wrote to `dispatch`
store.dispatch(fetchSomeData);
// logs: 'Number of todos after loading: ###'
```

### Redux Async Data Flow

Just like with a normal action, we first need to handle a user event in the application, such as a click on a button. Then, we call `dispatch()`, and pass in something, whether it be a plain action object, a function, or some other value that a middleware can look for.

Once that dispatched value reaches a middleware, it can make an async call, and then dispatch a real action object when the async call completes.

### Redux Thunk

Thunk middleware for Redux

```cmd
npm install redux-thunk
```

With a plain basic Redux store, you can only do simple synchronous updates by dispatching an action. Middleware extends the store's abilities, and lets you write async logic that interacts with the store.

Thunks are the recommended middleware for basic Redux side effects logic, including complex synchronous logic that needs access to the store, and simple async logic like AJAX requests.

Redux Thunk middleware allows you to write action creators that return a function instead of an action. The thunk can be used to delay the dispatch of an action, or to dispatch only if a certain condition is met. The inner function receives the store methods `dispatch` and `getState` as parameters.
