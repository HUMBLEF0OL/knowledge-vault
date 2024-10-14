---
tags:
  - Javascript
Date: 2024-10-12
Title: Introduction to Javascript
References:
  - https://developer.mozilla.org/en-US
---
### Section 10: **JavaScript Best Practices**

Following best practices can lead to more maintainable, efficient, and readable JavaScript code. This section outlines important conventions and techniques to consider when writing JavaScript.

#### 10.1 Use `const` and `let` Instead of `var`

- Use `const` for variables that will not be reassigned.
- Use `let` for variables that will be reassigned.
- Avoid `var` as it has function scope, which can lead to confusion.

##### Example:
```javascript
const pi = 3.14; // constant value
let count = 0;   // can be reassigned
```

**Useful Resources**:
- [MDN Variables](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Grammar_and_types#declarations)
- [JavaScript.info let, const](https://javascript.info/let-const)

---

#### 10.2 Use Strict Mode

Enabling strict mode can help you write cleaner code by enforcing stricter parsing and error handling in your JavaScript code.

##### Example:
```javascript
"use strict";

function myFunction() {
    x = 3.14; // Throws an error because x is not declared
}
myFunction();
```

**Useful Resources**:
- [MDN Strict Mode](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode)
- [JavaScript.info Strict Mode](https://javascript.info/strict-mode)

---

#### 10.3 Avoid Global Variables

Minimizing the use of global variables helps prevent naming conflicts and makes your code easier to maintain. Use closures or modules to encapsulate variables.

##### Example:
```javascript
(function() {
    let privateVariable = "I am private";
    
    function privateFunction() {
        console.log(privateVariable);
    }

    privateFunction(); // Output: I am private
})();
```

**Useful Resources**:
- [MDN Global Variables](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects)
- [JavaScript.info Global Variables](https://javascript.info/global-variables)

---

#### 10.4 Keep Your Code DRY (Don't Repeat Yourself)

Repetitive code can lead to bugs and makes maintenance harder. Use functions, modules, or classes to encapsulate reusable code.

##### Example:
```javascript
function calculateArea(width, height) {
    return width * height;
}

// Usage
const area1 = calculateArea(5, 10);
const area2 = calculateArea(2, 3);
```

**Useful Resources**:
- [MDN DRY Principle](https://developer.mozilla.org/en-US/docs/Glossary/DRY)
- [JavaScript.info DRY Principle](https://javascript.info/reusable)

---

#### 10.5 Use Descriptive Variable and Function Names

Choose clear, descriptive names for variables and functions to make your code self-documenting and easier to understand.

##### Example:
```javascript
function calculateTotalPrice(price, tax) {
    return price + (price * tax);
}
```

**Useful Resources**:
- [MDN Naming Conventions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Names_and_Values#naming_conventions)
- [JavaScript.info Naming Variables](https://javascript.info/names)

---

#### 10.6 Document Your Code

Use comments to explain complex logic or provide context about the code. Additionally, consider using JSDoc for documenting functions and their parameters.

##### Example:
```javascript
/**
 * Calculates the total price including tax.
 * @param {number} price - The base price.
 * @param {number} tax - The tax percentage (e.g., 0.2 for 20%).
 * @returns {number} The total price.
 */
function calculateTotalPrice(price, tax) {
    return price + (price * tax);
}
```

**Useful Resources**:
- [MDN Comments](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Comments)
- [JavaScript.info Documentation](https://javascript.info/intro#documentation)

---

#### 10.7 Error Handling

Use `try...catch` for error handling to prevent your application from crashing. Ensure you provide meaningful error messages to help debug issues.

##### Example:
```javascript
try {
    // Code that may throw an error
    const result = riskyFunction();
} catch (error) {
    console.error("An error occurred:", error.message);
}
```

**Useful Resources**:
- [MDN try...catch](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/try...catch)
- [JavaScript.info Error Handling](https://javascript.info/try-catch)

---

Let me know if you'd like to explore any topic further or if you're ready to move on to the next section!