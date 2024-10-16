---
tags:
  - Javascript
  - Async-Javascript
Date: 2024-10-12
Title: Introduction to Javascript
References:
  - https://developer.mozilla.org/en-US
---
# Callbacks in JavaScript

## Introduction to Callbacks

In the world of JavaScript programming, callbacks are essential for handling asynchronous operations. They allow specific tasks to be executed only after others have completed, ensuring the smooth flow of code execution.

## Why Callbacks Are Needed

Callbacks are crucial for managing tasks such as handling HTTP requests, responding to user interactions, or executing code after a timer finishes. They ensure that actions happen in the correct order when asynchronous tasks are involved.

### Real-world Scenarios: Callbacks in Action

Callbacks play a vital role in situations such as:

- **Handling HTTP Requests:** Ensuring that code executes only after data is retrieved from an API.
- **User Interactions:** Managing actions after user events, like clicking a button or submitting a form.

## Callback Example

```javascript
function solveCase(suspect, callback) {
  // Perform task

  // Once done, call the callback
  callback(`Case Solved: ${suspect}`);
}

function celebrateSuccess(result) {
  console.log(result);
  console.log("Celebrating success!");
}

// Call the solveCase function with a callback
solveCase("Vedha", celebrateSuccess);
```

**Output:**
```
Case Solved: Vedha
Celebrating success!
```

**Explanation:**
In this example, the `solveCase` function takes a callback that is executed once the task is completed, allowing the success to be celebrated after the case is solved.

## Limitations of Callbacks

Callbacks, while powerful, can lead to nested structures that make the code difficult to maintain, known as "==Callback Hell.==" As the number of callbacks grows, the code becomes harder to read and follow.

### Callback Hell Example

```javascript
detective.solveCase("Vikram", function (result) {
  console.log(result);

  crimeBoss.getPunishment("Vedha", function (punishment) {
    console.log(punishment);

    detective.reportToSuperior("Vikram", function (report) {
      console.log(report);

      // Additional nested callbacks
    });
  });
});
```

**Explanation:**
In this example, multiple nested callbacks make the code structure complicated and harder to maintain.

## The Road Ahead: Promises and Async/Await

Understanding callbacks and their limitations is essential. In the upcoming sections, we’ll explore Promises and `async/await`, which offer cleaner ways to handle asynchronous code, avoiding the complexity of callback hell.