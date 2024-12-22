---
tags:
  - ReactJs
  - Interview-Prep
Date: 2024-10-12
Title: Redux
References:
---
### **React Redux**

---

### **Beginner Level**

#### **1. What is Redux, and why is it used in React applications?**

**Answer:**  
Redux is a predictable state management library often used in JavaScript applications, including React. It helps manage the application's global state in a predictable manner, making it easier to debug and maintain. Redux is used in React applications to handle state that needs to be accessed and modified by multiple components, ensuring consistency and avoiding prop-drilling.

---

#### **2. Explain the core principles of Redux.**

**Answer:**  
The core principles of Redux are:

1. **Single Source of Truth**: The state of the entire application is stored in a single object tree within a central store.
2. **State is Read-Only**: State can only be changed by dispatching actions, ensuring predictability.
3. **Changes are Made with Pure Functions**: Reducers, which are pure functions, specify how the state changes in response to an action.

---

#### **3. What are the key components of Redux?**

**Answer:**  
The key components of Redux are:

1. **Store**: Holds the entire state of the application.
2. **Actions**: Objects that represent a change or event in the application. They must have a `type` field.
3. **Reducers**: Pure functions that take the current state and an action as arguments and return a new state.

---

#### **4. How does Redux differ from React Context API?**

**Answer:**  
While both Redux and Context API manage state globally:

- **Redux**:
    - Used for complex state management.
    - Includes advanced features like middleware and time-travel debugging.
    - Requires additional boilerplate and setup.
- **Context API**:
    - Ideal for simple state sharing.
    - Built directly into React but lacks advanced debugging and middleware capabilities.

---

#### **5. What is the role of a reducer in Redux? Provide an example.**

**Answer:**  
A reducer is a pure function that determines how the state should change based on an action.

**Example:**

```javascript
const counterReducer = (state = { count: 0 }, action) => {
  switch (action.type) {
    case "INCREMENT":
      return { count: state.count + 1 };
    case "DECREMENT":
      return { count: state.count - 1 };
    default:
      return state;
  }
};
```

---

#### **6. What is an action in Redux, and what does it typically contain?**

**Answer:**  
An action in Redux is a plain JavaScript object that describes a change in the application. Actions must have a `type` property and can optionally include additional data.

**Example:**

```javascript
const incrementAction = { type: "INCREMENT" };
const addTodoAction = { type: "ADD_TODO", payload: "Learn Redux" };
```

---

#### **7. How do you create a Redux store? Provide a code snippet.**

**Answer:**

```javascript
import { createStore } from "redux";
import counterReducer from "./reducers/counterReducer";

const store = createStore(counterReducer);
console.log(store.getState()); // Initial state
```

---

#### **8. What is `dispatch` in Redux? How is it used?**

**Answer:**  
`dispatch` is a method provided by the Redux store to send actions to reducers, updating the state.

**Example:**

```javascript
store.dispatch({ type: "INCREMENT" });
console.log(store.getState()); // Updated state
```

---

#### **9. Explain the concept of middleware in Redux. Can you name some commonly used middlewares?**

**Answer:**  
Middleware in Redux intercepts actions before they reach the reducer, allowing you to handle side effects like API calls or logging.

**Common Middlewares:**

- **Redux Thunk**: Handles asynchronous actions.
- **Redux Saga**: Handles complex asynchronous workflows.
- **Redux Logger**: Logs actions and state changes for debugging.

---

### **Intermediate Level**

#### **10. How do you integrate Redux with a React application?**

**Answer:**  
Integration involves:

1. Creating a Redux store.
2. Wrapping the application with `Provider` from `react-redux`.
3. Using `connect` or hooks like `useSelector` and `useDispatch` to interact with the store.

**Code Example:**

```javascript
import React from "react";
import { Provider } from "react-redux";
import { createStore } from "redux";
import rootReducer from "./reducers";

const store = createStore(rootReducer);

const App = () => (
  <Provider store={store}>
    <MyComponent />
  </Provider>
);
```

---

#### **11. What is the purpose of the `connect` function in React-Redux? Provide an example.**

**Answer:**  
`connect` maps state and dispatch to a component's props, enabling interaction with the Redux store.

**Example:**

```javascript
import { connect } from "react-redux";

const mapStateToProps = (state) => ({ count: state.count });
const mapDispatchToProps = (dispatch) => ({
  increment: () => dispatch({ type: "INCREMENT" }),
});

export default connect(mapStateToProps, mapDispatchToProps)(CounterComponent);
```

---

#### **12. What is Redux Thunk, and why is it used?**

**Answer:**  
Redux Thunk is middleware that allows you to write action creators returning functions instead of objects. It enables handling asynchronous logic like API calls.

**Example:**

```javascript
export const fetchData = () => async (dispatch) => {
  const response = await fetch("/data");
  const data = await response.json();
  dispatch({ type: "FETCH_SUCCESS", payload: data });
};
```

---

### **Advanced Level**

#### **21. What is memoization, and how is it applied in Redux selectors?**

**Answer:**  
Memoization is an optimization technique that stores the results of expensive function calls. In Redux, `reselect` is used to memoize selectors, ensuring they only recompute when input changes.

**Example:**

```javascript
import { createSelector } from "reselect";

const selectItems = (state) => state.items;
const selectFilteredItems = createSelector(
  [selectItems],
  (items) => items.filter((item) => item.active)
);
```

---

#### **29. What is Redux Toolkit, and how does it simplify Redux usage?**

**Answer:**  
Redux Toolkit is a library that simplifies Redux by reducing boilerplate and providing utilities like `createSlice`, `createAsyncThunk`, and `configureStore`.

**Example:**

```javascript
import { configureStore, createSlice } from "@reduxjs/toolkit";

const counterSlice = createSlice({
  name: "counter",
  initialState: { count: 0 },
  reducers: {
    increment: (state) => { state.count += 1; },
  },
});

const store = configureStore({ reducer: counterSlice.reducer });
store.dispatch(counterSlice.actions.increment());
console.log(store.getState()); // { count: 1 }
```


---

### **Intermediate Level**

#### **13. How is Redux Saga different from Redux Thunk? When would you use one over the other?**

**Answer:**

- **Redux Thunk**:
    
    - Allows action creators to return functions.
    - Good for simple asynchronous operations like API calls.
    - Easy to set up and lightweight.
- **Redux Saga**:
    
    - Uses ES6 generators to handle complex asynchronous workflows.
    - Ideal for handling multiple, interdependent side effects.
    - Provides better control over async flows through sagas like `takeEvery` and `takeLatest`.

**Use Case:**  
Use Redux Thunk for simple apps with minimal async needs. Use Redux Saga for complex workflows, such as handling race conditions or retrying failed requests.

---

#### **14. Explain the use of `useSelector` and `useDispatch` hooks in functional components.**

**Answer:**

- **`useSelector`**: Allows you to extract data from the Redux store's state.
- **`useDispatch`**: Provides access to the `dispatch` method to send actions.

**Example:**

```javascript
import React from "react";
import { useSelector, useDispatch } from "react-redux";

const Counter = () => {
  const count = useSelector((state) => state.count);
  const dispatch = useDispatch();

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => dispatch({ type: "INCREMENT" })}>Increment</button>
    </div>
  );
};
```

---

#### **15. How do you handle asynchronous actions in Redux?**

**Answer:**  
Asynchronous actions in Redux are handled using middlewares like **Redux Thunk** or **Redux Saga**. They allow dispatching actions at different points in an asynchronous flow.

**Thunk Example:**

```javascript
export const fetchData = () => async (dispatch) => {
  dispatch({ type: "FETCH_START" });
  try {
    const response = await fetch("/api/data");
    const data = await response.json();
    dispatch({ type: "FETCH_SUCCESS", payload: data });
  } catch (error) {
    dispatch({ type: "FETCH_ERROR", payload: error.message });
  }
};
```

---

#### **16. What are the common patterns for structuring a Redux store in a large-scale application?**

**Answer:**

1. **Feature-based structure**: Organize files by features or domains.
    
    ```
    /features
      /counter
        - CounterSlice.js
        - CounterComponent.js
    ```
    
2. **Normalized state**: Use flat structures and unique IDs for entities to avoid deeply nested state.
    
    ```javascript
    const state = {
      users: { byId: { 1: { id: 1, name: "Alice" }, 2: { id: 2, name: "Bob" } } },
      posts: { byId: { 101: { id: 101, title: "Post Title", userId: 1 } } },
    };
    ```
    
3. **Use Redux Toolkit**: Simplify slice creation and state updates.
    

---

#### **17. How do you persist the Redux state across page reloads?**

**Answer:**  
Use **localStorage**, **sessionStorage**, or libraries like **redux-persist**.

**Example with localStorage:**

```javascript
const saveToLocalStorage = (state) => {
  localStorage.setItem("reduxState", JSON.stringify(state));
};

const loadFromLocalStorage = () => {
  const serializedState = localStorage.getItem("reduxState");
  return serializedState ? JSON.parse(serializedState) : undefined;
};

const store = createStore(rootReducer, loadFromLocalStorage());
store.subscribe(() => saveToLocalStorage(store.getState()));
```

---

### **Advanced Level**

#### **18. What are immutable updates, and why are they important in Redux?**

**Answer:**  
Immutable updates ensure the original state is not directly modified. Instead, a new copy of the state is created with changes.

**Importance:**

1. Ensures state predictability.
2. Enables features like time-travel debugging.
3. Prevents unintended side effects.

**Example (Correct Way):**

```javascript
const reducer = (state, action) => {
  switch (action.type) {
    case "ADD_ITEM":
      return { ...state, items: [...state.items, action.payload] };
    default:
      return state;
  }
};
```

---

#### **19. What is `reselect`, and how is it used?**

**Answer:**  
`reselect` is a library for creating memoized selectors in Redux. It avoids unnecessary recomputation by caching the output unless inputs change.

**Example:**

```javascript
import { createSelector } from "reselect";

const selectItems = (state) => state.items;
const selectFilteredItems = createSelector(
  [selectItems],
  (items) => items.filter((item) => item.completed)
);

const mapStateToProps = (state) => ({
  filteredItems: selectFilteredItems(state),
});
```

---

#### **20. How can you manage complex side effects in Redux?**

**Answer:**  
Complex side effects can be managed using **Redux Saga**, where sagas handle workflows like API retries, concurrent requests, and debouncing.

**Example with Redux Saga:**

```javascript
import { call, put, takeEvery } from "redux-saga/effects";

function* fetchUser(action) {
  try {
    const user = yield call(fetch, `/api/user/${action.payload}`);
    yield put({ type: "USER_FETCH_SUCCESS", payload: user });
  } catch (e) {
    yield put({ type: "USER_FETCH_ERROR", payload: e.message });
  }
}

function* mySaga() {
  yield takeEvery("USER_FETCH_REQUEST", fetchUser);
}

export default mySaga;
```

---

#### **21. What is the difference between Redux and Redux Toolkit?**

**Answer:**  
**Redux Toolkit** simplifies Redux development by:

1. Reducing boilerplate with `createSlice`.
2. Providing built-in support for immutable updates via Immer.
3. Supporting powerful tools like `createAsyncThunk`.

**Redux Toolkit Example:**

```javascript
const counterSlice = createSlice({
  name: "counter",
  initialState: { count: 0 },
  reducers: {
    increment: (state) => { state.count += 1; },
  },
});
```

---

#### **22. How would you debug a Redux application? Which tools can you use?**

**Answer:**

- Use **Redux DevTools Extension** to inspect actions, state changes, and time-travel.
- Add logging middleware like **redux-logger**.
- Use custom logging inside reducers or middleware to trace state and action flow.

---

#### **23. What are the advantages and disadvantages of using Redux in a project?**

**Answer:**  
**Advantages:**

- Predictable state management.
- Debugging and time-travel capabilities.
- Scalability in complex apps.

**Disadvantages:**

- Steep learning curve.
- Boilerplate code (mitigated by Redux Toolkit).
- Overhead in simple applications.

---

### **Beginner-Level**

#### **1. What is Redux Toolkit? Why was it introduced?**

**Answer:**  
Redux Toolkit (RTK) is a library built on top of Redux to simplify and streamline the process of writing Redux logic.

**Key Features of Redux Toolkit:**

- Eliminates boilerplate code.
- Includes tools for immutable updates using Immer.
- Provides `createSlice`, `createAsyncThunk`, and other utilities.
- Integrates Redux DevTools and middleware by default.

**Why Introduced?**  
Redux Toolkit was introduced to address common pain points with Redux, such as excessive boilerplate code, difficulty managing state immutably, and confusion over setting up middleware.

---

#### **2. What is a slice in Redux Toolkit?**

**Answer:**  
A **slice** is a modular piece of Redux state logic created using the `createSlice` function. It includes:

1. State.
2. Reducers (actions).
3. Action creators (auto-generated).

**Example:**

```javascript
import { createSlice } from '@reduxjs/toolkit';

const counterSlice = createSlice({
  name: 'counter',
  initialState: { value: 0 },
  reducers: {
    increment: (state) => { state.value += 1; },
    decrement: (state) => { state.value -= 1; },
    reset: (state) => { state.value = 0; }
  }
});

export const { increment, decrement, reset } = counterSlice.actions;
export default counterSlice.reducer;
```

---

#### **3. What are the benefits of using `createSlice`?**

**Answer:**

- Combines action creators and reducers into one.
- Automatically generates action types and action creators.
- Makes state updates immutable using Immer under the hood.
- Reduces boilerplate code.

---

#### **4. What is the difference between `configureStore` and `createStore`?**

**Answer:**

- **`configureStore` (Redux Toolkit):** Simplifies store creation by combining reducers, middleware, and DevTools configuration automatically.
- **`createStore` (Redux):** Requires manual configuration of reducers, middleware, and enhancers.

**Example with `configureStore`:**

```javascript
import { configureStore } from '@reduxjs/toolkit';
import counterReducer from './counterSlice';

const store = configureStore({
  reducer: {
    counter: counterReducer
  }
});
```

---

#### **5. What are some built-in middleware included in Redux Toolkit?**

**Answer:**  
Redux Toolkit includes:

1. **`redux-thunk`**: For handling async logic.
2. **`serializableCheck`**: Ensures non-serializable values are not added to the Redux state.
3. **`immutableCheck`**: Warns if state mutations occur.

---

### **Intermediate-Level**

#### **6. How do you handle asynchronous logic in Redux Toolkit?**

**Answer:**  
Use **`createAsyncThunk`**, a utility provided by RTK for handling asynchronous logic.

**Example:**

```javascript
import { createAsyncThunk, createSlice } from '@reduxjs/toolkit';

// Define an async thunk
export const fetchUsers = createAsyncThunk('users/fetch', async () => {
  const response = await fetch('/api/users');
  return response.json();
});

// Slice
const usersSlice = createSlice({
  name: 'users',
  initialState: { data: [], status: 'idle', error: null },
  reducers: {},
  extraReducers: (builder) => {
    builder
      .addCase(fetchUsers.pending, (state) => {
        state.status = 'loading';
      })
      .addCase(fetchUsers.fulfilled, (state, action) => {
        state.status = 'succeeded';
        state.data = action.payload;
      })
      .addCase(fetchUsers.rejected, (state, action) => {
        state.status = 'failed';
        state.error = action.error.message;
      });
  }
});

export default usersSlice.reducer;
```

---

#### **7. What is the purpose of `extraReducers` in `createSlice`?**

**Answer:**  
`extraReducers` allows a slice to respond to actions defined outside of its own reducers.

- Typically used to handle actions from `createAsyncThunk` or actions from other slices.

---

#### **8. How does `createSlice` internally handle immutability?**

**Answer:**  
RTK uses **Immer** to handle immutability. Immer allows you to write code as if you're mutating state directly, but it produces an immutable state behind the scenes.

**Example:**

```javascript
reducers: {
  increment: (state) => {
    state.value += 1; // Looks mutable, but is immutable due to Immer
  }
}
```

---

#### **9. How do you combine multiple reducers in Redux Toolkit?**

**Answer:**  
Use the `configureStore` function and pass an object to the `reducer` field.

**Example:**

```javascript
import { configureStore } from '@reduxjs/toolkit';
import counterReducer from './counterSlice';
import usersReducer from './usersSlice';

const store = configureStore({
  reducer: {
    counter: counterReducer,
    users: usersReducer
  }
});
```

---

#### **10. How do you add middleware to a Redux Toolkit store?**

**Answer:**  
Use the `middleware` option in `configureStore`.

**Example:**

```javascript
import { configureStore } from '@reduxjs/toolkit';
import logger from 'redux-logger';
import counterReducer from './counterSlice';

const store = configureStore({
  reducer: { counter: counterReducer },
  middleware: (getDefaultMiddleware) => getDefaultMiddleware().concat(logger)
});
```

---

### **Advanced-Level**

#### **11. How can you test Redux Toolkit slices?**

**Answer:**  
You can test slices by directly invoking the reducer and comparing the state.

**Example Test (with Jest):**

```javascript
import counterReducer, { increment } from './counterSlice';

test('should increment the counter', () => {
  const initialState = { value: 0 };
  const nextState = counterReducer(initialState, increment());
  expect(nextState.value).toBe(1);
});
```

---

#### **12. What is the difference between `builder.addCase` and `builder.addMatcher` in `extraReducers`?**

**Answer:**

- **`addCase`**: Handles specific action types.
- **`addMatcher`**: Handles actions that match certain conditions (like type patterns).

**Example with `addMatcher`:**

```javascript
builder.addMatcher(
  (action) => action.type.endsWith('/rejected'),
  (state, action) => {
    state.error = action.error.message;
  }
);
```

---

#### **13. How does Redux Toolkit support code splitting?**

**Answer:**  
RTK supports dynamic addition of reducers using the `combineReducers` and `replaceReducer` methods. This is helpful for lazy-loading reducers in large applications.

**Example:**

```javascript
store.replaceReducer(newRootReducer);
```

---

#### **14. What is the purpose of `createEntityAdapter` in Redux Toolkit?**

**Answer:**  
`createEntityAdapter` simplifies managing normalized state for collections like arrays of data.

**Example:**

```javascript
import { createEntityAdapter, createSlice } from '@reduxjs/toolkit';

const usersAdapter = createEntityAdapter();

const usersSlice = createSlice({
  name: 'users',
  initialState: usersAdapter.getInitialState(),
  reducers: {
    addUser: usersAdapter.addOne,
    addUsers: usersAdapter.addMany,
    removeUser: usersAdapter.removeOne
  }
});

export const { addUser, addUsers, removeUser } = usersSlice.actions;
export default usersSlice.reducer;
```

---

#### **15. What are the pros and cons of Redux Toolkit?**

**Answer:**  
**Pros:**

- Reduces boilerplate code.
- Built-in support for async actions.
- Easy integration with DevTools and middleware.
- Supports modern Redux best practices.

**Cons:**

- Learning curve for advanced features like `createAsyncThunk` and `createEntityAdapter`.
- May not be necessary for very simple applications.

---

### **React Context API**

### **Beginner-Level**

#### **1. What is the Context API in React?**

**Answer:**  
The **Context API** is a feature in React that allows you to share data (state, functions, or objects) globally across the component tree without having to pass props down manually at every level.  
It helps in avoiding "prop drilling," where props are passed through many intermediate components.

---

#### **2. What are the main components of the Context API?**

**Answer:**  
The Context API has three main components:

1. **`React.createContext`**: Creates a context object.
2. **`Provider`**: A component that supplies the context value to its child components.
3. **`Consumer`**: A component that consumes and uses the context value.

**Example:**

```javascript
const MyContext = React.createContext();

function App() {
  return (
    <MyContext.Provider value="Hello World">
      <ChildComponent />
    </MyContext.Provider>
  );
}

function ChildComponent() {
  return (
    <MyContext.Consumer>
      {(value) => <div>{value}</div>}
    </MyContext.Consumer>
  );
}
```

---

#### **3. How do you create and use a Context in React?**

**Answer:**

1. **Create a context:**
    
    ```javascript
    const ThemeContext = React.createContext();
    ```
    
2. **Provide a value using `Provider`:**
    
    ```javascript
    <ThemeContext.Provider value="dark">
      <App />
    </ThemeContext.Provider>
    ```
    
3. **Consume the context value:**
    - Using `Consumer`:
        
        ```javascript
        <ThemeContext.Consumer>
          {(value) => <div>{value}</div>}
        </ThemeContext.Consumer>
        ```
        
    - Using `useContext` (preferred):
        
        ```javascript
        const theme = React.useContext(ThemeContext);
        console.log(theme); // "dark"
        ```
        

---

#### **4. What problem does the Context API solve?**

**Answer:**  
The Context API solves **prop drilling**, where data has to be passed down through multiple layers of components even if only one component at a deep level needs it.

---

#### **5. What is `useContext`? How is it used?**

**Answer:**  
`useContext` is a React Hook that provides access to a context value. It is a cleaner and more modern alternative to `Consumer`.

**Example:**

```javascript
const ThemeContext = React.createContext();

function Component() {
  const theme = React.useContext(ThemeContext);
  return <div>The theme is {theme}</div>;
}
```

---

### **Intermediate-Level**

#### **6. Can the Context API replace Redux?**

**Answer:**  
While the Context API can manage global state and is suitable for simple use cases, it cannot completely replace Redux for the following reasons:

- **Context API**: Ideal for small-to-medium apps with limited global state needs.
- **Redux**: Better for large-scale apps with complex state logic, middleware, and time-travel debugging.

---

#### **7. How do you manage multiple contexts?**

**Answer:**  
You can nest multiple `Provider` components or combine contexts using custom hooks.

**Example (Nesting):**

```javascript
<ThemeContext.Provider value="dark">
  <AuthContext.Provider value={{ user: 'John' }}>
    <App />
  </AuthContext.Provider>
</ThemeContext.Provider>
```

**Example (Combining Contexts with a Custom Hook):**

```javascript
function useCombinedContext() {
  const theme = useContext(ThemeContext);
  const auth = useContext(AuthContext);
  return { theme, auth };
}
```

---

#### **8. What are some potential downsides of using the Context API?**

**Answer:**

- **Re-renders:** If the context value changes, all components consuming the context re-render, which may lead to performance issues.
- **Complexity:** Using multiple contexts can make the code harder to manage.
- **Limited debugging tools:** Unlike Redux, the Context API lacks advanced debugging tools.

---

#### **9. How can you optimize performance when using Context API?**

**Answer:**

- **Memoize the context value:**  
    Use `useMemo` to prevent unnecessary re-renders.
    
    ```javascript
    const contextValue = useMemo(() => ({ theme }), [theme]);
    <ThemeContext.Provider value={contextValue}>
      <App />
    </ThemeContext.Provider>
    ```
    
- **Split contexts:**  
    Use multiple contexts to minimize unnecessary re-renders.
    

---

#### **10. How is the Context API different from props?**

**Answer:**

- **Props**: Used for passing data from parent to child in a unidirectional manner.
- **Context API**: Used for sharing global state or data across the component tree without passing props manually.

---

### **Advanced-Level**

#### **11. How do you test components that use Context?**

**Answer:**  
Use a mock provider in your test.

**Example with Jest/React Testing Library:**

```javascript
const ThemeContext = React.createContext();

function TestComponent() {
  const theme = useContext(ThemeContext);
  return <div>The theme is {theme}</div>;
}

test('renders the correct theme', () => {
  const { getByText } = render(
    <ThemeContext.Provider value="dark">
      <TestComponent />
    </ThemeContext.Provider>
  );
  expect(getByText('The theme is dark')).toBeInTheDocument();
});
```

---

#### **12. Can you update a context value dynamically?**

**Answer:**  
Yes, you can update context dynamically by maintaining the value in the state.

**Example:**

```javascript
const ThemeContext = React.createContext();

function App() {
  const [theme, setTheme] = useState('light');
  return (
    <ThemeContext.Provider value={{ theme, setTheme }}>
      <ChildComponent />
    </ThemeContext.Provider>
  );
}

function ChildComponent() {
  const { theme, setTheme } = useContext(ThemeContext);
  return (
    <div>
      Current theme: {theme}
      <button onClick={() => setTheme('dark')}>Change to Dark</button>
    </div>
  );
}
```

---

#### **13. How do you share functions through Context API?**

**Answer:**  
You can pass functions as part of the context value.

**Example:**

```javascript
const CounterContext = React.createContext();

function App() {
  const [count, setCount] = useState(0);
  const increment = () => setCount((c) => c + 1);
  
  return (
    <CounterContext.Provider value={{ count, increment }}>
      <ChildComponent />
    </CounterContext.Provider>
  );
}

function ChildComponent() {
  const { count, increment } = useContext(CounterContext);
  return (
    <div>
      Count: {count}
      <button onClick={increment}>Increment</button>
    </div>
  );
}
```

---

#### **14. How can you access a context value in class components?**

**Answer:**  
Use the `contextType` property or `<Context.Consumer>`.

**Using `contextType`:**

```javascript
const ThemeContext = React.createContext();

class MyClassComponent extends React.Component {
  static contextType = ThemeContext;
  render() {
    return <div>Theme: {this.context}</div>;
  }
}
```

---

#### **15. What are some common use cases for the Context API?**

**Answer:**

- **Theming**: Sharing a theme across the app.
- **Authentication**: Managing user authentication state.
- **Localization**: Providing language translations.
- **Global State Management**: Sharing app-wide settings like dark mode, user preferences, etc.
