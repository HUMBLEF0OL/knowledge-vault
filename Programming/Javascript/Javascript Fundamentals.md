---
tags:
  - Programming
  - Javascript
Date: 2024-10-12
Title: Introduction to Javascript
References:
  - https://developer.mozilla.org/en-US
---
### Section 1: **JavaScript Basics**

#### 1.1 Variables and Data Types

JavaScript has three ways to declare variables:
- `var`: Function-scoped.
- `let`: Block-scoped (introduced in ES6).
- `const`: Block-scoped and read-only.

##### Example:
```javascript
var name = "John"; // Function-scoped
let age = 25;      // Block-scoped
const country = "India"; // Block-scoped and cannot be reassigned
```

**Data Types**:
- **Primitive types**: `string`, `number`, `boolean`, `null`, `undefined`, `symbol`, `bigint`.
- **Non-Primitive types**: `object` (e.g., arrays, functions).

##### Example:
```javascript
let isActive = true;      // boolean
let score = 98.5;         // number
let description = "This is a string"; // string
let car = { brand: "Toyota", year: 2020 }; // object
```

**Useful Resources**:
- [MDN Variables](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Grammar_and_types#declarations)
- [JavaScript.info Data Types](https://javascript.info/types)

##### Diagram: Variable Scoping (`var` vs `let` vs `const`)

```plaintext
+--------------------------+
| Global Scope             |
|                          |
|  var x = 10;             |
|  let y = 20;             |
|                          |
|  function test() {       |
|      var a = 1;          |
|      let b = 2;          |
|      console.log(x);     | <-- Accesses global 'x'
|      console.log(a);     | <-- Accesses local 'a'
|  }                       |
+--------------------------+
```

---

#### 1.2 Functions

JavaScript functions are first-class citizens, meaning they can be passed as arguments, returned from other functions, and stored in variables.

##### Function Declaration:
```javascript
function greet(name) {
    return `Hello, ${name}!`;
}
console.log(greet("Alice"));
```

##### Function Expression:
```javascript
const greet = function(name) {
    return `Hello, ${name}!`;
};
console.log(greet("Bob"));
```

##### Arrow Functions (ES6):
```javascript
const greet = (name) => `Hello, ${name}!`;
console.log(greet("Charlie"));
```

**Useful Resources**:
- [MDN Functions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Functions)
- [JavaScript.info Functions](https://javascript.info/function-basics)

##### Diagram: Function Declaration vs Expression

```plaintext
Function Declaration:
    function myFunc() { }
    
    Accessible before declaration (hoisting)

Function Expression:
    const myFunc = function() { };
    
    Accessible only after declaration
```

---

#### 1.3 Arrays

Arrays in JavaScript are used to store multiple values in a single variable. They are dynamic and can hold any data type.

##### Example:
```javascript
const fruits = ["Apple", "Banana", "Mango"];
console.log(fruits[0]); // Output: Apple

// Add new item
fruits.push("Orange");
console.log(fruits); // Output: ["Apple", "Banana", "Mango", "Orange"]

// Loop through array
fruits.forEach((fruit) => console.log(fruit));
```

**Common Array Methods**:
- `.push()`, `.pop()`, `.shift()`, `.unshift()`
- `.map()`, `.filter()`, `.reduce()`

**Useful Resources**:
- [MDN Arrays](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)
- [JavaScript.info Arrays](https://javascript.info/array)

##### Diagram: Array Structure

```plaintext
+-----------------------------+
|  Index  |  0  |  1  |  2  |  3  |
|  Value  | "Apple" | "Banana" | "Mango" | "Orange" |
+-----------------------------+
```

---

Would you like to move on to the next section, or expand further on any specific topic in this section?