# Routing

## Review, Research, and Discussion

- Do child components have direct access to props/state from the parent?

The Child have an access to the parent state throw the props.

- When a component “wraps” another component, how does the child component’s output get rendered?

```javascript
<Main>
  <Content />
</Main>
```

- Can a component, such as <Content />, which is a child also be used as a standalone component elsewhere in the application?

- What trick can a parent use to share all props with it’s children

Make the parent warp the child before execution

## Vocabulary Terms

- **props.children** : It is an array of objects containing all the markup children that the component has warped

- **composition** : is a natural pattern of the component model. It's how we build components from other components, of varying complexity and specialization through props. Depending on how generalized these components are, they can be used in building many other components.

## Preparation Materials

### React Router V4

React Router v4 is a pure React rewrite of the popular React package. Previous versions of React Router used configuration disguised as pseudo-components and could be difficult to understand. With v4, everything is **just components**

1. Installation

```cmd
npm install --save react-router-dom
```

For browser based projects, there are **BrowserRouter** and **HashRouter** components.

- **BrowserRouter** : should be used when you have a server that will handle dynamic requests (knows how to respond to any possible URI).

- **HashRouter** : should be used for static websites (where the server can only respond to requests for files that it knows about).

2. Rendering a Router

Router components only expect to receive a single child element. To work within this limitation, it is useful to create an `<App>` component that renders the rest of your application. Separating your application from the router is also useful for server rendering because you can re-use the `<App>` on the server while switching the router to a MemoryRouter.

```javascript
import { BrowserRouter } from 'react-router-dom';

ReactDOM.render(
  <BrowserRouter>
    <App />
  </BrowserRouter>,
  document.getElementById('root')
);
```

```javascript
// this component will be rendered by our <___Router>
function App() {
  return (
    <div>
      <Header />
      <Main />
    </div>
  );
}
```

3. Routes

The `<Route>` component is the main building block of React Router. Anywhere that you want to only render content based on the location’s pathname, you should use a `<Route>` element.

Note: When it comes to matching routes, React Router only cares about the pathname of a location. That means that given the URL:

```
http://www.example.com/my-projects/one?extra=false
```

the only part that React Router attempts to match is /my-projects/one.

```javascript
<Route path='/roster'/>
// when the pathname is '/', the path does not match
// when the pathname is '/roster' or '/roster/2', the path matches
// If you only want to match '/roster', then you need to use
// the "exact" prop. The following will match '/roster', but not
// '/roster/2'.
<Route exact path='/roster'/>
```

What does the `<Route>` render?

- component — A React component. When a route with a component prop matches, the route will return a new element whose type is the provided React component (created using React.createElement).

- render — A function that returns a React element 5. It will be called when the path matches. This is similar to component, but is useful for inline rendering and passing extra props to the element.

- children — A function that returns a React element. Unlike the prior two props, this will always be rendered, regardless of whether the route’s path matches the current location.
