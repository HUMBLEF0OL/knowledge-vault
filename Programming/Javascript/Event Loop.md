---
tags:
  - Programming
  - Javascript
Date: 2024-10-12
Title: Introduction to Javascript
References:
  - https://developer.mozilla.org/en-US
---
Got it! I’ll include fundamental concepts like hoisting and the event loop in the remaining sections. Let's cover these important topics next.

### Section 22: **JavaScript Fundamentals**

This section covers fundamental concepts that are essential for understanding JavaScript's behavior and execution model.

#### 22.1 Hoisting

Hoisting is a JavaScript mechanism where variables and function declarations are moved to the top of their containing scope during compilation. This means you can use variables and functions before they are declared.

- **Variable Hoisting**: Only the declaration is hoisted, not the initialization.

##### Example:
```javascript
console.log(a); // Output: undefined
var a = 5;

console.log(b); // ReferenceError: Cannot access 'b' before initialization
let b = 10;
```

- **Function Hoisting**: Function declarations are fully hoisted, meaning you can call them before they are defined.

##### Example:
```javascript
console.log(myFunction()); // Output: "Hello, World!"

function myFunction() {
    return "Hello, World!";
}
```

**Useful Resources**:
- [MDN Hoisting](https://developer.mozilla.org/en-US/docs/Glossary/Hoisting)
- [JavaScript.info Hoisting](https://javascript.info/hoisting)

---

#### 22.2 The Event Loop

The event loop is a core concept in JavaScript that enables non-blocking I/O and asynchronous programming. It is responsible for executing code, collecting and processing events, and executing queued sub-tasks.

- **Call Stack**: This is where the execution context is stored. When a function is called, it gets added to the stack, and when it returns, it is removed.

- **Web APIs**: Browser APIs (like `setTimeout`, `DOM events`, etc.) that handle asynchronous operations outside of the JavaScript execution thread.

- **Callback Queue**: A queue where messages and events wait to be executed once the call stack is clear.

- **Event Loop**: The event loop continuously checks the call stack and the callback queue. If the call stack is empty, it pushes the first item from the callback queue to the call stack for execution.

##### Example:
```javascript
console.log("Start");

setTimeout(() => {
    console.log("Timeout");
}, 0);

console.log("End");

// Output:
// Start
// End
// Timeout
```

**Useful Resources**:
- [MDN Event Loop](https://developer.mozilla.org/en-US/docs/Web/JavaScript/EventLoop)
- [JavaScript.info Event Loop](https://javascript.info/event-loop)

---

#### 22.3 Best Practices for Understanding Fundamentals

- **Know the scope of variables**: Understand how variable declarations are hoisted to avoid unexpected behaviors.
- **Familiarize yourself with the event loop**: Understanding the event loop is key to mastering asynchronous programming in JavaScript.
- **Practice asynchronous code**: Use promises and async/await to manage asynchronous operations effectively.

**Useful Resources**:
- [MDN JavaScript Basics](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/First_steps)
- [JavaScript.info JavaScript Basics](https://javascript.info/first-steps)

---

Let me know if you'd like to continue to the next section or if you want to explore any specific topic further!