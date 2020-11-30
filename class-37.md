# Redux - Combined Reducers

## Review, Research, and Discussion

- Why choose Redux instead of the Context API for global state?

The idea of redux is, to have one state for the entire project that it is represented with an object, all the components have access to this state and can be affected when the state it self gonna change.

- What is the purpose of a reducer?

It is a function that will control the actions how they affect the state.

- What does an action contain?

It is a function that returns an object that contain this :

```javascript
{
    type: "" //A string that represent the type of the action
    payload: // for an example the thing that gonna change in the state
}
```

- Why do we need to copy the state in a reducer?

We have to keep out initial state untouched, so we can go back for it whenever we want, and each time we dispatch an action a new state will return to a specific component.

---

## Vocabulary Terms

- **immutable state** : A term that is used in Redux which means that we can't change the state directly, we have to use dispatchers (actions).

- **time travel in redux** : is the ability to move back and forth among the previous states of an application and view the results in real time.

- **action creator** : it is a function that returns an action object.

- **reducer** : a function that will control all the actions and how they affect the state, it will return a new state

- **dispatch** : The Redux store has a method called dispatch. The only way to update the state is to call store.dispatch() and pass in an action object.

---

## Preparation Materials

### Combine reducers

the most common approach to writing reducer logic for that state shape is to have "slice reducer" functions, each with the same `(state, action)` signature, and each responsible for managing all updates to that specific slice of state. Multiple slice reducers can respond to the same action, independently update their own slice as needed, and the updated slices are combined into the new state object.

Because this pattern is so common, Redux provides the `combineReducers` utility to implement that behavior. It is an example of a higher-order reducer, which takes an object full of slice reducer functions, and returns a new reducer function.

`combineReducers` : a utility function to simplify the most common use case when writing Redux reducers.

Since `combineReducers` is wrapping all the reducers dose it call all the reducer when an action is called, well no it does not in order toi assemble the new state tree, `combineReducers` will call each slice reducer with it is current slice of state and the current action, giving the slice reducer a chance to respond and update it's slice of state if needed.

```javascript
// reducers.js
export default theDefaultReducer = (state = 0, action) => state;

export const firstNamedReducer = (state = 1, action) => state;

export const secondNamedReducer = (state = 2, action) => state;

// rootReducer.js
import { combineReducers, createStore } from 'redux';

import theDefaultReducer, {
  firstNamedReducer,
  secondNamedReducer
} from './reducers';

const rootReducer = combineReducers({
  theDefaultReducer,
  firstNamedReducer,
  secondNamedReducer
});

const store = createStore(rootReducer);
console.log(store.getState());
// {theDefaultReducer : 0, firstNamedReducer : 1, secondNamedReducer : 2}
```
