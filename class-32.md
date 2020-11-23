# Custom Hooks

## Review

- What does a component’s lifecycle refer to?

it referrer to the steps that all the React component go throw, first the component is created (Mounted on the DOM), Updated , and (unmounted on Dom)

- Why do you sometimes need to wrap functions in `useCallback` when called from within `useEffect`.

To ensure that the logic inside it is invoked when the component in Mounted in to the DOm for an example.

- Why are functional components preferred over class components?

Functional component are much easier to read and test because they are plain JavaScript functions without state or lifecycle-hooks. You end up with less code. They help you to use best practices

- What is wrong with the following code?

```javascript
import React, { useState, useEffect } from 'react';

function MyComponent(props) {
  const [count, setCount] = useState(0);

  function changeCount(e) {
    setCount(e.target.value);
  }

  let renderedItems = [];

  for (let i = 0; i < count; i++) {
    useEffect(() => {
      console.log('component mount/update');
    }, [count]);

    renderedItems.push(<div key={i}>Item</div>);
  }

  return (
    <div>
      <input type='number' value={count} onChange={changeCount} />
      {renderedItems}
    </div>
  );
}
```

Instead of using the for loop to push a new item to the renderedItems array, we can use a state instead, and the for loop will be invoked one time since it is not effected with the update state of the count.

```javascript
useEffect(() => {
  let renderedItems = [];
  for (let i = 0; i < count; i++) {
    console.log('component mount/update');

    renderedItems.push(<div key={i}>Item</div>);
  }
}, [count]);
```

## Vocabulary Terms

- **state hook** : it is a special function (Hook) that let you use React features, for an example we can use the useState hook which let you use the state without creating a react class component.

* **effect hook** : one of React hocks, that let you use the React feature, such as listening when the component is Mounted to the DOM, or some component got updated and so on.

* **reducer hook** : it allows functional components in React access to reducer functions from your state management.

## Preparation Materials

### Hooks

First released in October of 2018, the React hook APIs provide an alternative to writing class-based components, and offer an alternative approach to state management and lifecycle methods.

The side-by-side below shows how the component saved us about five lines of code, and the readability and test-ability also improve with the change over to Hooks.

![Example](https://d585tldpucybw.cloudfront.net/sfimages/default-source/default-album/beforeandafter.gif?sfvrsn=8a30f722_1)

**Five Important Rules for Hooks**

- Never call Hooks from inside a loop, condition or nested function
- Hooks should sit at the top-level of your component
- Only call Hooks from React functional components
- Never call a Hook from a regular function
- Hooks can call other Hooks

### React Hooks with Async-Await

<p style='color:red; font-size:20px'>We cannot use 'async' keyword with 'useEffect' callback method. It will result in race conditions.</p>

```javascript
function useAsyncHook(searchBook) {
  const [result, setResult] = React.useState([]);
  const [loading, setLoading] = React.useState('false');

  React.useEffect(() => {
    async function fetchBookList() {
      try {
        setLoading('true');
        const response = await fetch(
          `https://www.googleapis.com/books/v1/volumes?q=${searchBook}`
        );

        const json = await response.json();
        // console.log(json);
        setResult(
          json.items.map((item) => {
            console.log(item.volumeInfo.title);
            return item.volumeInfo.title;
          })
        );
      } catch (error) {
        setLoading('null');
      }
    }

    if (searchBook !== '') {
      fetchBookList();
    }
  }, [searchBook]);

  return [result, loading];
}
```

React.useEffect method will only run when our 'searchBook' got change, the useEffect function is lesitining on the change of the [searchBook], if it was changed thats mean our useEffect function will be invoked
