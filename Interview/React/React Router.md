---
tags:
  - ReactJs
Date: 2024-10-12
Title: React Router
References:
  - https://github.com/sudheerj/reactjs-interview-questions
---
## React Router

79. ### What is React Router?
    React Router is a powerful routing library built on top of React that helps you add new screens and flows to your application incredibly quickly, all while keeping the URL in sync with what's being displayed on the page.

80. ### How React Router is different from history library?

  

    React Router is a wrapper around the `history` library which handles interaction with the browser's `window.history` with its browser and hash histories. It also provides memory history which is useful for environments that don't have global history, such as mobile app development (React Native) and unit testing with Node.

  



  

81. ### What are the `<Router>` components of React Router v6?

  

    React Router v6 provides below 4 `<Router>` components:

  

    1.  `<BrowserRouter>`:Uses the HTML5 history API for standard web apps.

    2.  `<HashRouter>`:Uses hash-based routing for static servers.

    3.  `<MemoryRouter>`:Uses in-memory routing for testing and non-browser environments.

    4.  `<StaticRouter>`:Provides static routing for server-side rendering (SSR).

  

    The above components will create _browser_, _hash_, _memory_ and _static_ history instances. React Router v6 makes the properties and methods of the `history` instance associated with your router available through the context in the `router` object.

  



  

82. ### What is the purpose of `push()` and `replace()` methods of `history`?

  

    A history instance has two methods for navigation purpose.

  

    1.  `push()`

    2.  `replace()`

  

    If you think of the history as an array of visited locations, `push()` will add a new location to the array and `replace()` will replace the current location in the array with the new one.

  



  

83. ### How do you programmatically navigate using React Router v4?

  

    There are three different ways to achieve programmatic routing/navigation within components.

  

    1.  **Using the `withRouter()` higher-order function:**

  

        The `withRouter()` higher-order function will inject the history object as a prop of the component. This object provides `push()` and `replace()` methods to avoid the usage of context.

  

        ```jsx harmony

        import { withRouter } from "react-router-dom"; // this also works with 'react-router-native'

  

        const Button = withRouter(({ history }) => (

          <button

            type="button"

            onClick={() => {

              history.push("/new-location");

            }}

          >

            {"Click Me!"}

          </button>

        ));

        ```

  

    2.  **Using `<Route>` component and render props pattern:**

  

        The `<Route>` component passes the same props as `withRouter()`, so you will be able to access the history methods through the history prop.

  

        ```jsx harmony

        import { Route } from "react-router-dom";

  

        const Button = () => (

          <Route

            render={({ history }) => (

              <button

                type="button"

                onClick={() => {

                  history.push("/new-location");

                }}

              >

                {"Click Me!"}

              </button>

            )}

          />

        );

        ```

  

    3.  **Using context:**

  

        This option is not recommended and treated as unstable API.

  

        ```jsx harmony

        const Button = (props, context) => (

          <button

            type="button"

            onClick={() => {

              context.history.push("/new-location");

            }}

          >

            {"Click Me!"}

          </button>

        );

  

        Button.contextTypes = {

          history: React.PropTypes.shape({

            push: React.PropTypes.func.isRequired,

          }),

        };

        ```

  



  

84. ### How to get query parameters in React Router v4?

  

    The ability to parse query strings was taken out of React Router v4 because there have been user requests over the years to support different implementation. So the decision has been given to users to choose the implementation they like. The recommended approach is to use query strings library.

  

    ```javascript

    const queryString = require("query-string");

    const parsed = queryString.parse(props.location.search);

    ```

  

    You can also use `URLSearchParams` if you want something native:

  

    ```javascript

    const params = new URLSearchParams(props.location.search);

    const foo = params.get("name");

    ```

  

    You should use a _polyfill_ for IE11.

  



  

85. ### Why you get "Router may have only one child element" warning?

  

    You have to wrap your Route's in a `<Switch>` block because `<Switch>` is unique in that it renders a route exclusively.

  

    At first you need to add `Switch` to your imports:

  

    ```javascript

    import { Switch, Router, Route } from "react-router";

    ```

  

    Then define the routes within `<Switch>` block:

  

    ```jsx harmony

    <Router>

      <Switch>

        <Route {/* ... */} />

        <Route {/* ... */} />

      </Switch>

    </Router>

    ```

  



  

86. ### How to pass params to `history.push` method in React Router v4?

  

    While navigating you can pass props to the `history` object:

  

    ```javascript

    this.props.history.push({

      pathname: "/template",

      search: "?name=sudheer",

      state: { detail: response.data },

    });

    ```

  

    The `search` property is used to pass query params in `push()` method.

  



  

87. ### How to implement _default_ or _NotFound_ page?

  

    A `<Switch>` renders the first child `<Route>` that matches. A `<Route>` with no path always matches. So you just need to simply drop path attribute as below

  

    ```jsx harmony

    <Switch>

      <Route exact path="/" component={Home} />

      <Route path="/user" component={User} />

      <Route component={NotFound} />

    </Switch>

    ```

  



  

88. ### How to get history on React Router v4?

  

    Below are the list of steps to get history object on React Router v4,

  

    1.  Create a module that exports a `history` object and import this module across the project.

  

        For example, create `history.js` file:

  

        ```javascript

        import { createBrowserHistory } from "history";

  

        export default createBrowserHistory({

          /* pass a configuration object here if needed */

        });

        ```

  

    2.  You should use the `<Router>` component instead of built-in routers. Import the above `history.js` inside `index.js` file:

  

        ```jsx harmony

        import { Router } from "react-router-dom";

        import history from "./history";

        import App from "./App";

  

        ReactDOM.render(

          <Router history={history}>

            <App />

          </Router>,

          holder

        );

        ```

  

    3.  You can also use push method of `history` object similar to built-in history object:

  

        ```javascript

        // some-other-file.js

        import history from "./history";

  

        history.push("/go-here");

        ```

  



  

89. ### How to perform automatic redirect after login?

  

    The `react-router` package provides `<Redirect>` component in React Router. Rendering a `<Redirect>` will navigate to a new location. Like server-side redirects, the new location will override the current location in the history stack.

  

    ```javascript

    import { Redirect } from "react-router";

  

    export default function Login {

        if (this.state.isLoggedIn === true) {

          return <Redirect to="/your/redirect/page" />;

        } else {

          return <div>{"Login Please"}</div>;

        }

    }

    ```

  

      <details><summary><b>See Class</b></summary>

      <p>

  

    ```jsx

    import React, { Component } from "react";

    import { Redirect } from "react-router";

  

    export default class LoginComponent extends Component {

      render() {

        if (this.state.isLoggedIn === true) {

          return <Redirect to="/your/redirect/page" />;

        } else {

          return <div>{"Login Please"}</div>;

        }

      }

    }

    ```

  

       </p>

       </details>

  

