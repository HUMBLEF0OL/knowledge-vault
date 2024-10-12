---
tags:
  - Programming
  - Javascript
Date: 2024-10-12
Title: Asynchronous JavaScript
References:
  - https://developer.mozilla.org/en-US
---
### Section 4: **Asynchronous JavaScript**

Asynchronous programming allows JavaScript to handle operations like network requests, file reading, or timers without blocking the main execution thread. This is crucial for building responsive web applications.

#### 4.1 Callbacks

A callback is a function passed into another function as an argument. It gets executed after the completion of the asynchronous operation.

##### Example:
```javascript
function fetchData(callback) {
    setTimeout(() => {
        const data = { id: 1, name: "Alice" };
        callback(data);
    }, 2000); // Simulates a network request
}

fetchData((data) => {
    console.log("Data received:", data); // Output: Data received: { id: 1, name: 'Alice' }
});
```

**Useful Resources**:
- [MDN Callbacks](https://developer.mozilla.org/en-US/docs/Glossary/Callback_function)
- [JavaScript.info Callbacks](https://javascript.info/callbacks)

---

#### 4.2 Promises

A promise is an object that represents the eventual completion (or failure) of an asynchronous operation. It can be in one of three states: pending, fulfilled, or rejected.

##### Creating a Promise:
```javascript
const fetchData = () => {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            const data = { id: 1, name: "Alice" };
            resolve(data); // Successfully fetched data
            // reject("Error fetching data"); // Uncomment to simulate error
        }, 2000);
    });
};

// Using the promise
fetchData()
    .then((data) => {
        console.log("Data received:", data); // Output: Data received: { id: 1, name: 'Alice' }
    })
    .catch((error) => {
        console.log(error); // Output: Error message if rejected
    });
```

**Useful Resources**:
- [MDN Promises](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)
- [JavaScript.info Promises](https://javascript.info/promise-basics)

##### Diagram: Promise States

```plaintext
+------------------+
|      Pending     |
+--------+---------+
         |
  Resolves |
         V
+--------+---------+
|     Fulfilled    |
+------------------+
         |
  Rejects  |
         V
+------------------+
|     Rejected     |
+------------------+
```

---

#### 4.3 Async/Await

`async/await` is syntactic sugar built on top of promises. It makes asynchronous code look and behave more like synchronous code, improving readability.

##### Example:
```javascript
const fetchData = () => {
    return new Promise((resolve) => {
        setTimeout(() => {
            const data = { id: 1, name: "Alice" };
            resolve(data);
        }, 2000);
    });
};

const getData = async () => {
    try {
        const data = await fetchData();
        console.log("Data received:", data); // Output: Data received: { id: 1, name: 'Alice' }
    } catch (error) {
        console.log(error);
    }
};

getData();
```

**Useful Resources**:
- [MDN async function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async_function)
- [JavaScript.info Async/Await](https://javascript.info/async)

---

#### 4.4 Error Handling

Proper error handling is essential in asynchronous programming. Using `.catch()` with promises or `try/catch` with `async/await` helps manage errors gracefully.

##### Example with Promises:
```javascript
fetchData()
    .then((data) => {
        console.log("Data received:", data);
    })
    .catch((error) => {
        console.log("Error:", error);
    });
```

##### Example with async/await:
```javascript
const getData = async () => {
    try {
        const data = await fetchData();
        console.log("Data received:", data);
    } catch (error) {
        console.log("Error:", error);
    }
};
```

**Useful Resources**:
- [MDN Error Handling](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Control_flow_and_error_handling#exception_handling)
- [JavaScript.info Error Handling](https://javascript.info/try-catch)

---

Let me know if you'd like to explore any topic further or if you're ready to proceed to the next section!