---
tags:
  - ReactJs
  - Interview-Prep
Date: 2024-06-16
Title: Core React Interview Questions
References:
  - https://github.com/sudheerj/reactjs-interview-questions
---
## Core React

1.  ### What is React?
   
    React is a front-end and ==open-source JavaScript library== which is useful in developing user interfaces specifically for applications with a [single page](obsidian://open?vault=knowledge-vault&file=Interview%2FMisc%2FSPA%20vs%20MPA). It is helpful in building complex and reusable user interface(UI) components of mobile and web applications as it follows the component-based approach.

	The important features of React are:
	
	- It supports [server-side rendering](obsidian://open?vault=knowledge-vault&file=Programming%2FReactJs%2FServer%20Side%20Rendering).
	- It will make use of the virtual DOM rather than real DOM (Data Object Model) as RealDOM manipulations are expensive.
	- It follows unidirectional data binding or data flow.
	- It uses reusable UI components for developing the view.
---
2.  ### ~~What is the history behind React evolution?~~

    The history of ReactJS started in 2010 with the creation of **XHP**. XHP is a PHP extension which improved the syntax of the language such that XML document fragments become valid PHP expressions and the primary purpose was used to create custom and reusable HTML elements.

    The main principle of this extension was to make front-end code easier to understand and to help avoid cross-site scripting attacks. The project was successful to prevent the malicious content submitted by the scrubbing user.

    **Note:** JSX comes from the idea of XHP
---

3.  ### What are the major features of React?

    The major features of React are:

    - Uses **JSX** syntax, a syntax extension of JS that allows developers to write HTML in their JS code.
    - It uses **Virtual DOM** instead of Real DOM considering that Real DOM manipulations are expensive.
    - Supports [**server-side rendering**](obsidian://open?vault=knowledge-vault&file=Programming%2FReactJs%2FServer%20Side%20Rendering) which is useful for Search Engine Optimizations(SEO).
    - Follows **Unidirectional or one-way** data flow or data binding.
    - Uses **reusable/composable** UI components to develop the view.
---

4.  ### What is JSX?

    _JSX_ stands for ==_JavaScript XML_== and it is an XML-like syntax extension to ECMAScript. Basically it just provides the syntactic sugar for the `React.createElement(type, props, ...children)` function, giving us expressiveness of JavaScript along with HTML like template syntax.

    In the example below, the text inside `<h1>` tag is returned as JavaScript function to the render function.

    ```jsx harmony
    export default function App() {
      return <h1 className="greeting">{"Hello, this is a JSX Code!"}</h1>;
    }
    ```

    If you don't use JSX syntax then the respective JavaScript code should be written as below,

    ```javascript
    import { createElement } from "react";

    export default function App() {
      return createElement(
        "h1",
        { className: "greeting" },
        "Hello, this is a JSX Code!"
      );
    }
    ```

     <details><summary><b>See Class</b></summary>
     <p>

    ```jsx harmony
    class App extends React.Component {
      render() {
        return <h1 className="greeting">{"Hello, this is a JSX Code!"}</h1>;
      }
    }
    ```

     </p>
     </details>

    **Note:** JSX is stricter than HTML
---

5.  ### What is the difference between Element and Component?

    In React, **elements** and **components** are fundamental building blocks, but they serve different purposes. Here's a breakdown of each:
	
	##### 1. **React Element**
	- **Definition:** A React element is a plain object that describes what you want to see on the UI. It is the smallest building block in React and represents a DOM node or a component.
	- **Creation:** React elements are typically created using JSX syntax or `React.createElement()`.
	- **Immutability:** React elements are immutable. Once an element is created, you cannot modify its attributes or children.
	- **Rendering:** An element is directly rendered into the DOM via methods like `ReactDOM.render()`.
	  
	**Example:**
	```jsx
	const element = <h1>Hello, World!</h1>;
	```
	In this case, `<h1>Hello, World!</h1>` is a React element that describes an `h1` DOM node.
	
	##### 2. **React Component**
	- **Definition:** A React component is a JavaScript function or class that optionally accepts input (called "props") and returns a React element describing what should appear on the screen. Components are reusable, and they allow you to split the UI into independent, reusable pieces.
	- **Types:**
	  - **Function Component:** A JavaScript function that returns a React element.
	  - **Class Component:** A JavaScript class that extends `React.Component` and must have a `render` method that returns a React element.
	- **State and Lifecycle:** Components can manage internal state (especially class components or with hooks in function components) and handle lifecycle events.
	- **Reusability:** Components can be reused throughout the application, allowing for modular, maintainable code.
	  
	**Example:**
	
	- **Function Component:**
	  ```jsx
	  function Welcome(props) {
	    return <h1>Hello, {props.name}!</h1>;
	  }
	  ```
	
	- **Class Component:**
	  ```jsx
	  class Welcome extends React.Component {
	    render() {
	      return <h1>Hello, {this.props.name}!</h1>;
	    }
	  }
	  ```
	
	##### **Key Differences**
	
	| **Aspect**          | **React Element**                                        | **React Component**                                     |
	|---------------------|----------------------------------------------------------|---------------------------------------------------------|
	| **Definition**       | Plain object describing the UI.                          | A function or class that returns a React element.        |
	| **Creation**         | Created using JSX or `React.createElement()`.            | Defined as functions or classes.                        |
	| **Reusability**      | Not reusable.                                            | Highly reusable and can be used in multiple places.      |
	| **State Management** | Cannot manage state or lifecycle events.                 | Can manage state and handle lifecycle events.            |
	| **Rendering**        | Directly rendered into the DOM.                          | Returns elements that describe what to render.           |
	| **Purpose**          | Defines what is shown on the UI.                         | Defines how UI is structured, reused, and behaves.       |
	| **Immutability**     | Immutable once created.                                  | Components can be dynamic (due to state or props).       |

---
6.  ### How to create components in React?

    Components are the building blocks of creating User Interfaces(UI) in React. There are two possible ways to create a component.

    1. **Function Components:** This is the simplest way to create a component. Those are pure JavaScript functions that accept props object as the one and only one parameter and return React elements to render the output:

       ```jsx harmony
       function Greeting({ message }) {
         return <h1>{`Hello, ${message}`}</h1>;
       }
       ```

    2. **Class Components:** You can also use ES6 class to define a component. The above function component can be written as a class component:

       ```jsx harmony
       class Greeting extends React.Component {
         render() {
           return <h1>{`Hello, ${this.props.message}`}</h1>;
         }
       }
       ```
---

7.  ### When to use a Class Component over a Function Component?

	 *With the present version of React, we can achieve everything with the function components*
    After the addition of Hooks(i.e. React 16.8 onwards) it is always recommended to use Function components over Class components in React. Because you could use state, lifecycle methods and other features that were only available in class component present in function component too.

    But even there are two reasons to use Class components over Function components.

    1. If you need a React functionality whose Function component equivalent is not present yet, like Error Boundaries.
    2. In older versions, If the component needs _state or lifecycle methods_ then you need to use class component.

    So the summary to this question is as follows:

    **Use Function Components:**

    - If you don't need state or lifecycle methods, and your component is purely presentational.
    - For simplicity, readability, and modern code practices, especially with the use of React Hooks for state and side effects.

    **Use Class Components:**

    - If you need to manage state or use lifecycle methods.
    - In scenarios where backward compatibility or integration with older code is necessary.

    **Note:** You can also use reusable [react error boundary](https://github.com/bvaughn/react-error-boundary) third-party component without writing any class. i.e, No need to use class components for Error boundaries.

    The usage of Error boundaries from the above library is quite straight forward.

    > **_Note when using react-error-boundary:_** ErrorBoundary is a client component. You can only pass props to it that are serializable or use it in files that have a `"use client";` directive.

    ```jsx
    "use client";

    import { ErrorBoundary } from "react-error-boundary";

    <ErrorBoundary fallback={<div>Something went wrong</div>}>
      <ExampleApplication />
    </ErrorBoundary>;
    ```
---

8.  ### What are Pure Components?

    Pure components are the components which render the same output for the same state and props. In function components, you can achieve these pure components through memoized `React.memo()`. This API prevents unnecessary re-renders by comparing the previous props and new props using shallow comparison. So it will be helpful for performance optimizations.

    But at the same time, it won't compare the previous state with the current state because function component itself prevents the unnecessary rendering by default when you set the same state again.

    The syntactic representation of memoized components looks like below,

    ```jsx
    const MemoizedComponent = memo(SomeComponent, arePropsEqual?);
    ```

    Below is the example of how child component(i.e., EmployeeProfile) prevents re-renders for the same props passed by parent component(i.e.,EmployeeRegForm).

    ```jsx
    import { memo, useState } from "react";

    const EmployeeProfile = memo(function EmployeeProfile({ name, email }) {
      return (
        <>
          <p>Name:{name}</p>
          <p>Email: {email}</p>
        </>
      );
    });
    export default function EmployeeRegForm() {
      const [name, setName] = useState("");
      const [email, setEmail] = useState("");
      return (
        <>
          <label>
            Name:{" "}
            <input value={name} onChange={(e) => setName(e.target.value)} />
          </label>
          <label>
            Email:{" "}
            <input value={email} onChange={(e) => setEmail(e.target.value)} />
          </label>
          <hr />
          <EmployeeProfile name={name} />
        </>
      );
    }
    ```

    In the above code, the email prop has not been passed to child component. So there won't be any re-renders for email prop change.

    In class components, the components extending _`React.PureComponent`_ instead of _`React.Component`_ become the pure components. When props or state changes, _PureComponent_ will do a ==shallow comparison==(i.e object are checked for their references note their actual content) on both props and state by invoking `shouldComponentUpdate()` lifecycle method.

    **Note:** `React.memo()` is a high-order component.
---

9.  ### What is state in React?

    In React, **state** is an object that represents the dynamic data in a component. It is used to store values that may change over time and control how the component behaves or renders. Whenever the state changes, React re-renders the component to reflect the new state in the UI.
    ![state](assets/images/react-state.jpg)

    Let's take an example of **User** component with `message` state. Here, **useState** hook has been used to add state to the User component and it returns an array with current state and function to update it.

    ```jsx harmony
    import { useState } from "react";

    function User() {
      const [message, setMessage] = useState("Welcome to React world");

      return (
        <div>
          <h1>{message}</h1>
        </div>
      );
    }
    ```

    Whenever React calls your component or access `useState` hook, it gives you a snapshot of the state for that particular render.

    <details><summary><b>See Class</b></summary>
    <p>

    ```jsx harmony
    import React from "react";
    class User extends React.Component {
      constructor(props) {
        super(props);

        this.state = {
          message: "Welcome to React world",
        };
      }

      render() {
        return (
          <div>
            <h1>{this.state.message}</h1>
          </div>
        );
      }
    }
    ```

    </p>
    </details>

    State is similar to props, but it is private and fully controlled by the component ,i.e., it is not accessible to any other component till the owner component decides to pass it.

---

10. ### What are props in React?

    In React, **props** (short for "properties") are a way to pass data from a parent component to a child component. They are used to configure and customize components, making them reusable and dynamic. Unlike **state**, which is managed within a component, props are passed down the component tree and cannot be modified by the receiving component.
    
    ##### Example of Props in React:
	Consider a simple button component that can be customized using props:
	##### 1. **Parent Component:**
	```javascript
		import React from "react";
		import Button from "./Button";
		function App() {
		  return (
		    <div>
		      {" "}
		      <Button label="Submit" color="blue" />{" "}
		      <Button label="Cancel" color="red" />{" "}
		    </div>
		  );
		}
		export default App;
	```
	#### 2. **Child Component (Button):**
	```javascript
		import React from "react";
		function Button(props) {
		  return (
		    <button style={{ backgroundColor: props.color }}> {props.label} </button>
		  );
		}
		export default Button;
	```
	Here, the parent component (`App`) passes two props (`label` and `color`) to the `Button` component. The `Button` component then renders a button element with the `label` as its content and the `color` as its background color.

---

11. ### What is the difference between state and props?
	Props vs State in React
	
	| **Aspect**           | **Props**                                                          | **State**                                                                                                 |
	| -------------------- | ------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------- |
	| **Data Source**      | Passed from parent to child.                                       | Managed within the component itself.                                                                      |
	| **Mutability**       | Immutable (read-only).                                             | Mutable (can be changed using `setState` or hooks).                                                       |
	| **Responsibility**   | Managed by the parent component.                                   | Managed internally by the component.                                                                      |
	| **Usage**            | Used to pass data, functions, and configuration.                   | Used to manage dynamic, local data within the component.                                                  |
	| **Re-rendering**     | Changing props in the parent re-renders the child.                 | State changes trigger a re-render in the same component.                                                  |
	| **Default Behavior** | Passed as arguments to child components.                           | Initialized inside the component and can be updated over time.                                            |
	| **Modifiability**    | Cannot be modified by the receiving component.                     | Can be updated via `setState` in class components or hooks in functional components.                      |
	| **Common Use**       | Ideal for customizing child components and passing event handlers. | Best for managing data that changes over time, like form inputs or UI elements based on user interaction. |

---

12. ### What is the difference between HTML and React event handling?

    Below are some of the main differences between HTML and React event handling,

    1. In HTML, the event name usually represents in _lowercase_ as a convention:

       ```html
       <button onclick="activateLasers()"></button>
       ```

       Whereas in React it follows _camelCase_ convention:

       ```jsx harmony
       <button onClick={activateLasers}>
       ```

    2. In HTML, you can return `false` to prevent default behavior:

       ```html
       <a
         href="#"
         onclick='console.log("The link was clicked."); return false;'
       />
       ```

       Whereas in React you must call `preventDefault()` explicitly:

       ```javascript
       function handleClick(event) {
         event.preventDefault();
         console.log("The link was clicked.");
       }
       ```

    3. In HTML, you need to invoke the function by appending `()`
       Whereas in react you should not append `()` with the function name. (refer "activateLasers" function in the first point for example)

    

13. ### What are synthetic events in React?

    `SyntheticEvent` is a cross-browser wrapper around the browser's native event. Its API is same as the browser's native event, including `stopPropagation()` and `preventDefault()`, except the events work identically across all browsers. The native events can be accessed directly from synthetic events using `nativeEvent` attribute.

    Let's take an example of BookStore title search component with the ability to get all native event properties

    ```js
    function BookStore() {
      function handleTitleChange(e) {
        console.log("The new title is:", e.target.value);
        // 'e' represents synthetic event
        const nativeEvent = e.nativeEvent;
        console.log(nativeEvent);
        e.stopPropagation();
        e.preventDefault();
      }

      return <input name="title" onChange={handleTitleChange} />;
    }
    ```

    

14. ### What are inline conditional expressions?

    You can use either _if statements_ or _ternary expressions_ which are available from JS to conditionally render expressions. Apart from these approaches, you can also embed any expressions in JSX by wrapping them in curly braces and then followed by JS logical operator `&&`.

    ```jsx harmony
    <h1>Hello!</h1>;
    {
      messages.length > 0 && !isLogin ? (
        <h2>You have {messages.length} unread messages.</h2>
      ) : (
        <h2>You don't have unread messages.</h2>
      );
    }
    ```

    

15. ### What is "key" prop and what is the benefit of using it in arrays of elements?

    A `key` is a special attribute you **should** include when mapping over arrays to render data. _Key_ prop helps React identify which items have changed, are added, or are removed.

    Keys should be unique among its siblings. Most often we use ID from our data as _key_:

    ```jsx harmony
    const todoItems = todos.map((todo) => <li key={todo.id}>{todo.text}</li>);
    ```

    When you don't have stable IDs for rendered items, you may use the item _index_ as a _key_ as a last resort:

    ```jsx harmony
    const todoItems = todos.map((todo, index) => (
      <li key={index}>{todo.text}</li>
    ));
    ```

    **Note:**

    1. Using _indexes_ for _keys_ is **not recommended** if the order of items may change. This can negatively impact performance and may cause issues with component state.
    2. If you extract list item as separate component then apply _keys_ on list component instead of `li` tag.
    3. There will be a warning message in the console if the `key` prop is not present on list items.
    4. The key attribute accepts either string or number and internally convert it as string type.
    5. Don't generate the key on the fly something like `key={Math.random()}`. Because the keys will never match up between re-renders and DOM created everytime.

    

16. ### What is Virtual DOM?

    The _Virtual DOM_ (VDOM) is an in-memory representation of _Real DOM_. The representation of a UI is kept in memory and synced with the "real" DOM. It's a step that happens between the render function being called and the displaying of elements on the screen. This entire process is called _reconciliation_.

    

17. ### How Virtual DOM works?

    The _Virtual DOM_ works in three simple steps.

    1. Whenever any underlying data changes, the entire UI is re-rendered in Virtual DOM representation.

       ![vdom](images/vdom1.png)

    2. Then the difference between the previous DOM representation and the new one is calculated.

       ![vdom2](images/vdom2.png)

    3. Once the calculations are done, the real DOM will be updated with only the things that have actually changed.

       ![vdom3](images/vdom3.png)

    

18. ### What is the difference between Shadow DOM and Virtual DOM?

    The _Shadow DOM_ is a browser technology designed primarily for scoping variables and CSS in _web components_. The _Virtual DOM_ is a concept implemented by libraries in JavaScript on top of browser APIs.

    

19. ### What is React Fiber?

    Fiber is the new _reconciliation_ engine or reimplementation of core algorithm in React v16. The goal of React Fiber is to increase its suitability for areas like animation, layout, gestures, ability to pause, abort, or reuse work and assign priority to different types of updates; and new concurrency primitives.

    

20. ### What is the main goal of React Fiber?

    The goal of _React Fiber_ is to increase its suitability for areas like animation, layout, and gestures. Its headline feature is **incremental rendering**: the ability to split rendering work into chunks and spread it out over multiple frames.

    _from documentation_

    Its main goals are:

    1. Ability to split interruptible work in chunks.
    2. Ability to prioritize, rebase and reuse work in progress.
    3. Ability to yield back and forth between parents and children to support layout in React.
    4. Ability to return multiple elements from render().
    5. Better support for error boundaries.

    

21. ### What are controlled components?

    A component that controls the input elements within the forms on subsequent user input is called **Controlled Component**, i.e, every state mutation will have an associated handler function. That means, the displayed data is always in sync with the state of the component.

    The controlled components will be implemented using the below steps,

    1. Initialize the state using use state hooks in function components or inside constructor for class components.
    2. Set the value of the form element to the respective state variable.
    3. Create an event handler to handle the user input changes through useState updater function or setState from class component.
    4. Attach the above event handler to form elements change or click events

    For example, the name input field updates the user name using `handleChange` event handler as below,

    ```javascript
    import React, { useState } from "react";

    function UserProfile() {
      const [username, setUsername] = useState("");

      const handleChange = (e) => {
        setUsername(e.target.value);
      };

      return (
        <form>
          <label>
            Name:
            <input type="text" value={username} onChange={handleChange} />
          </label>
        </form>
      );
    }
    ```

    

22. ### What are uncontrolled components?

    The **Uncontrolled Components** are the ones that store their own state internally, and you query the DOM using a ref to find its current value when you need it. This is a bit more like traditional HTML.

    The uncontrolled components will be implemented using the below steps,

    1. Create a ref using useRef react hook in function component or `React.createRef()` in class based component.
    2. Attach this ref to the form element.
    3. The form element value can be accessed directly through `ref` in event handlers or `componentDidMount` for class components

    In the below UserProfile component, the `username` input is accessed using ref.

    ```jsx harmony
    import React, { useRef } from "react";

    function UserProfile() {
      const usernameRef = useRef(null);

      const handleSubmit = (event) => {
        event.preventDefault();
        console.log("The submitted username is: " + usernameRef.current.value);
      };

      return (
        <form onSubmit={handleSubmit}>
          <label>
            Username:
            <input type="text" ref={usernameRef} />
          </label>
          <button type="submit">Submit</button>
        </form>
      );
    }
    ```

    In most cases, it's recommend to use controlled components to implement forms. In a controlled component, form data is handled by a React component. The alternative is uncontrolled components, where form data is handled by the DOM itself.

    <details><summary><b>See Class</b></summary>
    <p>

    ```jsx harmony
    class UserProfile extends React.Component {
      constructor(props) {
        super(props);
        this.handleSubmit = this.handleSubmit.bind(this);
        this.input = React.createRef();
      }

      handleSubmit(event) {
        alert("A name was submitted: " + this.input.current.value);
        event.preventDefault();
      }

      render() {
        return (
          <form onSubmit={this.handleSubmit}>
            <label>
              {"Name:"}
              <input type="text" ref={this.input} />
            </label>
            <input type="submit" value="Submit" />
          </form>
        );
      }
    }
    ```

    </p>
    </details>

    

23. ### What is the difference between createElement and cloneElement?

    JSX elements will be transpiled to `React.createElement()` functions to create React elements which are going to be used for the object representation of UI. Whereas `cloneElement` is used to clone an element and pass it new props.

    

24. ### What is Lifting State Up in React?

    When several components need to share the same changing data then it is recommended to _lift the shared state up_ to their closest common ancestor. That means if two child components share the same data from its parent, then move the state to parent instead of maintaining local state in both of the child components.

    

25. ### What are Higher-Order Components?

    A _higher-order component_ (_HOC_) is a function that takes a component and returns a new component. Basically, it's a pattern that is derived from React's compositional nature.

    We call them **pure components** because they can accept any dynamically provided child component but they won't modify or copy any behavior from their input components.

    ```javascript
    const EnhancedComponent = higherOrderComponent(WrappedComponent);
    ```

    HOC can be used for many use cases:

    1. Code reuse, logic and bootstrap abstraction.
    2. Render hijacking.
    3. State abstraction and manipulation.
    4. Props manipulation.

    

26. ### What is children prop?

    _Children_ is a prop that allows you to pass components as data to other components, just like any other prop you use. Component tree put between component's opening and closing tag will be passed to that component as `children` prop.

    A simple usage of children prop looks as below,

    ```jsx harmony
    function MyDiv({ children }){
        return (
          <div>
            {children}
          </div>;
        );
    }

    export default function Greeting() {
      return (
        <MyDiv>
          <span>{"Hello"}</span>
          <span>{"World"}</span>
        </MyDiv>
      );
    }
    ```

    <details><summary><b>See Class</b></summary>
    <p>

    ```jsx harmony
    const MyDiv = React.createClass({
      render: function () {
        return <div>{this.props.children}</div>;
      },
    });

    ReactDOM.render(
      <MyDiv>
        <span>{"Hello"}</span>
        <span>{"World"}</span>
      </MyDiv>,
      node
    );
    ```

    </p>
    </details>

    **Note:** There are several methods available in the legacy React API to work with this prop. These include `React.Children.map`, `React.Children.forEach`, `React.Children.count`, `React.Children.only`, `React.Children.toArray`.

    

27. ### How to write comments in React?

    The comments in React/JSX are similar to JavaScript Multiline comments but are wrapped in curly braces.

    **Single-line comments:**

    ```jsx harmony
    <div>
      {/* Single-line comments(In vanilla JavaScript, the single-line comments are represented by double slash(//)) */}
      {`Welcome ${user}, let's play React`}
    </div>
    ```

    **Multi-line comments:**

    ```jsx harmony
    <div>
      {/* Multi-line comments for more than
       one line */}
      {`Welcome ${user}, let's play React`}
    </div>
    ```

    

28. ### What is reconciliation?

    `Reconciliation` is the process through which React updates the Browser DOM and makes React work faster. React use a `diffing algorithm` so that component updates are predictable and faster. React would first calculate the difference between the `real DOM` and the copy of DOM `(Virtual DOM)` when there's an update of components.
    React stores a copy of Browser DOM which is called `Virtual DOM`. When we make changes or add data, React creates a new Virtual DOM and compares it with the previous one. This comparison is done by `Diffing Algorithm`.
    Now React compares the Virtual DOM with Real DOM. It finds out the changed nodes and updates only the changed nodes in Real DOM leaving the rest nodes as it is. This process is called _Reconciliation_.

    

29. ### Does the lazy function support named exports?

    No, currently `React.lazy` function supports default exports only. If you would like to import modules which are named exports, you can create an intermediate module that reexports it as the default. It also ensures that tree shaking keeps working and don’t pull unused components.
    Let's take a component file which exports multiple named components,

    ```javascript
    // MoreComponents.js
    export const SomeComponent = /* ... */;
    export const UnusedComponent = /* ... */;
    ```

    and reexport `MoreComponents.js` components in an intermediate file `IntermediateComponent.js`

    ```javascript
    // IntermediateComponent.js
    export { SomeComponent as default } from "./MoreComponents.js";
    ```

    Now you can import the module using lazy function as below,

    ```javascript
    import React, { lazy } from "react";
    const SomeComponent = lazy(() => import("./IntermediateComponent.js"));
    ```

    

30. ### Why React uses `className` over `class` attribute?

    The attribute names written in JSX turned into keys of JavaScript objects and the JavaScript names cannot contain dashes or reversed words, it is recommended to use camelCase wherever applicable in JSX code. The attribute `class` is a keyword in JavaScript, and JSX is an extension of JavaScript. That's the principle reason why React uses `className` instead of `class`. Pass a string as the `className` prop.

    ```jsx harmony
    render() {
      return <span className="menu navigation-menu">{'Menu'}</span>
    }
    ```

    

31. ### What are fragments?

    It's a common pattern or practice in React for a component to return multiple elements. _Fragments_ let you group a list of children without adding extra nodes to the DOM.
    You need to use either `<Fragment>` or a shorter syntax having empty tag (`<></>`).

    Below is the example of how to use fragment inside _Story_ component.

    ```jsx harmony
    function Story({ title, description, date }) {
      return (
        <Fragment>
          <h2>{title}</h2>
          <p>{description}</p>
          <p>{date}</p>
        </Fragment>
      );
    }
    ```

    It is also possible to render list of fragments inside a loop with the mandatory **key** attribute supplied.

    ```jsx harmony
    function StoryBook() {
      return stories.map((story) => (
        <Fragment key={story.id}>
          <h2>{story.title}</h2>
          <p>{story.description}</p>
          <p>{story.date}</p>
        </Fragment>
      ));
    }
    ```

    Usually, you don't need to use `<Fragment>` until there is a need of _key_ attribute. The usage of shorter syntax looks like below.

    ```jsx harmony
    function Story({ title, description, date }) {
      return (
        <>
          <h2>{title}</h2>
          <p>{description}</p>
          <p>{date}</p>
        </>
      );
    }
    ```

    

32. ### Why fragments are better than container divs?

    Below are the list of reasons to prefer fragments over container DOM elements,

    1. Fragments are a bit faster and use less memory by not creating an extra DOM node. This only has a real benefit on very large and deep trees.
    2. Some CSS mechanisms like _Flexbox_ and _CSS Grid_ have a special parent-child relationships, and adding divs in the middle makes it hard to keep the desired layout.
    3. The DOM Inspector is less cluttered.

    

33. ### What are portals in React?

    _Portal_ is a recommended way to render children into a DOM node that exists outside the DOM hierarchy of the parent component. When using
    CSS transform in a component, its descendant elements should not use fixed positioning, otherwise the layout will blow up.

    ```javascript
    ReactDOM.createPortal(child, container);
    ```

    The first argument is any render-able React child, such as an element, string, or fragment. The second argument is a DOM element.

    

34. ### What are stateless components?

    If the behaviour of a component is independent of its state then it can be a stateless component. You can use either a function or a class for creating stateless components. But unless you need to use a lifecycle hook in your components, you should go for function components. There are a lot of benefits if you decide to use function components here; they are easy to write, understand, and test, a little faster, and you can avoid the `this` keyword altogether.

    

35. ### What are stateful components?

    If the behaviour of a component is dependent on the _state_ of the component then it can be termed as stateful component. These _stateful components_ are either function components with hooks or _class components_.

    Let's take an example of function stateful component which update the state based on click event,

    ```javascript
    import React, {useState} from 'react';

    const App = (props) => {
    const [count, setCount] = useState(0);
    handleIncrement() {
      setCount(count+1);
    }

    return (
      <>
        <button onClick={handleIncrement}>Increment</button>
        <span>Counter: {count}</span>
      </>
      )
    }
    ```

    <details><summary><b>See Class</b></summary>
    <p>
    The equivalent class stateful component with a state that gets initialized in the `constructor`.

    ```jsx harmony
    class App extends Component {
      constructor(props) {
        super(props);
        this.state = { count: 0 };
      }

      handleIncrement() {
        setState({ count: this.state.count + 1 });
      }

      render() {
        <>
          <button onClick={() => this.handleIncrement}>Increment</button>
          <span>Count: {count}</span>
        </>;
      }
    }
    ```

    </p>
    </details>

    

36. ### How to apply validation on props in React?

    When the application is running in _development mode_, React will automatically check all props that we set on components to make sure they have _correct type_. If the type is incorrect, React will generate warning messages in the console. It's disabled in _production mode_ due to performance impact. The mandatory props are defined with `isRequired`.

    The set of predefined prop types:

    1. `PropTypes.number`
    2. `PropTypes.string`
    3. `PropTypes.array`
    4. `PropTypes.object`
    5. `PropTypes.func`
    6. `PropTypes.node`
    7. `PropTypes.element`
    8. `PropTypes.bool`
    9. `PropTypes.symbol`
    10. `PropTypes.any`

    We can define `propTypes` for `User` component as below:

    ```jsx harmony
    import React from "react";
    import PropTypes from "prop-types";

    class User extends React.Component {
      static propTypes = {
        name: PropTypes.string.isRequired,
        age: PropTypes.number.isRequired,
      };

      render() {
        return (
          <>
            <h1>{`Welcome, ${this.props.name}`}</h1>
            <h2>{`Age, ${this.props.age}`}</h2>
          </>
        );
      }
    }
    ```

    **Note:** In React v15.5 _PropTypes_ were moved from `React.PropTypes` to `prop-types` library.

    _The Equivalent Functional Component_

    ```jsx harmony
    import React from "react";
    import PropTypes from "prop-types";

    function User({ name, age }) {
      return (
        <>
          <h1>{`Welcome, ${name}`}</h1>
          <h2>{`Age, ${age}`}</h2>
        </>
      );
    }

    User.propTypes = {
      name: PropTypes.string.isRequired,
      age: PropTypes.number.isRequired,
    };
    ```

    

37. ### What are the advantages of React?

    Below are the list of main advantages of React,

    1. Increases the application's performance with _Virtual DOM_.
    2. JSX makes code easy to read and write.
    3. It renders both on client and server side (_SSR_).
    4. Easy to integrate with frameworks (Angular, Backbone) since it is only a view library.
    5. Easy to write unit and integration tests with tools such as Jest.

    

38. ### What are the limitations of React?

    Apart from the advantages, there are few limitations of React too,

    1. React is just a view library, not a full framework.
    2. There is a learning curve for beginners who are new to web development.
    3. Integrating React into a traditional MVC framework requires some additional configuration.
    4. The code complexity increases with inline templating and JSX.
    5. Too many smaller components leading to over engineering or boilerplate.

    

39. ### What are the recommended ways for static type checking?

    Normally we use _PropTypes library_ (`React.PropTypes` moved to a `prop-types` package since React v15.5) for _type checking_ in the React applications. For large code bases, it is recommended to use _static type checkers_ such as Flow or TypeScript, that perform type checking at compile time and provide auto-completion features.

    

40. ### What is the use of `react-dom` package?

    The `react-dom` package provides _DOM-specific methods_ that can be used at the top level of your app. Most of the components are not required to use this module. Some of the methods of this package are:

    1. `render()`
    2. `hydrate()`
    3. `unmountComponentAtNode()`
    4. `findDOMNode()`
    5. `createPortal()`

    

41. ### What is ReactDOMServer?

    The `ReactDOMServer` object enables you to render components to static markup (typically used on node server). This object is mainly used for _server-side rendering_ (SSR). The following methods can be used in both the server and browser environments:

    1. `renderToString()`
    2. `renderToStaticMarkup()`

    For example, you generally run a Node-based web server like Express, Hapi, or Koa, and you call `renderToString` to render your root component to a string, which you then send as response.

    ```javascript
    // using Express
    import { renderToString } from "react-dom/server";
    import MyPage from "./MyPage";

    app.get("/", (req, res) => {
      res.write(
        "<!DOCTYPE html><html><head><title>My Page</title></head><body>"
      );
      res.write('<div id="content">');
      res.write(renderToString(<MyPage />));
      res.write("</div></body></html>");
      res.end();
    });
    ```

    

42. ### How to use innerHTML in React?

    The `dangerouslySetInnerHTML` attribute is React's replacement for using `innerHTML` in the browser DOM. Just like `innerHTML`, it is risky to use this attribute considering cross-site scripting (XSS) attacks. You just need to pass a `__html` object as key and HTML text as value.

    In this example MyComponent uses `dangerouslySetInnerHTML` attribute for setting HTML markup:

    ```jsx harmony
    function createMarkup() {
      return { __html: "First &middot; Second" };
    }

    function MyComponent() {
      return <div dangerouslySetInnerHTML={createMarkup()} />;
    }
    ```

    

43. ### How to use styles in React?

    The `style` attribute accepts a JavaScript object with camelCased properties rather than a CSS string. This is consistent with the DOM style JavaScript property, is more efficient, and prevents XSS security holes.

    ```jsx harmony
    const divStyle = {
      color: "blue",
      backgroundImage: "url(" + imgUrl + ")",
    };

    function HelloWorldComponent() {
      return <div style={divStyle}>Hello World!</div>;
    }
    ```

    Style keys are camelCased in order to be consistent with accessing the properties on DOM nodes in JavaScript (e.g. `node.style.backgroundImage`).

    

44. ### How events are different in React?

    Handling events in React elements has some syntactic differences:

    1. React event handlers are named using camelCase, rather than lowercase.
    2. With JSX you pass a function as the event handler, rather than a string.

    

45. ### What is the impact of indexes as keys?

    Keys should be stable, predictable, and unique so that React can keep track of elements.

    In the below code snippet each element's key will be based on ordering, rather than tied to the data that is being represented. This limits the optimizations that React can do and creates confusing bugs in the application.

    ```jsx harmony
    {
      todos.map((todo, index) => <Todo {...todo} key={index} />);
    }
    ```

    If you use element data for unique key, assuming `todo.id` is unique to this list and stable, React would be able to reorder elements without needing to reevaluate them as much.

    ```jsx harmony
    {
      todos.map((todo) => <Todo {...todo} key={todo.id} />);
    }
    ```

    **Note:** If you don't specify `key` prop at all, React will use index as a key's value while iterating over an array of data.

    

46. ### How do you conditionally render components?

    In some cases you want to render different components depending on some state. JSX does not render `false` or `undefined`, so you can use conditional _short-circuiting_ to render a given part of your component only if a certain condition is true.

    ```jsx harmony
    const MyComponent = ({ name, address }) => (
      <div>
        <h2>{name}</h2>
        {address && <p>{address}</p>}
      </div>
    );
    ```

    If you need an `if-else` condition then use _ternary operator_.

    ```jsx harmony
    const MyComponent = ({ name, address }) => (
      <div>
        <h2>{name}</h2>
        {address ? <p>{address}</p> : <p>{"Address is not available"}</p>}
      </div>
    );
    ```

    

47. ### Why we need to be careful when spreading props on DOM elements?

    When we _spread props_ we run into the risk of adding unknown HTML attributes, which is a bad practice. Instead we can use prop destructuring with `...rest` operator, so it will add only required props.

    For example,

    ```jsx harmony
    const ComponentA = () => (
      <ComponentB isDisplay={true} className={"componentStyle"} />
    );

    const ComponentB = ({ isDisplay, ...domProps }) => (
      <div {...domProps}>{"ComponentB"}</div>
    );
    ```

    

48. ### How do you memoize a component?

    There are memoize libraries available which can be used on function components.

    For example `moize` library can memoize the component in another component.

    ```jsx harmony
    import moize from "moize";
    import Component from "./components/Component"; // this module exports a non-memoized component

    const MemoizedFoo = moize.react(Component);

    const Consumer = () => {
      <div>
        {"I will memoize the following entry:"}
        <MemoizedFoo />
      </div>;
    };
    ```

    **Update:** Since React v16.6.0, we have a `React.memo`. It provides a higher order component which memoizes component unless the props change. To use it, simply wrap the component using React.memo before you use it.

    ```js
    const MemoComponent = React.memo(function MemoComponent(props) {
      /* render using props */
    });
    OR;
    export default React.memo(MyFunctionComponent);
    ```

    

49. ### How you implement Server Side Rendering or SSR?

    React is already equipped to handle rendering on Node servers. A special version of the DOM renderer is available, which follows the same pattern as on the client side.

    ```jsx harmony
    import ReactDOMServer from "react-dom/server";
    import App from "./App";

    ReactDOMServer.renderToString(<App />);
    ```

    This method will output the regular HTML as a string, which can be then placed inside a page body as part of the server response. On the client side, React detects the pre-rendered content and seamlessly picks up where it left off.

    

50. ### How to enable production mode in React?

    You should use Webpack's `DefinePlugin` method to set `NODE_ENV` to `production`, by which it strip out things like propType validation and extra warnings. Apart from this, if you minify the code, for example, Uglify's dead-code elimination to strip out development only code and comments, it will drastically reduce the size of your bundle.

    

51. ### Do Hooks replace render props and higher order components?

    Both render props and higher-order components render only a single child but in most of the cases Hooks are a simpler way to serve this by reducing nesting in your tree.

    

52. ### What is a switching component?

    A _switching component_ is a component that renders one of many components. We need to use object to map prop values to components.

    For example, a switching component to display different pages based on `page` prop:

    ```jsx harmony
    import HomePage from "./HomePage";
    import AboutPage from "./AboutPage";
    import ServicesPage from "./ServicesPage";
    import ContactPage from "./ContactPage";

    const PAGES = {
      home: HomePage,
      about: AboutPage,
      services: ServicesPage,
      contact: ContactPage,
    };

    const Page = (props) => {
      const Handler = PAGES[props.page] || ContactPage;

      return <Handler {...props} />;
    };

    // The keys of the PAGES object can be used in the prop types to catch dev-time errors.
    Page.propTypes = {
      page: PropTypes.oneOf(Object.keys(PAGES)).isRequired,
    };
    ```

    

53. ### What are React Mixins?

    _Mixins_ are a way to totally separate components to have a common functionality. Mixins **should not be used** and can be replaced with _higher-order components_ or _decorators_.

    One of the most commonly used mixins is `PureRenderMixin`. You might be using it in some components to prevent unnecessary re-renders when the props and state are shallowly equal to the previous props and state:

    ```javascript
    const PureRenderMixin = require("react-addons-pure-render-mixin");

    const Button = React.createClass({
      mixins: [PureRenderMixin],
      // ...
    });
    ```

     <!-- TODO: mixins are deprecated -->

    

54. ### What are the Pointer Events supported in React?

    _Pointer Events_ provide a unified way of handling all input events. In the old days we had a mouse and respective event listeners to handle them but nowadays we have many devices which don't correlate to having a mouse, like phones with touch surface or pens. We need to remember that these events will only work in browsers that support the _Pointer Events_ specification.

    The following event types are now available in _React DOM_:

    1. `onPointerDown`
    2. `onPointerMove`
    3. `onPointerUp`
    4. `onPointerCancel`
    5. `onGotPointerCapture`
    6. `onLostPointerCapture`
    7. `onPointerEnter`
    8. `onPointerLeave`
    9. `onPointerOver`
    10. `onPointerOut`

    

55. ### Why should component names start with capital letter?

    If you are rendering your component using JSX, the name of that component has to begin with a capital letter otherwise React will throw an error as an unrecognized tag. This convention is because only HTML elements and SVG tags can begin with a lowercase letter.

    ```jsx harmony
    function SomeComponent {
      // Code goes here
    }
    ```

    You can define function component whose name starts with lowercase letter, but when it's imported it should have a capital letter. Here lowercase is fine:

    ```jsx harmony
    function myComponent {
      render() {
        return <div />;
      }
    }

    export default myComponent;
    ```

    While when imported in another file it should start with capital letter:

    ```jsx harmony
    import MyComponent from "./myComponent";
    ```

    

56. ### Are custom DOM attributes supported in React v16?

    Yes. In the past, React used to ignore unknown DOM attributes. If you wrote JSX with an attribute that React doesn't recognize, React would just skip it.

    For example, let's take a look at the below attribute:

    ```jsx harmony
    <div mycustomattribute={"something"} />
    ```

    Would render an empty div to the DOM with React v15:

    ```html
    <div />
    ```

    In React v16 any unknown attributes will end up in the DOM:

    ```html
    <div mycustomattribute="something" />
    ```

    This is useful for supplying browser-specific non-standard attributes, trying new DOM APIs, and integrating with opinionated third-party libraries.

    

57. ### How to loop inside JSX?

    You can simply use `Array.prototype.map` with ES6 _arrow function_ syntax.

    For example, the `items` array of objects is mapped into an array of components:

    ```jsx harmony
    <tbody>
      {items.map((item) => (
        <SomeComponent key={item.id} name={item.name} />
      ))}
    </tbody>
    ```

    But you can't iterate using `for` loop:

    ```jsx harmony
    <tbody>
      for (let i = 0; i < items.length; i++) {
        <SomeComponent key={items[i].id} name={items[i].name} />
      }
    </tbody>
    ```

    This is because JSX tags are transpiled into _function calls_, and you can't use statements inside expressions. This may change thanks to `do` expressions which are _stage 1 proposal_.

    

58. ### How do you access props in attribute quotes?

    React (or JSX) doesn't support variable interpolation inside an attribute value. The below representation won't work:

    ```jsx harmony
    <img className="image" src="images/{this.props.image}" />
    ```

    But you can put any JS expression inside curly braces as the entire attribute value. So the below expression works:

    ```jsx harmony
    <img className="image" src={"images/" + this.props.image} />
    ```

    Using _template strings_ will also work:

    ```jsx harmony
    <img className="image" src={`images/${this.props.image}`} />
    ```

    

59. ### What is React proptype array with shape?

    If you want to pass an array of objects to a component with a particular shape then use `React.PropTypes.shape()` as an argument to `React.PropTypes.arrayOf()`.

    ```javascript
    ReactComponent.propTypes = {
      arrayWithShape: React.PropTypes.arrayOf(
        React.PropTypes.shape({
          color: React.PropTypes.string.isRequired,
          fontSize: React.PropTypes.number.isRequired,
        })
      ).isRequired,
    };
    ```

    

60. ### How to conditionally apply class attributes?

    You shouldn't use curly braces inside quotes because it is going to be evaluated as a string.

    ```jsx harmony
    <div className="btn-panel {this.props.visible ? 'show' : 'hidden'}">
    ```

    Instead you need to move curly braces outside (don't forget to include spaces between class names):

    ```jsx harmony
    <div className={'btn-panel ' + (this.props.visible ? 'show' : 'hidden')}>
    ```

    _Template strings_ will also work:

    ```jsx harmony
    <div className={`btn-panel ${this.props.visible ? 'show' : 'hidden'}`}>
    ```

    

61. ### What is the difference between React and ReactDOM?

    The `react` package contains `React.createElement()`, `React.Component`, `React.Children`, and other helpers related to elements and component classes. You can think of these as the isomorphic or universal helpers that you need to build components. The `react-dom` package contains `ReactDOM.render()`, and in `react-dom/server` we have _server-side rendering_ support with `ReactDOMServer.renderToString()` and `ReactDOMServer.renderToStaticMarkup()`.

    

62. ### Why ReactDOM is separated from React?

    The React team worked on extracting all DOM-related features into a separate library called _ReactDOM_. React v0.14 is the first release in which the libraries are split. By looking at some of the packages, `react-native`, `react-art`, `react-canvas`, and `react-three`, it has become clear that the beauty and essence of React has nothing to do with browsers or the DOM.

    To build more environments that React can render to, React team planned to split the main React package into two: `react` and `react-dom`. This paves the way to writing components that can be shared between the web version of React and React Native.

    

63. ### How to use React label element?

    If you try to render a `<label>` element bound to a text input using the standard `for` attribute, then it produces HTML missing that attribute and prints a warning to the console.

    ```jsx harmony
    <label for={'user'}>{'User'}</label>
    <input type={'text'} id={'user'} />
    ```

    Since `for` is a reserved keyword in JavaScript, use `htmlFor` instead.

    ```jsx harmony
    <label htmlFor={'user'}>{'User'}</label>
    <input type={'text'} id={'user'} />
    ```

    

64. ### How to combine multiple inline style objects?

    You can use _spread operator_ in regular React:

    ```jsx harmony
    <button style={{ ...styles.panel.button, ...styles.panel.submitButton }}>
      {"Submit"}
    </button>
    ```

    If you're using React Native then you can use the array notation:

    ```jsx harmony
    <button style={[styles.panel.button, styles.panel.submitButton]}>
      {"Submit"}
    </button>
    ```

    

65. ### How to re-render the view when the browser is resized?

    You can use the `useState` hook to manage the width and height state variables, and the `useEffect` hook to add and remove the `resize` event listener. The `[]` dependency array passed to useEffect ensures that the effect only runs once (on mount) and not on every re-render.

    ```javascript
    import React, { useState, useEffect } from "react";
    function WindowDimensions() {
      const [dimensions, setDimensions] = useState({
        width: window.innerWidth,
        height: window.innerHeight,
      });

      useEffect(() => {
        function handleResize() {
          setDimensions({
            width: window.innerWidth,
            height: window.innerHeight,
          });
        }
        window.addEventListener("resize", handleResize);
        return () => window.removeEventListener("resize", handleResize);
      }, []);

      return (
        <span>
          {dimensions.width} x {dimensions.height}
        </span>
      );
    }
    ```

    <details>
    <summary><h4>Using Class Component</h4></summary>

    You can listen to the `resize` event in `componentDidMount()` and then update the dimensions (`width` and `height`). You should remove the listener in `componentWillUnmount()` method.

    ```javascript
    class WindowDimensions extends React.Component {
      constructor(props) {
        super(props);
        this.updateDimensions = this.updateDimensions.bind(this);
      }

      componentWillMount() {
        this.updateDimensions();
      }

      componentDidMount() {
        window.addEventListener("resize", this.updateDimensions);
      }

      componentWillUnmount() {
        window.removeEventListener("resize", this.updateDimensions);
      }

      updateDimensions() {
        this.setState({
          width: window.innerWidth,
          height: window.innerHeight,
        });
      }

      render() {
        return (
          <span>
            {this.state.width} x {this.state.height}
          </span>
        );
      }
    }
    ```

    </details>



66. ### How to pretty print JSON with React?

    We can use `<pre>` tag so that the formatting of the `JSON.stringify()` is retained:

    ```jsx harmony
    const data = { name: "John", age: 42 };

    function User {
        return <pre>{JSON.stringify(data, null, 2)}</pre>;
    }

    const container = createRoot(document.getElementById("container"));

    container.render(<User />);
    ```

      <details><summary><b>See Class</b></summary>
      <p>

    ```jsx harmony
    const data = { name: "John", age: 42 };

    class User extends React.Component {
      render() {
        return <pre>{JSON.stringify(data, null, 2)}</pre>;
      }
    }

    React.render(<User />, document.getElementById("container"));
    ```

      </p>
      </details>



67. ### Why you can't update props in React?

    The React philosophy is that props should be _immutable_(read only) and _top-down_. This means that a parent can send any prop values to a child, but the child can't modify received props.



68. ### How to focus an input element on page load?

    You need to use `useEffect` hook to set focus on input field during page load time for functional component.

    ```jsx harmony
    import React, { useEffect, useRef } from "react";

    const App = () => {
      const inputElRef = useRef(null);

      useEffect(() => {
        inputElRef.current.focus();
      }, []);

      return (
        <div>
          <input defaultValue={"Won't focus"} />
          <input ref={inputElRef} defaultValue={"Will focus"} />
        </div>
      );
    };

    ReactDOM.render(<App />, document.getElementById("app"));
    ```

      <details><summary><b>See Class</b></summary>
      <p>
      You can do it by creating _ref_ for `input` element and using it in `componentDidMount()`:

    ```jsx harmony
    class App extends React.Component {
      componentDidMount() {
        this.nameInput.focus();
      }

      render() {
        return (
          <div>
            <input defaultValue={"Won't focus"} />
            <input
              ref={(input) => (this.nameInput = input)}
              defaultValue={"Will focus"}
            />
          </div>
        );
      }
    }

    ReactDOM.render(<App />, document.getElementById("app"));
    ```

      </p>
      </details>



69. ### How can we find the version of React at runtime in the browser?

    You can use `React.version` to get the version.

    ```jsx harmony
    const REACT_VERSION = React.version;

    ReactDOM.render(
      <div>{`React version: ${REACT_VERSION}`}</div>,
      document.getElementById("app")
    );
    ```



70. ### How to add Google Analytics for React Router?

    Add a listener on the `history` object to record each page view:

    ```javascript
    history.listen(function (location) {
      window.ga("set", "page", location.pathname + location.search);
      window.ga("send", "pageview", location.pathname + location.search);
    });
    ```



71. ### How do you apply vendor prefixes to inline styles in React?

    React _does not_ apply _vendor prefixes_ automatically. You need to add vendor prefixes manually.

    ```jsx harmony
    <div
      style={{
        transform: "rotate(90deg)",
        WebkitTransform: "rotate(90deg)", // note the capital 'W' here
        msTransform: "rotate(90deg)", // 'ms' is the only lowercase vendor prefix
      }}
    />
    ```



72. ### How to import and export components using React and ES6?

    You should use default for exporting the components

    ```jsx harmony
    import User from "user";

    export default function MyProfile {
        return <User type="customer">//...</User>;
    }
    ```

    <details><summary><b>See Class</b></summary>
    <p>
     ```jsx harmony
     import React from "react";
     import User from "user";

    export default class MyProfile extends React.Component {
    render() {
    return <User type="customer">//...</User>;
    }
    }

    ```
    </p>
    </details>

    With the export specifier, the MyProfile is going to be the member and exported to this module and the same can be imported without mentioning the name in other components.
    ```



73. ### What are the exceptions on React component naming?

    The component names should start with an uppercase letter but there are few exceptions to this convention. The lowercase tag names with a dot (property accessors) are still considered as valid component names.
    For example, the below tag can be compiled to a valid component,

    ```jsx harmony
         render() {
              return (
                <obj.component/> // `React.createElement(obj.component)`
              )
        }
    ```

    

74. ### Is it possible to use async/await in plain React?

    If you want to use `async`/`await` in React, you will need _Babel_ and [transform-async-to-generator](https://babeljs.io/docs/en/babel-plugin-transform-async-to-generator) plugin. React Native ships with Babel and a set of transforms.



75. ### What are the common folder structures for React?

    There are two common practices for React project file structure.

    1.  **Grouping by features or routes:**

        One common way to structure projects is locate CSS, JS, and tests together, grouped by feature or route.

        ```
        common/
        ├─ Avatar.js
        ├─ Avatar.css
        ├─ APIUtils.js
        └─ APIUtils.test.js
        feed/
        ├─ index.js
        ├─ Feed.js
        ├─ Feed.css
        ├─ FeedStory.js
        ├─ FeedStory.test.js
        └─ FeedAPI.js
        profile/
        ├─ index.js
        ├─ Profile.js
        ├─ ProfileHeader.js
        ├─ ProfileHeader.css
        └─ ProfileAPI.js
        ```

    2.  **Grouping by file type:**

        Another popular way to structure projects is to group similar files together.

        ```
        api/
        ├─ APIUtils.js
        ├─ APIUtils.test.js
        ├─ ProfileAPI.js
        └─ UserAPI.js
        components/
        ├─ Avatar.js
        ├─ Avatar.css
        ├─ Feed.js
        ├─ Feed.css
        ├─ FeedStory.js
        ├─ FeedStory.test.js
        ├─ Profile.js
        ├─ ProfileHeader.js
        └─ ProfileHeader.css
        ```



76. ### What are the popular packages for animation?

    _React Transition Group_ and _React Motion_ are popular animation packages in React ecosystem.



77. ### What is the benefit of styles modules?

    It is recommended to avoid hard coding style values in components. Any values that are likely to be used across different UI components should be extracted into their own modules.

    For example, these styles could be extracted into a separate component:

    ```javascript
    export const colors = {
      white,
      black,
      blue,
    };

    export const space = [0, 8, 16, 32, 64];
    ```

    And then imported individually in other components:

    ```javascript
    import { space, colors } from "./styles";
    ```



78. ### What are the popular React-specific linters?

    ESLint is a popular JavaScript linter. There are plugins available that analyse specific code styles. One of the most common for React is an npm package called `eslint-plugin-react`. By default, it will check a number of best practices, with rules checking things from keys in iterators to a complete set of prop types.

    Another popular plugin is `eslint-plugin-jsx-a11y`, which will help fix common issues with accessibility. As JSX offers slightly different syntax to regular HTML, issues with `alt` text and `tabindex`, for example, will not be picked up by regular plugins.


