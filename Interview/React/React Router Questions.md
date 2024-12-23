---
tags:
  - ReactJs
  - Interview-Prep
Date: 2024-10-12
Title: React Router
References:
  - https://github.com/sudheerj/reactjs-interview-questions
---

### **Beginner-Level**

#### **1. What is React Router?**

**Answer:**  
React Router is a standard library for routing in React. It enables navigation between views of different components in a React application, allowing developers to implement dynamic and declarative routing.

---

#### **2. What are the main components of React Router?**

**Answer:**

1. **`BrowserRouter`**: Uses the HTML5 history API for navigation.
2. **`Routes`**: Defines a collection of routes in the app.
3. **`Route`**: Defines a single route and what component to render when matched.
4. **`Link`**: Creates navigation links.
5. **`NavLink`**: Similar to `Link` but adds styling for active routes.
6. **`useNavigate`**: Hook for programmatic navigation.
7. **`useParams`**: Hook to access route parameters.

---

#### **3. What is the difference between `BrowserRouter` and `HashRouter`?**

**Answer:**

- **BrowserRouter**: Uses the HTML5 history API to manage URLs (e.g., `/about`).
- **HashRouter**: Uses the hash portion of the URL (e.g., `#/about`) and works in environments where the server doesn't support dynamic routes.

---

#### **4. How do you set up a basic route in React Router?**

**Answer:**  
**Example:**

```javascript
import { BrowserRouter as Router, Routes, Route } from 'react-router-dom';
import Home from './Home';
import About from './About';

function App() {
  return (
    <Router>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
      </Routes>
    </Router>
  );
}
```

---

#### **5. How do you create navigation links in React Router?**

**Answer:**  
Use the `Link` or `NavLink` component.  
**Example:**

```javascript
import { Link } from 'react-router-dom';

function Navbar() {
  return (
    <nav>
      <Link to="/">Home</Link>
      <Link to="/about">About</Link>
    </nav>
  );
}
```

---

#### **6. What is the difference between `Link` and `NavLink`?**

**Answer:**

- **`Link`**: Provides basic navigation.
- **`NavLink`**: Adds a class to the active link by default. You can also customize the active class.

**Example:**

```javascript
<NavLink to="/about" className={({ isActive }) => (isActive ? 'active' : '')}>
  About
</NavLink>
```

---

#### **7. How do you handle a 404 page in React Router?**

**Answer:**  
Use the wildcard `*` path to define a fallback route.  
**Example:**

```javascript
<Routes>
  <Route path="/" element={<Home />} />
  <Route path="*" element={<NotFound />} />
</Routes>
```

---

### **Intermediate-Level**

#### **8. How do you use dynamic routing with React Router?**

**Answer:**  
Dynamic routing is achieved using route parameters with `:parameterName`.  
**Example:**

```javascript
<Route path="/user/:id" element={<User />} />

// Access the parameter
function User() {
  const { id } = useParams();
  return <div>User ID: {id}</div>;
}
```

---

#### **9. What is the `useNavigate` hook, and how is it used?**

**Answer:**  
The `useNavigate` hook allows programmatic navigation.  
**Example:**

```javascript
import { useNavigate } from 'react-router-dom';

function Component() {
  const navigate = useNavigate();
  return <button onClick={() => navigate('/home')}>Go to Home</button>;
}
```

---

#### **10. How do you pass data between routes in React Router?**

**Answer:**

1. **Via URL parameters:**
    
    ```javascript
    <Route path="/user/:id" element={<User />} />
    ```
    
2. **Via state in `Link`:**
    
    ```javascript
    <Link to="/about" state={{ from: 'home' }}>About</Link>
    ```
    
    Access state in the component:
    
    ```javascript
    import { useLocation } from 'react-router-dom';
    const location = useLocation();
    console.log(location.state.from);
    ```
    

---

#### **11. What is the `Outlet` component used for?**

**Answer:**  
The `Outlet` component renders child routes in nested routing.  
**Example:**

```javascript
<Route path="/dashboard" element={<Dashboard />}>
  <Route path="stats" element={<Stats />} />
</Route>

function Dashboard() {
  return (
    <div>
      <h1>Dashboard</h1>
      <Outlet />
    </div>
  );
}
```

---

#### **12. How do you redirect in React Router?**

**Answer:**  
Use the `Navigate` component or `useNavigate` hook.

**Example: Using `Navigate`:**

```javascript
<Route path="/old-path" element={<Navigate to="/new-path" />} />
```

**Example: Using `useNavigate`:**

```javascript
const navigate = useNavigate();
navigate('/new-path');
```

---

### **Advanced-Level**

#### **13. What are lazy-loaded routes, and how do you implement them?**

**Answer:**  
Lazy loading defers the loading of components until they are needed, improving performance.

**Example:**

```javascript
import { lazy, Suspense } from 'react';
const About = lazy(() => import('./About'));

function App() {
  return (
    <Suspense fallback={<div>Loading...</div>}>
      <Routes>
        <Route path="/about" element={<About />} />
      </Routes>
    </Suspense>
  );
}
```

---

#### **14. How do you protect routes in React Router?**

**Answer:**  
Use a wrapper component to check authentication before rendering the route.  
**Example:**

```javascript
function ProtectedRoute({ children }) {
  const isAuthenticated = useAuth(); // Custom hook or logic
  return isAuthenticated ? children : <Navigate to="/login" />;
}

// Usage
<Route path="/dashboard" element={<ProtectedRoute><Dashboard /></ProtectedRoute>} />
```

---

#### **15. How can you prefetch data before rendering a route?**

**Answer:**  
Use a wrapper component to fetch data before rendering the desired component.  
**Example:**

```javascript
function DataLoader({ children }) {
  const [data, setData] = useState(null);

  useEffect(() => {
    fetch('/api/data').then((res) => res.json()).then(setData);
  }, []);

  if (!data) return <div>Loading...</div>;
  return children;
}

<Route path="/data" element={<DataLoader><DataComponent /></DataLoader>} />
```

---

#### **16. What is the `useRoutes` hook?**

**Answer:**  
`useRoutes` allows you to define routes programmatically.

**Example:**

```javascript
const routes = useRoutes([
  { path: '/', element: <Home /> },
  { path: '/about', element: <About /> },
]);

function App() {
  return routes;
}
```

---

#### **17. How do you handle query parameters in React Router?**

**Answer:**  
Use the `useSearchParams` hook.

**Example:**

```javascript
import { useSearchParams } from 'react-router-dom';

function Component() {
  const [searchParams, setSearchParams] = useSearchParams();
  const query = searchParams.get('query');

  return (
    <div>
      Search Query: {query}
      <button onClick={() => setSearchParams({ query: 'React' })}>Search React</button>
    </div>
  );
}
```

---

#### **18. How do you create a custom hook for routing logic?**

**Answer:**  
**Example:**

```javascript
function useAuthRedirect() {
  const navigate = useNavigate();
  const isAuthenticated = useAuth();

  useEffect(() => {
    if (!isAuthenticated) navigate('/login');
  }, [isAuthenticated, navigate]);
}
```

---

Let me know if you'd like examples expanded or additional questions!