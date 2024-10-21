---
tags:
  - ReactJs
Date: 2024-10-12
Title: 
References:
  - https://www.freecodecamp.org/news/react-context-api-explained-with-examples/
---
Here are extensive notes on **React Context API**, based on the FreeCodeCamp article.

---

### React Context API: Explained with Examples

#### What is Context API?
The **React Context API** provides a way to share data (such as global state) across the component tree without having to pass props down manually at every level. It is particularly useful for managing **global state**, such as theme settings, user authentication, and other configurations that need to be accessible by many components at different levels of the hierarchy.

Before Context API, prop drilling (passing props through intermediate components) was the main way to share data between components that were not directly related. Context API simplifies this by providing a global store of data that any component can subscribe to.

---

### When to Use Context API
Context API should be used sparingly because it can introduce complexity if not managed properly. It is best used when:
- Data needs to be accessible globally.
- Multiple components need access to the same data.
- Passing props down many levels is cumbersome (prop drilling).
  
#### Common Use Cases
1. **Theme Settings**: Managing light/dark mode across the application.
2. **User Authentication**: Providing the authenticated user's information to multiple components.
3. **Localization**: Sharing language or localization settings.
4. **Global Settings**: Sharing global configuration like app-wide notifications, error handlers, etc.

---

### Creating and Using Context API

#### Step 1: Create a Context
To start using Context, first create a context using `React.createContext()`. This creates an object with two components:
- **Provider**: Wraps components that need access to the context.
- **Consumer**: Components that need to consume the context data.

```javascript
import React, { createContext } from 'react';

const ThemeContext = createContext(); // Creating a context object
```

This `ThemeContext` is now ready to share data across components.

#### Step 2: Provide Context Data
The **Provider** component is used to wrap the part of the component tree where you want to provide context data. It accepts a `value` prop, which will be available to all its children.

```javascript
const App = () => {
  return (
    <ThemeContext.Provider value="dark">
      <Header />
      <Content />
    </ThemeContext.Provider>
  );
};
```

Here, the **`ThemeContext.Provider`** wraps components like `<Header />` and `<Content />`, and it passes the value `"dark"` to all of its children.

#### Step 3: Consume Context Data
Any component that needs access to the context can consume it using either:
1. **Context Consumer**.
2. **`useContext` Hook**.

##### Using Context Consumer
The **Consumer** component subscribes to context changes and renders the content accordingly.

```javascript
const Header = () => {
  return (
    <ThemeContext.Consumer>
      {(value) => (
        <h1>The theme is {value}</h1> // Accessing the context value
      )}
    </ThemeContext.Consumer>
  );
};
```

##### Using the `useContext` Hook (Recommended)
The `useContext` hook simplifies consuming context data. It takes the context object and returns the current value for that context.

```javascript
import { useContext } from 'react';

const Header = () => {
  const theme = useContext(ThemeContext); // Using useContext hook
  return <h1>The theme is {theme}</h1>;
};
```

---

### Example: Passing Data with Context API

Let's build a simple example where we share the **theme** across multiple components using Context API.

```javascript
import React, { createContext, useContext } from 'react';

// Step 1: Create the context
const ThemeContext = createContext();

// Step 2: Create a component that provides the context
const App = () => {
  return (
    <ThemeContext.Provider value="dark">
      <Toolbar />
    </ThemeContext.Provider>
  );
};

// Step 3: Create a component that consumes the context
const Toolbar = () => {
  return (
    <div>
      <ThemedButton />
    </div>
  );
};

// Step 4: Create another component that consumes the context using useContext hook
const ThemedButton = () => {
  const theme = useContext(ThemeContext); // Access context data
  return <button style={{ background: theme === 'dark' ? '#333' : '#FFF' }}>Themed Button</button>;
};

export default App;
```

**Explanation**:
1. **ThemeContext** is created and used to share the "dark" theme across the app.
2. **ThemedButton** consumes this context using the `useContext` hook and changes the background color of the button based on the theme.

---

### Updating Context

The context value can be dynamic, meaning it can be changed by components within the Provider.

#### Example: Updating the Context Value
Let’s update the theme based on a toggle.

```javascript
import React, { createContext, useContext, useState } from 'react';

// Step 1: Create the context
const ThemeContext = createContext();

const App = () => {
  const [theme, setTheme] = useState('light');

  const toggleTheme = () => {
    setTheme((prevTheme) => (prevTheme === 'light' ? 'dark' : 'light'));
  };

  return (
    <ThemeContext.Provider value={theme}>
      <Toolbar />
      <button onClick={toggleTheme}>Toggle Theme</button>
    </ThemeContext.Provider>
  );
};

const Toolbar = () => {
  return (
    <div>
      <ThemedButton />
    </div>
  );
};

const ThemedButton = () => {
  const theme = useContext(ThemeContext);
  return <button style={{ background: theme === 'dark' ? '#333' : '#FFF' }}>Themed Button</button>;
};

export default App;
```

In this example, the theme can be toggled between **light** and **dark** using the button. The `ThemeContext.Provider` now provides the current value of `theme`, which is updated whenever the button is clicked.

---

### Nested Context and Context Composition

In more complex applications, you might want to have multiple contexts handling different parts of the state (e.g., theme and authentication).

#### Example: Nested Contexts

```javascript
import React, { createContext, useContext, useState } from 'react';

// Create contexts
const ThemeContext = createContext();
const AuthContext = createContext();

const App = () => {
  const [theme] = useState('dark');
  const [user] = useState({ name: 'John' });

  return (
    <ThemeContext.Provider value={theme}>
      <AuthContext.Provider value={user}>
        <Page />
      </AuthContext.Provider>
    </ThemeContext.Provider>
  );
};

const Page = () => {
  return (
    <div>
      <ThemedHeader />
      <UserInfo />
    </div>
  );
};

const ThemedHeader = () => {
  const theme = useContext(ThemeContext);
  return <h1 style={{ background: theme === 'dark' ? '#333' : '#FFF' }}>Themed Header</h1>;
};

const UserInfo = () => {
  const user = useContext(AuthContext);
  return <h2>Welcome, {user.name}</h2>;
};

export default App;
```

In this example:
- We have two contexts: **ThemeContext** and **AuthContext**.
- **ThemedHeader** consumes the theme, and **UserInfo** consumes the authenticated user.

---

### Context API vs Redux

Though both Context API and **Redux** can be used for global state management, they serve different purposes:

| Feature         | Context API                     | Redux                              |
|-----------------|---------------------------------|------------------------------------|
| Use Case        | Small to medium state sharing.  | Complex, large-scale state management. |
| Boilerplate     | Minimal.                        | Requires setup (actions, reducers). |
| Performance     | Can cause re-renders if not optimized. | Optimized with immutability and middleware. |
| Learning Curve  | Easy to learn.                  | Higher learning curve.             |

For simple global state like theme toggling or user info, Context API is preferable. However, for managing complex application state with actions and reducers, Redux is more efficient.

---

### Optimizing Performance with Context API

One downside of Context API is that when the context value changes, all components that consume the context will re-render. This can lead to performance issues if not handled properly.

**Optimization Tips**:
1. **Memoize the Context Value**: Use `useMemo` to prevent unnecessary re-renders.
   ```javascript
   const theme = useMemo(() => ({ mode: 'dark' }), []);
   ```
2. **Split Contexts**: Avoid putting too much data in a single context. Instead, split it into smaller contexts based on the need.
3. **Use React DevTools**: Analyze component re-renders and performance using React DevTools.

---

### Conclusion

The **React Context API** provides a powerful and simple way to share data between components without passing props manually. It is ideal for managing global state, such as theme settings or user authentication, but should be used cautiously to avoid performance pitfalls. For larger and more complex state management, tools like Redux might be a better fit.

--- 

Let me know if you need any additional details or diagrams for this topic!