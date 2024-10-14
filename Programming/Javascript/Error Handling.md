---
tags:
  - Javascript
Date: 2024-10-12
Title: Introduction to Javascript
References:
  - https://developer.mozilla.org/en-US
---
### Section 14: **JavaScript Error Handling**

Error handling is an important aspect of programming that allows developers to manage and respond to runtime errors effectively. This section covers different types of errors in JavaScript, as well as techniques for handling them.

#### 14.1 Types of Errors

JavaScript has several types of built-in errors that can occur during execution:

- **SyntaxError**: Occurs when there is a syntax mistake in the code.
- **ReferenceError**: Occurs when trying to access a variable that has not been declared.
- **TypeError**: Occurs when a value is not of the expected type.
- **RangeError**: Occurs when a value is not within the expected range (e.g., array length).
- **EvalError**: Occurs when the `eval()` function is used incorrectly.

##### Example:
```javascript
// SyntaxError
// console.log("Hello); // Uncaught SyntaxError: Unexpected end of input

// ReferenceError
// console.log(nonExistentVariable); // Uncaught ReferenceError: nonExistentVariable is not defined

// TypeError
const num = 42;
console.log(num.toUpperCase()); // Uncaught TypeError: num.toUpperCase is not a function
```

**Useful Resources**:
- [MDN Error Types](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Error)
- [JavaScript.info Error Handling](https://javascript.info/try-catch)

---

#### 14.2 Try...Catch

The `try...catch` statement allows you to catch errors that occur in the `try` block and handle them in the `catch` block. This helps prevent the entire script from failing due to an unhandled error.

##### Example:
```javascript
try {
    const result = riskyFunction(); // This function might throw an error
} catch (error) {
    console.error("An error occurred:", error.message);
}
```

**Useful Resources**:
- [MDN try...catch](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/try...catch)
- [JavaScript.info Try...Catch](https://javascript.info/try-catch)

---

#### 14.3 Finally Block

The `finally` block can be used with `try...catch` to execute code regardless of whether an error was thrown or not. It is useful for cleanup actions.

##### Example:
```javascript
try {
    const data = riskyFunction();
    console.log(data);
} catch (error) {
    console.error("An error occurred:", error.message);
} finally {
    console.log("This will always execute.");
}
```

**Useful Resources**:
- [MDN finally](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/try...catch#finally)
- [JavaScript.info Finally](https://javascript.info/try-catch#finally)

---

#### 14.4 Throwing Errors

You can throw your own errors using the `throw` statement. This can be useful for enforcing conditions or providing custom error messages.

##### Example:
```javascript
function checkAge(age) {
    if (age < 18) {
        throw new Error("You must be at least 18 years old.");
    }
    return "Access granted.";
}

try {
    console.log(checkAge(16));
} catch (error) {
    console.error(error.message); // Output: You must be at least 18 years old.
}
```

**Useful Resources**:
- [MDN throw](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/throw)
- [JavaScript.info Throwing Errors](https://javascript.info/throw)

---

#### 14.5 Custom Error Types

You can create custom error types by extending the built-in `Error` class. This allows you to define specific error types with additional properties or methods.

##### Example:
```javascript
class ValidationError extends Error {
    constructor(message) {
        super(message);
        this.name = "ValidationError"; // Custom error name
    }
}

function validateInput(input) {
    if (!input) {
        throw new ValidationError("Input cannot be empty.");
    }
}

try {
    validateInput("");
} catch (error) {
    console.error(`${error.name}: ${error.message}`); // Output: ValidationError: Input cannot be empty.
}
```

**Useful Resources**:
- [MDN Custom Errors](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Error#custom_errors)
- [JavaScript.info Custom Error Types](https://javascript.info/custom-errors)

---

#### 14.6 Asynchronous Error Handling

In asynchronous code, error handling can be done using `try...catch` with async/await or by attaching `.catch()` to promises.

##### Example with async/await:
```javascript
async function fetchData() {
    throw new Error("Failed to fetch data");
}

async function getData() {
    try {
        await fetchData();
    } catch (error) {
        console.error("Error:", error.message);
    }
}

getData(); // Output: Error: Failed to fetch data
```

**Useful Resources**:
- [MDN Async/Await Error Handling](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Asynchronous/Async_await#handling_errors)
- [JavaScript.info Async/Await Error Handling](https://javascript.info/async-await#errors)

---

Let me know if you'd like to explore any topic further or if you're ready to move on to the next section!