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
---

13. ### What are synthetic events in React?

    `SyntheticEvent` is a cross-browser wrapper around the browser's native event. Its API is same as the browser's native event. They are part of the React event system, which is designed to be consistent across all browsers, ensuring that event handling works the same way regardless of the environment.

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
---

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
---

15. ### What is "key" prop and what is the benefit of using it in arrays of elements?

    The **`key`** prop in React is a special attribute used when rendering arrays of elements. It helps React identify which elements have changed, been added, or removed. This is especially important when React re-renders lists of items because it allows React to optimize the update process and avoid unnecessary re-rendering of unchanged elements.

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

---

16. ### What is Virtual DOM?

    The _Virtual DOM_ (VDOM) is an in-memory representation of _Real DOM_. The representation of a UI is kept in memory and synced with the "real" DOM. ==It's a step that happens between the render function being called and the displaying of elements on the screen. This entire process is called _reconciliation_.==

---

17. ### How Virtual DOM works?

    The _Virtual DOM_ works in three simple steps.

    1. Whenever any underlying data changes, the entire UI is re-rendered in Virtual DOM representation.

       ![vdom](images/vdom1.png)

    2. Then the difference between the previous DOM representation and the new one is calculated.

       ![vdom2](images/vdom2.png)

    3. Once the calculations are done, the real DOM will be updated with only the things that have actually changed.

       ![vdom3](images/vdom3.png)

---

18. ### What is the difference between Shadow DOM and Virtual DOM?

    The _Shadow DOM_ is a browser technology designed primarily for scoping variables and CSS in _web components_. The _Virtual DOM_ is a concept implemented by libraries in JavaScript on top of browser APIs.

---

19. ### What is React Fiber?

    Fiber is the new _reconciliation_ engine or reimplementation of core algorithm in React v16. The goal of React Fiber is to increase its suitability for areas like animation, layout, gestures, ability to pause, abort, or reuse work and assign priority to different types of updates; and new concurrency primitives.

---

20. ### What is the main goal of React Fiber?

    The goal of _React Fiber_ is to increase its suitability for areas like animation, layout, and gestures. Its headline feature ==is **incremental rendering**:== the ability to split rendering work into chunks and spread it out over multiple frames.

    _from documentation_

    Its main goals are:

    1. Ability to split interruptible work in chunks.
    2. Ability to prioritize, rebase and reuse work in progress.
    3. Ability to yield back and forth between parents and children to support layout in React.
    4. Ability to return multiple elements from render().
    5. Better support for error boundaries.

    

21. ### What are controlled components?

    In React, **controlled components** are form elements (like `<input>`, `<textarea>`, etc.) where the value is controlled by the component’s state. The input value is derived from the state, and any change is handled by updating the state through an `onChange` handler. This ensures the form input always reflects the React state, providing a "single source of truth" for form data and enabling easier validation and management.

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

---

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
| Feature                 | Controlled Components                               | Uncontrolled Components                          |
|-------------------------|----------------------------------------------------|-------------------------------------------------|
| Value Management        | Managed by React state                             | Managed by the DOM                              |
| Updates                 | Requires `onChange` handler to update state        | Value accessed through `ref`                    |
| State Synchronization   | Always in sync with React state                    | Not automatically synced with state             |
| Use Case                | Ideal for validation and complex form logic        | Simpler for basic forms without validation      |
| Example                 | `<input value={state} onChange={handleChange} />`  | `<input ref={inputRef} />`                      |


---

23. ### What is the difference between createElement and cloneElement?

	| Feature                     | `React.createElement`                                     | `React.cloneElement`                                       |
	|-----------------------------|----------------------------------------------------------|------------------------------------------------------------|
	| Purpose                     | Creates a new React element from scratch.                | Clones an existing React element and allows modifications.  |
	| Parameters                  | Type (component/tag), props, and children.               | Existing element, new props (optional), and new children.   |
	| Use Case                    | Used to create any React element in JSX or JavaScript.    | Used to clone elements, often modifying props or children.  |
	| Example                     | `React.createElement('div', { className: 'box' }, 'Text')` | `React.cloneElement(element, { className: 'new-class' })`   |
	| JSX Equivalent              | `<div className="box">Text</div>`                         | Cloning isn’t directly available in JSX, must use JS.       |
	
	**`createElement`** is for creating new elements, while **`cloneElement`** is for copying and modifying existing ones.

---

24. ### What is Lifting State Up in React?

    **Lifting State Up** in React is a pattern where you move the shared state to a common ancestor component, allowing sibling components to share and sync data through that parent.
	
	Why Use It?
	When multiple components need to share data, lifting the state to their closest common parent ensures that all components have access to the same state and can update it consistently.
	
	Example:
	
	```jsx
	function Parent() {
	  const [sharedValue, setSharedValue] = useState('');
	
	  return (
	    <div>
	      <ChildA value={sharedValue} onChange={setSharedValue} />
	      <ChildB value={sharedValue} />
	    </div>
	  );
	}
	
	function ChildA({ value, onChange }) {
	  return <input value={value} onChange={(e) => onChange(e.target.value)} />;
	}
	
	function ChildB({ value }) {
	  return <p>{value}</p>;
	}
	```
	
	Here, the state (`sharedValue`) is lifted up to the `Parent` component, so both `ChildA` and `ChildB` can access and update it.

---

25. ### What are Higher-Order Components?

    **Higher-Order Components (HOCs)** in React are functions that take a component as an argument and return a new component with enhanced functionality. They allow you to reuse component logic and share behavior across multiple components.

	Key Points:
	- HOCs don’t modify the original component but wrap it in a new one.
	- Commonly used for cross-cutting concerns like adding authentication, logging, or data fetching.
	- They follow the pattern: `const EnhancedComponent = higherOrderComponent(WrappedComponent)`.
	
	### Example:
	
	```jsx
	import React, { useState, useEffect } from 'react';
	
	// UserProfile component to display user data
	function UserProfile({ user }) {
	  return (
	    <div>
	      <h2>{user.name}</h2>
	      <p>Email: {user.email}</p>
	    </div>
	  );
	}
	
	// HOC to handle loading spinner
	function withLoadingSpinner(Component) {
	  return function EnhancedComponent({ isLoading, ...props }) {
	    if (isLoading) {
	      return <div>Loading...</div>;  // Show loading spinner when isLoading is true
	    }
	    return <Component {...props} />;  // Render the original component when isLoading is false
	  };
	}
	
	// Wrapping UserProfile with the HOC
	const UserProfileWithSpinner = withLoadingSpinner(UserProfile);
	
	// Parent component simulating an API call to fetch data
	function App() {
	  const [isLoading, setIsLoading] = useState(true);
	  const [user, setUser] = useState(null);
	
	  useEffect(() => {
	    // Simulate API call with a 2-second delay
	    setTimeout(() => {
	      setUser({ name: 'John Doe', email: 'john.doe@example.com' });
	      setIsLoading(false);  // Stop loading once data is fetched
	    }, 2000);
	  }, []);
	
	  return (
	    <div>
	      {/* Pass isLoading and user as props to the enhanced component */}
	      <UserProfileWithSpinner isLoading={isLoading} user={user} />
	    </div>
	  );
	}
	
	export default App;

	```
	
	Here, `withLoadingSpinner` is an HOC that adds loading behavior to `MyComponent` without altering its original logic.

---

26. ### What is children prop?
	
	The `children` prop in React is a special prop that allows you to pass elements or components as children to a parent component. It is used to create a flexible and reusable component structure, enabling the composition of components by nesting them within one another.
	
	### Key Points:
	- **Implicit Prop**: The `children` prop is automatically passed to every React component. You don't need to explicitly define it in the component's props.
	- **Types of Children**: `children` can be any valid React node, including:
	  - Single or multiple elements (like `<div>`, `<span>`, etc.).
	  - Strings or numbers.
	  - Arrays of elements.
	  - Other components.
	
	### Example:
	
	```jsx
	// Parent component that uses children
	function Wrapper({ children }) {
	  return (
	    <div style={{ border: '2px solid blue', padding: '10px' }}>
	      {children} {/* Render the children here */}
	    </div>
	  );
	}
	
	// Child components
	function App() {
	  return (
	    <Wrapper>
	      <h1>Hello, World!</h1>
	      <p>This is a simple example of using the children prop.</p>
	    </Wrapper>
	  );
	}
	
	export default App;
	```
	
	### Benefits of Using `children`:
	1. **Composition**: It enables building complex UIs by composing simpler components together.
	2. **Reusability**: Components can be reused in different contexts, and the content can be varied by changing the children passed to them.
	3. **Flexibility**: Developers can create components that can accept different types and structures of content.
--- 

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

---

28. ### What is reconciliation?

    `Reconciliation` is the process through which React updates the Browser DOM and makes React work faster. React use a `diffing algorithm` so that component updates are predictable and faster. React would first calculate the difference between the `real DOM` and the copy of DOM `(Virtual DOM)` when there's an update of components.
    React stores a copy of Browser DOM which is called `Virtual DOM`. When we make changes or add data, React creates a new Virtual DOM and compares it with the previous one. This comparison is done by `Diffing Algorithm`.
    Now React compares the Virtual DOM with Real DOM. It finds out the changed nodes and updates only the changed nodes in Real DOM leaving the rest nodes as it is. This process is called _Reconciliation_.

---

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

---

30. ### Why React uses `className` over `class` attribute?

    The attribute names written in JSX turned into keys of JavaScript objects and the JavaScript names cannot contain dashes or reversed words, it is recommended to use camelCase wherever applicable in JSX code. ==The attribute `class` is a keyword== in JavaScript, and JSX is an extension of JavaScript. That's the principle reason why React uses `className` instead of `class`. Pass a string as the `className` prop.

    ```jsx harmony
    render() {
      return <span className="menu navigation-menu">{'Menu'}</span>
    }
    ```

---

31. ### What are fragments?

    It's a common pattern or practice in React for a component to return multiple elements. ==_Fragments_ let you group a list of children without adding extra nodes to the DOM.==
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

---

32. ### Why fragments are better than container divs?

    Below are the list of reasons to prefer fragments over container DOM elements,

    1. Fragments are a bit faster and use less memory by not creating an extra DOM node. This only has a real benefit on very large and deep trees.
    2. Some CSS mechanisms like _Flexbox_ and _CSS Grid_ have a special parent-child relationships, and adding divs in the middle makes it hard to keep the desired layout.
    3. The DOM Inspector is less cluttered.

---

33. ### What are portals in React?

    _Portal_ is a recommended way to render children into a DOM node that exists outside the DOM hierarchy of the parent component. When using
    CSS transform in a component, its descendant elements should not use fixed positioning, otherwise the layout will blow up.

    ```javascript
    ReactDOM.createPortal(child, container);
    ```

    The first argument is any render-able React child, such as an element, string, or fragment. The second argument is a DOM element.
    **Use Cases**:
	- **Modals**: Overlaying content that needs to appear on top of other UI elements.
	- **Tooltips**: Displaying information without being constrained by parent elements.
	- **Notifications**: Consistently showing alerts or messages in a designated area of the screen

---

34. ### What are stateless components?

    **Stateless components** in React are components that do not maintain their own state. They are often referred to as **functional components** and are primarily used for rendering UI based on the props passed to them.

---

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

---

36. ### How to apply validation on props in React?

	You can validate props in React using **PropTypes** or **TypeScript**.
	
	#### 1. Using PropTypes
	
	- **Install**: 
	  ```bash
	  npm install prop-types
	  ```
	- **Example**:
	  ```jsx
	  import React from 'react';
	  import PropTypes from 'prop-types';
	
	  const Greeting = ({ name, age }) => {
	    return <h1>Hello, {name}! You are {age} years old.</h1>;
	  };
	
	  Greeting.propTypes = {
	    name: PropTypes.string.isRequired, // required string
	    age: PropTypes.number                // optional number
	  };
	
	  export default Greeting;
	  ```
	
	#### 2. Using TypeScript
	
	- **Example**:
	  ```tsx
	  import React from 'react';
	
	  interface GreetingProps {
	    name: string;  // required string
	    age?: number;  // optional number
	  }
	
	  const Greeting: React.FC<GreetingProps> = ({ name, age }) => {
	    return <h1>Hello, {name}! You are {age ? age : "unknown"} years old.</h1>;
	  };
	
	  export default Greeting;
	  ```
	
	### Summary
	
	- **PropTypes**: Runtime validation; useful for quick checks.
	- **TypeScript**: Compile-time validation; provides stronger type safety.
---

37. ### What are the advantages of React?

    Below are the list of main advantages of React,
	1. **Component-Based Architecture**: Promotes modularity and reusability, making maintenance easier.
	2. **Virtual DOM**: Optimizes rendering for faster updates and improved performance.
	3. **Unidirectional Data Flow**: Simplifies data management and debugging.
	4. **Declarative Syntax**: Enhances readability and understanding of UI code.
	5. **Strong Community Support**: Provides extensive resources, libraries, and tools.
	6. **Rich Ecosystem**: Easily integrates with libraries like Redux and React Router.
	7. **Performance Optimization**: Features like code splitting and lazy loading improve load times.
	8. **Cross-Platform Development**: React Native allows code reuse for mobile applications.
	9. **Developer Tools**: Excellent debugging tools facilitate inspection and optimization.
	10. **Backward Compatibility**: Enables upgrades without significant refactoring.

---

38. ### What are the limitations of React?

    Apart from the advantages, there are few limitations of React too,
	1. **SEO Limitations**: Client-side rendering can hinder search engine indexing, affecting SEO unless server-side rendering is used.
	2. **Learning Curve**: Advanced concepts like hooks and context API can be challenging for beginners.
	3. **Performance Issues**: Unoptimized components may lead to unnecessary re-renders, impacting performance.
	4. **Boilerplate Code**: Initial setup can involve a lot of boilerplate, especially when integrating with libraries.
	5. **Rapidly Changing Ecosystem**: Frequent updates and changes can be overwhelming to keep up with.
	6. **State Management**: Managing global state can become complex, requiring additional libraries.
	7. **Tooling Fragmentation**: The vast ecosystem may lead to decision fatigue when selecting tools and libraries.
	8. **JSX Syntax**: JSX can be unfamiliar and may pose a learning curve for new developers.

---

39. ### What are the recommended ways for static type checking?

    Normally we use _PropTypes library_ (`React.PropTypes` moved to a ==`prop-types`== package since React v15.5) for _type checking_ in the React applications. For large code bases, it is recommended to use _static type checkers_ such as Flow or ==TypeScript==, that perform type checking at compile time and provide auto-completion features.

---

40. ### What is the use of `react-dom` package?

    The `react-dom` package provides _DOM-specific methods_ that can be used at the top level of your app. Most of the components are not required to use this module. Some of the methods of this package are:

    1. `render()`
    2. `hydrate()`
    3. `unmountComponentAtNode()`
    4. `findDOMNode()`
    5. `createPortal()`

---

41. ### What is ReactDOMServer?

    `ReactDOMServer` is a module in React that provides methods to render React components to static markup (HTML) on the server side. This enables server-side rendering (SSR), which allows web applications to send fully rendered HTML pages to clients, improving initial load times and SEO.

    1. `renderToString()`
    2. `renderToStaticMarkup()`

    For example, you generally run a Node-based web server like Express, Hapi, or Koa, and you call `renderToString` to render your root component to a string, which you then send as response.

    ```javascript
    // server.js
	import express from 'express';
	import React from 'react';
	import ReactDOMServer from 'react-dom/server';
	import Hello from './Hello'; // Import the Hello component
	
	const app = express();
	
	app.get('/', (req, res) => {
	    // Render the Hello component to a string
	    const html = ReactDOMServer.renderToString(<Hello />);
	    
	    // Send the rendered HTML as the response
	    res.send(`
	        <!DOCTYPE html>
	        <html>
	            <head>
	                <title>Server-Side Rendering Example</title>
	            </head>
	            <body>
	                <div id="root">${html}</div>
	                <script src="client.js"></script> <!-- Client-side bundle for hydration -->
	            </body>
	        </html>
	    `);
	});
	
	// Start the server
	app.listen(3000, () => {
	    console.log('Server is running on http://localhost:3000');
	});

    ```

--- 

42. ### How to use innerHTML in React?

    Using `innerHTML` in React allows you to set HTML content directly within a component. However, it should be used cautiously to avoid security risks, such as Cross-Site Scripting (XSS) attacks. Here’s how to use `innerHTML` in React:

	### Example of Using `innerHTML` in React
	
	1. **Basic Usage**: You can set `innerHTML` using the `dangerouslySetInnerHTML` prop, which is the official way to set HTML in React.
	
	#### Step 1: Create a React Component
	
	Here's a simple example of a component that uses `dangerouslySetInnerHTML`.
	
	```jsx
	// MyComponent.js
	import React from 'react';
	
	const MyComponent = () => {
	    const htmlContent = '<h1>Hello, <strong>World!</strong></h1><p>This is rendered using <code>dangerouslySetInnerHTML</code>.</p>';
	
	    return (
	        <div>
	            <div dangerouslySetInnerHTML={{ __html: htmlContent }} />
	        </div>
	    );
	};
	
	export default MyComponent;
	```
	
	### Step 2: Use the Component
		
	### Important Considerations
	
	1. **Security Risks**: Using `dangerouslySetInnerHTML` can expose your application to XSS attacks if the HTML content comes from an untrusted source. Always sanitize user-generated content before rendering it.
	
	2. **Escaping Content**: If you're just displaying text and want to prevent HTML from being rendered, it's better to use curly braces (`{}`) to escape content.

---

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

---

44. ### How events are different in React?

    Handling events in React elements has some syntactic differences:

    1. React event handlers are named using camelCase, rather than lowercase.
    2. With JSX you pass a function as the event handler, rather than a string.

---

45. ### What is the impact of indexes as keys?

    ==Keys should be stable, predictable, and unique so that React can keep track of elements.==

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

---

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

---

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

---

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

---

49. ### How you implement Server Side Rendering or SSR?

    React is already equipped to handle rendering on Node servers. A special version of the DOM renderer is available, which follows the same pattern as on the client side.

    ```jsx harmony
    import ReactDOMServer from "react-dom/server";
    import App from "./App";

    ReactDOMServer.renderToString(<App />);
    ```

    This method will output the regular HTML as a string, which can be then placed inside a page body as part of the server response. On the client side, React detects the pre-rendered content and seamlessly picks up where it left off.
	Or we can use react frameworks like Next.Js(recommended)

---

50. ### How to enable production mode in React?

    You should use Webpack's `DefinePlugin` method to set `NODE_ENV` to `production`, by which it strip out things like propType validation and extra warnings. Apart from this, if you minify the code, for example, Uglify's dead-code elimination to strip out development only code and comments, it will drastically reduce the size of your bundle.

---

51. ### Do Hooks replace render props and higher order components?

    Hooks, introduced in React 16.8, provide a new way to manage state and side effects in functional components. They do not **replace** render props and higher-order components (HOCs) but rather offer an alternative approach that can simplify the code and make it easier to manage stateful logic.
    
    Advantages of Using Hooks Over Render Props and HOCs
	
	1. **Simplicity**: Hooks reduce the complexity that comes with nesting components and prop drilling.
	2. **Readability**: The code becomes easier to read and maintain as related logic is kept together in one component.
	3. **No Wrapper Hell**: Using hooks avoids deeply nested structures caused by HOCs and render props.
	4. **Encapsulation**: Hooks allow you to extract stateful logic into reusable functions, promoting better code organization

---

52. ### ~~What is a switching component?~~

    In the context of React, a **switching component** typically refers to a component that is responsible for conditionally rendering different child components based on some internal state or props. This pattern is commonly used to manage and display various views or UI states, such as when navigating between different routes or showing different content based on user interactions.
---

53. ### ~~What are React Mixins?~~

    **React Mixins** are a pattern that was used in older versions of React (before the introduction of Hooks and the functional component paradigm) to allow components to share behavior and code. Mixins were a way to add additional functionality to components without modifying their prototypes directly. However, mixins are now considered an outdated approach due to several limitations and the introduction of newer patterns, such as higher-order components (HOCs) and hooks.
    
---
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

---

55. ### Why should component names start with capital letter?

    If you are rendering your component using JSX, the name of that component has to begin with a capital letter otherwise React will throw an error as an unrecognized tag. ==This convention is because only HTML elements and SVG tags can begin with a lowercase letter.==

    ```jsx harmony
    function SomeComponent {
      // Code goes here
    }
    ```

    ==You can define function component whose name starts with lowercase letter, but when it's imported it should have a capital letter. Here lowercase is fine:==

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

---

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

---

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

    The reason you can't use a `for` loop directly to return components inside JSX (as shown in your second example) is that the `for` loop doesn't produce a return value like the `map` function does. In React, you need to return a valid JSX structure from the component, and the `for` loop doesn't inherently return anything to be rendered.

---

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

---

59. ### What is React proptype array with shape?

    In React, `PropTypes` is a library used for type checking props in React components. It helps ensure that the components receive the correct type of data, which can prevent bugs and make the code easier to understand. The `arrayOf` and `shape` validators allow you to define complex prop types, including arrays of objects with specific structures.

	##### `PropTypes.arrayOf` with `PropTypes.shape`
	
	- **`PropTypes.arrayOf`**: This validator checks that the prop is an array and that all elements in the array conform to a specified type.
	- **`PropTypes.shape`**: This validator allows you to define an object with a specific structure, specifying the types of each property.
	
	When combined, `PropTypes.arrayOf` and `PropTypes.shape` allow you to specify an array of objects, where each object must have a defined structure.
	```javascript 
	import React from 'react';
	import PropTypes from 'prop-types';
	
	const UserList = ({ users }) => {
	  return (
	    <ul>
	      {users.map(user => (
	        <li key={user.id}>
	          {user.name} - {user.age} years old
	        </li>
	      ))}
	    </ul>
	  );
	};
	
	// Define prop types for the UserList component
	UserList.propTypes = {
	  users: PropTypes.arrayOf(
	    PropTypes.shape({
	      id: PropTypes.number.isRequired, // id is a required number
	      name: PropTypes.string.isRequired, // name is a required string
	      age: PropTypes.number,              // age is an optional number
	    })
	  ).isRequired // users is a required array
	};
	
	export default UserList;

	```
	  
---

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

---

61. ### What is the difference between React and ReactDOM?
		
	| **Aspect**            | **React**                                             | **ReactDOM**                                           |
	|-----------------------|------------------------------------------------------|-------------------------------------------------------|
	| **Purpose**           | A JavaScript library for building user interfaces.   | A package that provides DOM-specific methods for React. |
	| **Core Functionality**| Responsible for creating React components and managing the component lifecycle. | Provides methods for rendering React components to the DOM. |
	| **Usage**             | Used to define and manage component logic and structure. | Used for manipulating the DOM and rendering components to the web page. |
	| **Rendering**         | Does not render components directly to the DOM.     | Specifically designed to render React components to the browser's DOM. |
	| **Installation**      | Installed with the `react` package.                  | Installed with the `react-dom` package.               |
	| **Example Methods**   | `React.createElement`, `React.Component`, `React.useState`, etc. | `ReactDOM.render`, `ReactDOM.unmountComponentAtNode`, `ReactDOM.createPortal`, etc. |
	| **Target Environment**| Works in both client-side and server-side rendering. | Primarily targets the browser's DOM environment.       |
	
	#### Summary
	
	- **React** is focused on building the UI components and managing their behavior.
	- **ReactDOM** provides the necessary methods to render those components into the browser's DOM, bridging the gap between React components and the actual rendering in a web application.

---

62. ### ~~Why ReactDOM is separated from React?~~

    The React team worked on extracting all DOM-related features into a separate library called _ReactDOM_. React v0.14 is the first release in which the libraries are split. By looking at some of the packages, `react-native`, `react-art`, `react-canvas`, and `react-three`, it has become clear that the beauty and essence of React has nothing to do with browsers or the DOM.

    To build more environments that React can render to, React team planned to split the main React package into two: `react` and `react-dom`. This paves the way to writing components that can be shared between the web version of React and React Native.

---

63. ### How to use React label element?

    If you try to render a `<label>` element bound to a text input using the standard `for` attribute, then it produces HTML missing that attribute and prints a warning to the console.

    ```jsx harmony
    <label for={'user'}>{'User'}</label>
    <input type={'text'} id={'user'} />
    ```

    ==Since `for` is a reserved keyword in JavaScript, use `htmlFor` instead.==

    ```jsx harmony
    <label htmlFor={'user'}>{'User'}</label>
    <input type={'text'} id={'user'} />
    ```

---

64. ### How to combine multiple inline style objects?

    You can use _spread operator_ in regular React:

    ```jsx harmony
    <button style={{ ...styles.panel.button, ...styles.panel.submitButton }}>
      {"Submit"}
    </button>
    ```

--- 

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

---

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

---

67. ### Why you can't update props in React?

    The React philosophy is that props should be _immutable_(read only) and _top-down_. This means that a parent can send any prop values to a child, but the child can't modify received props.

---

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

---

69. ### ~~How can we find the version of React at runtime in the browser?~~

    You can use `React.version` to get the version.

    ```jsx harmony
    const REACT_VERSION = React.version;

    ReactDOM.render(
      <div>{`React version: ${REACT_VERSION}`}</div>,
      document.getElementById("app")
    );
    ```

---

70. ### How to add Google Analytics for React Router?

    Add a listener on the `history` object to record each page view:

    ```javascript
    history.listen(function (location) {
      window.ga("set", "page", location.pathname + location.search);
      window.ga("send", "pageview", location.pathname + location.search);
    });
    ```

---

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

---

72. ### How to import and export components using React and ES6?

    You should use default for exporting the components

    ```jsx harmony
    import User from "user";

    export default function MyProfile {
        return <User type="customer">//...</User>;
    }
    ```

--- 

74. ### Is it possible to use async/await in plain React?

    If you want to use `async`/`await` in React, you will need _Babel_ and [transform-async-to-generator](https://babeljs.io/docs/en/babel-plugin-transform-async-to-generator) plugin. React Native ships with Babel and a set of transforms.

---

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

---

76. ### ~~What are the popular packages for animation?~~

    _React Transition Group_ and _React Motion_ are popular animation packages in React ecosystem.

---

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

---

78. ### What are the popular React-specific linters?

    ESLint is a popular JavaScript linter. There are plugins available that analyse specific code styles. One of the most common for React is an npm package called `eslint-plugin-react`. By default, it will check a number of best practices, with rules checking things from keys in iterators to a complete set of prop types.

    Another popular plugin is `eslint-plugin-jsx-a11y`, which will help fix common issues with accessibility. As JSX offers slightly different syntax to regular HTML, issues with `alt` text and `tabindex`, for example, will not be picked up by regular plugins.
