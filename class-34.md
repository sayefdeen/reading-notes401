# <Login /> and <Auth />

## Review, Research, and Discussion

- Why is the Context API useful?

Well it is very useful when we need to define a global state that we can use in each components without the need to have a relation between those components

- Can a component outside of a provider get its context?

Yes, by importing the context to that component

- What are some common use cases for using the Context API?

For Authentication, to make sure that the user is registered or not each time the user is trying to do something in the website .

- Describe “Context Hell”

---

## Vocabulary Terms

- **global state** : It is a state that can be accessed/updated from any component in the application

- **global context** : A set of methods/function or states that can be accessed from any component in the application without the need for the relation between these components

- **provider** : Its a React context that will provide some methods/states to the whole application as global

- **consumer** : It is a React component that is using the the context provider.

---

## Preparation Materials

Role-based access control (RBAC) restricts network access based on a person's role within an organization and has become one of the main methods for advanced access control. **The roles in RBAC refer to the levels of access that employees have to the network.**

Access can be based on several factors, such as authority, responsibility, and job competency. In addition, access to computer resources can be limited to specific tasks such as the ability to view, create, or modify a file.

### Benefits of RBAC

- Reducing administrative work and IT support

- Maximizing operational efficiency

- Improving compliance.

### Best Practices for Implementing RBAC

- **Current Status:** Create a list of every software, hardware and app that has some sort of security.

- **Current Roles:** Even if you do not have a formal roster and list of roles, determining what each individual team member does may only take a little discussion.

- **Write a Policy:** Any changes made need to be written for all current and future employees to see.

- **Make Changes:**Once the current security status and roles are understood, it’s time to make the changes.

- **Continually Adapt:** It’s likely that the first iteration of RBAC will require some tweaking. Early on, you should evaluate your roles and security status frequently.

The RBAC Could be achieved in React by using this npm package, To be able to access user cookies while doing server-rendering,

[react-cookies](https://www.npmjs.com/package/react-cookies)

```cmd
npm i react-cookies
```

```javascript
import { Component } from 'react';
import cookie from 'react-cookies';

import LoginPanel from './LoginPanel';
import Dashboard from './Dashboard';

class MyApp extends Component {
  constructor() {
    super();

    this.onLogin = this.onLogin.bind(this);
    this.onLogout = this.onLogout.bind(this);
  }

  componentWillMount() {
    this.state = { userId: cookie.load('userId') };
  }

  onLogin(userId) {
    this.setState({ userId });
    cookie.save('userId', userId, { path: '/' });
  }

  onLogout() {
    cookie.remove('userId', { path: '/' });
  }

  render() {
    const { userId } = this.state;

    if (!userId) {
      return <LoginPanel onSuccess={this.onLogin} />;
    }

    return <Dashboard userId={userId} />;
  }
}
```
