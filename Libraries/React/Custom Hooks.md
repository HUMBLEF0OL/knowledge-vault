---
tags:
  - ReactJs
Date: 2024-10-20
Title: Custom Hooks
References:
  - https://react.dev/learn/reusing-logic-with-custom-hooks#custom-hooks-sharing-logic-between-components
---
Here are detailed notes on **Custom Hooks** based on the article from React.dev.

---

### Custom Hooks: Reusing Logic Between Components

#### What are Custom Hooks?
Custom Hooks in React allow you to **encapsulate and reuse logic** across multiple components without repeating the same code. They enable you to extract reusable logic from component functions, especially when dealing with side effects or stateful logic.

Custom Hooks leverage React’s native **Hooks** like `useState`, `useEffect`, `useContext`, etc., and are JavaScript functions whose names start with `use`. This convention is critical because React uses this prefix to differentiate Hooks from regular functions.

---

### Why Use Custom Hooks?
1. **Code Reusability**: Custom Hooks allow you to **reuse complex logic** across components, avoiding duplication of code.
2. **Separation of Concerns**: You can extract logic away from UI components, making components more focused on rendering and less on handling logic.
3. **Cleaner Components**: Custom Hooks help **declutter component code** by moving stateful logic out of components.

---

### Creating Custom Hooks

Custom Hooks are simply functions that use other React Hooks. You can extract any logic that involves React Hooks and reuse it across your components.

#### Example of a Custom Hook:
Let’s create a custom hook to manage a **counter**:

```javascript
import { useState } from 'react';

// Define the custom hook
function useCounter(initialValue = 0) {
  const [count, setCount] = useState(initialValue);

  const increment = () => setCount(count + 1);
  const decrement = () => setCount(count - 1);
  const reset = () => setCount(initialValue);

  return { count, increment, decrement, reset };
}
```

**Explanation**:
- `useCounter` is a custom hook that encapsulates state and logic related to incrementing, decrementing, and resetting a counter.
- It uses the `useState` hook internally and returns functions to manage the counter logic.

Now, you can use this custom hook in any component:

```javascript
function CounterComponent() {
  const { count, increment, decrement, reset } = useCounter(10); // Using custom hook

  return (
    <div>
      <h1>Count: {count}</h1>
      <button onClick={increment}>Increment</button>
      <button onClick={decrement}>Decrement</button>
      <button onClick={reset}>Reset</button>
    </div>
  );
}
```

---

### When to Create a Custom Hook?

You should create a custom hook when:
- You find yourself repeating the same logic across different components.
- The logic is **complex** or involves **side effects** like data fetching, timers, or subscriptions.
- You want to isolate state management or behavior to **keep components clean** and focused on rendering.

---

### Sharing Logic Across Components

Custom Hooks are essential when you need to share logic (not state) across different components. Even though each component using the custom hook will have its own isolated state, they will **share the same logic**.

#### Example: Custom Hook for Fetching Data

Data fetching is a common use case for custom hooks. Let's create a `useFetch` custom hook:

```javascript
import { useState, useEffect } from 'react';

function useFetch(url) {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    const fetchData = async () => {
      try {
        const response = await fetch(url);
        const result = await response.json();
        setData(result);
      } catch (err) {
        setError(err);
      } finally {
        setLoading(false);
      }
    };

    fetchData();
  }, [url]); // Dependency array ensures data is refetched when URL changes

  return { data, loading, error };
}
```

In this example:
- **`useFetch`** encapsulates the logic of fetching data from a URL.
- It returns **data**, **loading state**, and **error** so that components using it can render accordingly.

You can reuse this hook across multiple components to fetch different data:

```javascript
function UserProfile() {
  const { data, loading, error } = useFetch('https://api.example.com/user');

  if (loading) return <p>Loading...</p>;
  if (error) return <p>Error: {error.message}</p>;

  return <div>{data.name}</div>;
}

function PostList() {
  const { data, loading, error } = useFetch('https://api.example.com/posts');

  if (loading) return <p>Loading...</p>;
  if (error) return <p>Error: {error.message}</p>;

  return (
    <ul>
      {data.map(post => (
        <li key={post.id}>{post.title}</li>
      ))}
    </ul>
  );
}
```

Both **UserProfile** and **PostList** components are reusing the same **fetch logic** without duplicating code, making the application cleaner and easier to maintain.

---

### Composing Multiple Hooks

Custom hooks can also compose other hooks, including both **built-in** and **custom** hooks. This allows for powerful abstractions.

#### Example: Custom Hook Combining `useFetch` and State Management

Let’s enhance the `useFetch` hook to add caching:

```javascript
import { useState, useEffect } from 'react';

// Caching logic
const cache = {};

function useFetchWithCache(url) {
  const [data, setData] = useState(cache[url] || null);
  const [loading, setLoading] = useState(!cache[url]);
  const [error, setError] = useState(null);

  useEffect(() => {
    if (!cache[url]) {
      const fetchData = async () => {
        try {
          const response = await fetch(url);
          const result = await response.json();
          cache[url] = result; // Cache the result
          setData(result);
        } catch (err) {
          setError(err);
        } finally {
          setLoading(false);
        }
      };

      fetchData();
    }
  }, [url]);

  return { data, loading, error };
}
```

In this case, the **caching mechanism** prevents repeated network requests for the same URL. This is a great example of combining **stateful logic** with external hooks to create optimized, reusable hooks.

---

### Debugging Custom Hooks

Since custom hooks follow the same rules as React’s built-in hooks, it’s essential to follow **the rules of hooks**:
1. **Only call hooks at the top level**: Don’t call hooks inside loops, conditions, or nested functions.
2. **Only call hooks from React functions**: Hooks should only be used in functional components or other custom hooks.

You can use **React DevTools** to inspect the state managed by custom hooks, and you can also apply performance optimizations (e.g., memoization) just as you would with regular hooks.

---

### Best Practices for Custom Hooks

1. **Use a descriptive name**: Always start the hook name with "use" and make it clear what the hook does. For example, `useAuth` for managing authentication state or `useWindowWidth` for tracking window dimensions.
   
2. **Extract reusable logic**: Custom Hooks should focus on extracting logic that can be reused across different components. Avoid including rendering logic or UI-specific code inside them.

3. **Keep them isolated**: Don’t rely on global variables or external state inside custom hooks unless it’s necessary. Keep custom hooks self-contained.

4. **Use parameters wisely**: Custom hooks can accept parameters to make them more flexible. For example, a `useFetch` hook can take a URL and options like headers or query parameters.

5. **Memoization**: Use `useMemo` or `useCallback` inside your custom hooks when you need to ensure that the returned values or functions remain stable across renders.

---

### Custom Hooks vs Higher-Order Components (HOCs)

Custom hooks are often seen as a more **modern and flexible alternative** to HOCs for sharing logic. Both Custom Hooks and HOCs are used to reuse logic, but there are some differences:
- **Custom Hooks**: Reuse logic inside functional components, simpler, and don’t introduce additional layers in the component tree.
- **HOCs**: Introduce an additional layer of components, commonly used in class-based components.

In most cases, custom hooks are the preferred method for sharing logic in modern React applications.

---

### Conclusion

Custom Hooks are a powerful feature of React that enables the **reuse of stateful logic** and **side effects** across different components. They are lightweight, easy to write, and help in maintaining a clean and maintainable codebase by separating logic from UI. By encapsulating logic in a hook, you can **share it across many components** while keeping the components focused on rendering.

Custom Hooks are essential for modern React development, allowing you to **compose** and **reuse** functionality in a way that was not possible before React Hooks were introduced.