---
tags:
  - Javascript
  - Async-Javascript
Date: 2024-10-12
Title: Promises
References:
---
#### **Introduction**
JavaScript promises are used to handle asynchronous operations, ensuring the app remains responsive while operations like API calls, file I/O, and timers run in the background.

#### **Promise Basics**
- A **Promise** represents the eventual completion (success) or failure of an asynchronous operation.
- States:
  - **Pending**: Operation hasn't completed yet.
  - **Fulfilled**: Operation completed successfully.
  - **Rejected**: Operation failed.

#### **Promise Structure**
A Promise constructor accepts an executor function (`resolve`, `reject`):

```javascript
const myPromise = new Promise((resolve, reject) => {
  // asynchronous operation
  if (/* success */) resolve('Success');
  else reject('Error');
});
```

#### **Using Promises**
- **.then()**: Handles fulfilled state.
- **.catch()**: Handles errors in the chain.
- **.finally()**: Executes regardless of fulfillment or rejection.
  
```javascript
myPromise
  .then((value) => console.log(value))  // success
  .catch((error) => console.error(error))  // error
  .finally(() => console.log('Completed'));  // cleanup
```

#### **Promise Chaining**
Promises can be chained to execute asynchronous operations sequentially:

```javascript
myPromise
  .then(result => anotherPromise(result))
  .then(finalResult => console.log(finalResult))
  .catch(error => console.error(error));
```

#### **Error Handling**
Proper error handling is vital:
- Use **.catch()** to catch errors that occur during any step of a promise chain.
  
```javascript
fetch('https://api.example.com/data')
  .then(response => response.json())
  .catch(error => console.error('Fetch error:', error));
```

Errors propagate down the chain until a `.catch()` handles them.

#### **Advanced Features**
1. **`Promise.all()`**: Waits for all promises to resolve.
    - Resolves when all succeed, rejects if any fails.
    ```javascript
    // Sample API call function that returns a promise
function fetchUserData(userId) {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            // Simulating an API call success
            resolve(`User data for user ID: ${userId}`);
        }, 1000); // Simulates a 1-second API call delay
    });
}

function fetchOrderData(orderId) {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            // Simulating an API call success
            resolve(`Order data for order ID: ${orderId}`);
        }, 1500); // Simulates a 1.5-second API call delay
    });
}

function fetchProductData(productId) {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            // Simulating an API call success
            resolve(`Product data for product ID: ${productId}`);
        }, 800); // Simulates a 0.8-second API call delay
    });
}

// Using Promise.all to fetch data concurrently
async function fetchAllData() {
    try {
        const userId = 1;
        const orderId = 2;
        const productId = 3;

        const [userData, orderData, productData] = await Promise.all([
            fetchUserData(userId),
            fetchOrderData(orderId),
            fetchProductData(productId),
        ]);

        console.log(userData);   // Output: User data for user ID: 1
        console.log(orderData);   // Output: Order data for order ID: 2
        console.log(productData);  // Output: Product data for product ID: 3
    } catch (error) {
        console.error("An error occurred:", error);
    }
}

// Execute the function to fetch all data
fetchAllData();

    ```

2. **`Promise.race()`**: Resolves/rejects as soon as the first promise settles.
    ```javascript
    Promise.race([promise1, promise2])
      .then(result => console.log(result))
      .catch(error => console.error(error));
    ```

3. **`Promise.allSettled()`**: Waits for all promises, returns array with each promise’s status (`fulfilled` or `rejected`).
    ```javascript
    Promise.allSettled([promise1, promise2])
      .then(results => results.forEach(result => console.log(result.status)));
    ```

4. **`Promise.any()`**: Resolves as soon as the first promise is fulfilled (ignores rejections).
    ```javascript
    Promise.any([promise1, promise2])
      .then(value => console.log(value))
      .catch(error => console.error('All promises rejected.'));
    ```

#### **Real-World Use Cases**
- **Fetching data**: Asynchronous API calls.
  ```javascript
  fetch('https://api.example.com/data')
    .then(response => response.json())
    .then(data => console.log(data))
    .catch(error => console.error('Fetch error:', error));
  ```

- **Wrapping callback-based functions**:
  Node.js functions like `fs.readFile()` can be wrapped into promises for modern usage.
  ```javascript
  const fs = require('fs').promises;
  
  fs.readFile('path/to/file.txt', 'utf8')
    .then(data => console.log(data))
    .catch(error => console.error('Read file error:', error));
  ```

#### **Promises vs. Async/Await**
- **async/await** simplifies working with promises.
- `async` functions return a promise; `await` pauses execution until the promise resolves or rejects.

```javascript
async function fetchData() {
  try {
    const response = await fetch('https://api.example.com/data');
    const data = await response.json();
    console.log(data);
  } catch (error) {
    console.error('Fetch error:', error);
  }
}
```

#### **Best Practices and Common Mistakes**
- **Avoid Promise Hell**: Use `Promise.all()` or async/await instead of deeply nested chains.
- **Always catch errors**: Ensure error handling using `.catch()` or `try/catch` in async functions.
- **Proper chaining**: Return promises in `.then()` to continue chaining.
Here’s a comprehensive table summarizing key aspects of Promises in JavaScript:

| **Promise Method**      | **Description**                                                                 | **Resolves When**                           | **Rejects When**                             | **Use Case**                                     |
|-------------------------|---------------------------------------------------------------------------------|---------------------------------------------|---------------------------------------------|-------------------------------------------------|
| `Promise.then()`         | Handles fulfilled Promise, chaining additional callbacks                        | The promise is fulfilled (successful)       | Can include optional rejection handler      | Process the resolved value, chain next operation |
| `Promise.catch()`        | Handles rejected Promise                                                        | N/A                                         | The promise is rejected (failure)           | Handle errors, preventing uncaught exceptions    |
| `Promise.finally()`      | Executes regardless of fulfillment or rejection                                 | After resolution (fulfilled or rejected)    | After rejection                             | Clean-up tasks, such as hiding spinners          |
| `Promise.all()`          | Resolves when all promises are fulfilled                                        | All promises resolve                        | Any promise rejects                         | Wait for multiple async operations               |
| `Promise.allSettled()`   | Resolves when all promises settle (fulfilled or rejected)                       | All promises settle                         | N/A                                         | Retrieve results of all promises (success or fail)|
| `Promise.any()`          | Resolves with the first fulfilled promise                                       | First promise fulfills                      | All promises reject                         | Return the first successful result               |
| `Promise.race()`         | Resolves or rejects with the first promise that settles                         | First promise fulfills                      | First promise rejects                       | Get result from the fastest async operation      |
| `Promise.resolve()`      | Creates a promise that resolves immediately                                     | Immediately resolves                        | N/A                                         | Useful for wrapping non-promise values in a promise|
| `Promise.reject()`       | Creates a promise that rejects immediately                                      | N/A                                         | Immediately rejects                         | Useful for returning immediate error             |

#### **Conclusion**
JavaScript promises provide a more readable, manageable approach to asynchronous programming compared to callbacks. By mastering promises, developers can improve the efficiency and clarity of their asynchronous code, especially with patterns like `async/await` for cleaner syntax.