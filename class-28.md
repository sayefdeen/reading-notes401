# Component Composition

- Can a parent component access the state of a child component?

access to a child state that is declared as a functional component (hooks) you can declare a ref in the parent component, then pass it as a ref attribute to the child

- What can be passed along in a prop variable?

its a Javascript object which can have methods or properties.

- How can a child component “know” the state of another component?

by using the props, first it should be passed to the parent after that any child can have access it in the props object

## Vocabulary Terms

- **component props** : components that are passed in the props object from the parent class to any functional components
- **component state** : its the case of what the component is rendered write know.
- **application state** : interface between your data from any kind of backend or local change and the representation of this data with UI-elements in the frontend.

## Preparation Materials

### The Component Lifecycle

By far the most important concept on this list is understanding the component lifecycle. The component lifecycle is exactly what it sounds like: it details the life of a component. Like us, components are born, do some things during their time here on earth, and then they die .

### Mounting

Since class-based components are classes, hence the name, the first method that runs is the constructor method. Typically, the constructor is where you would initialize component state.

Next, the component runs the getDerivedStateFromProps. I’m going to skip this method since it has limited use.

Now we come to the render method which returns your JSX. Now React “mounts” onto the DOM.

Lastly, the componentDidMount method runs. Here is where you would do any asynchronous calls to databases or directly manipulate the DOM if you need. Just like that, our component is born.

### Updating

This phase is triggered every time state or props change. Like in mounting, getDerivedStateFromProps is called (but no constructor this time!).

Next shouldComponentUpdate runs. Here you can compare old props/state with the new set of props/state. You can determine if your component should re-render or not by returning true or false. This can make your web app more efficient by cutting down on extra re-renders. If shouldComponentUpdate returns false, this update cycle ends.

### Unmounting

Our component lived a good life, but all good things must come to an end. The unmounting phase is that last stage of the component lifecycle. When you remove a component from the DOM, React runs componentWillUnmount right before it gets removed. You should use this method to clean up any open connections such as WebSockets or intervals.

### React’s props.children

this.props.children does is that it is used to display whatever you include between the opening and closing tags when invoking a component.

```javascript
const Picture = (props) => {
  return (
    <div>
      <img src={props.src} />
      {props.children}
    </div>
  );
};
```

### Composition vs Inheritance

Props and composition give you all the flexibility you need to customize a component’s look and behavior in an explicit and safe way. Remember that components may accept arbitrary props, including primitive values, React elements, or functions.

If you want to reuse non-UI functionality between components, we suggest extracting it into a separate JavaScript module. The components may import it and use that function, object, or a class, without extending it.
