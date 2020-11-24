# Context API

## Review

- Describe use cases for `useMemo()` and `useReducer()`

  - `useMemo()` : useMemo will only recompute the memoized value when one of the dependencies has changed.
  - `useReducer()` : `useReducer` is usually preferable to `useState` when you have complex state logic that involves multiple sub-values or when the next state depends on the previous one

- Why do custom hooks need the use prefix?
  Hooks are just like a normal function. Its name should always start with `use` so that you can tell at a glance that the rules of Hooks apply to it.
- What do custom hooks usually do?

lets you extract component logic into reusable functions.

- Using any list of custom hooks, research and name one that you think will be useful in your applications

[🍪](https://github.com/craig1123/react-recipes/blob/master/docs/useCookie.md) `useCookie` : Create, read, or delete cookies

- Describe how a hook that fetches API data might work

Well, to make it more generic we will pass the API URL as an argument to this hock, it will contain the basic CRUD RestAPI methods, (Create,Read,Update,Delete), and it should take the setState function and the state it self.

---

## Vocabulary Terms

- **reducer** : a reducer is a function which takes two arguments -- the current state and an action -- and returns based on both arguments a new state.

---

## Preparation Materials

## Context

Context provides a way to pass data through the component tree without having to pass props down manually at every level.

In a typical React application, data is passed top-down (parent to child) via props, but this can be cumbersome for certain types of props that are required by many components within an application.

Context is designed to share data that can be considered “global” for a tree of React components, such as the current authenticated user, theme, or preferred language.

Context is primarily used when some data needs to be accessible by many components at different nesting levels. Apply it sparingly because it makes component reuse more difficult.

If you only want to avoid passing some props through many levels, component composition is often a simpler solution than context.
