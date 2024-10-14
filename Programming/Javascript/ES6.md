---
tags:
  - Javascript
Date: 2024-10-12
Title: Introduction to Javascript
References:
  - https://developer.mozilla.org/en-US
---
### Section 11: **JavaScript ES6 Features**

ECMAScript 2015 (ES6) introduced many new features that enhance the JavaScript language. This section covers some of the most important features and how to use them effectively.

#### 11.1 Arrow Functions

Arrow functions provide a shorter syntax for writing functions and also lexically bind the `this` value, making them particularly useful in certain contexts.

##### Example:
```javascript
const add = (a, b) => a + b;

console.log(add(2, 3)); // Output: 5

const obj = {
    value: 42,
    getValue: () => this.value // 'this' refers to the surrounding lexical context
};

console.log(obj.getValue()); // Output: undefined
```

**Useful Resources**:
- [MDN Arrow Functions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions)
- [JavaScript.info Arrow Functions](https://javascript.info/arrow-functions)

---

#### 11.2 Template Literals

Template literals allow for multi-line strings and string interpolation, making it easier to work with strings.

##### Example:
```javascript
const name = "John";
const greeting = `Hello, ${name}! Welcome to ES6.`;

console.log(greeting); // Output: Hello, John! Welcome to ES6.

const multiLineString = `This is a string
that spans multiple lines.`;

console.log(multiLineString);
```

**Useful Resources**:
- [MDN Template Literals](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals)
- [JavaScript.info Template Literals](https://javascript.info/template-literals)

---

#### 11.3 Destructuring Assignment

Destructuring allows unpacking values from arrays or properties from objects into distinct variables, making code more concise and readable.

##### Example:
```javascript
// Array destructuring
const arr = [1, 2, 3];
const [first, second] = arr;

console.log(first); // Output: 1
console.log(second); // Output: 2

// Object destructuring
const person = { name: "Alice", age: 25 };
const { name, age } = person;

console.log(name); // Output: Alice
console.log(age); // Output: 25
```

**Useful Resources**:
- [MDN Destructuring Assignment](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)
- [JavaScript.info Destructuring Assignment](https://javascript.info/destructuring-assignment)

---

#### 11.4 Default Parameters

Default parameters allow you to initialize function parameters with default values if no values or `undefined` are passed.

##### Example:
```javascript
function multiply(a, b = 1) {
    return a * b;
}

console.log(multiply(5)); // Output: 5
console.log(multiply(5, 2)); // Output: 10
```

**Useful Resources**:
- [MDN Default Parameters](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Default_parameters)
- [JavaScript.info Default Parameters](https://javascript.info/function-basics#default-parameters)

---

#### 11.5 Spread and Rest Operators

- The **spread operator** (`...`) allows an iterable (like an array) to be expanded in places where zero or more arguments or elements are expected.
- The **rest operator** (`...`) allows you to represent an indefinite number of arguments as an array.

##### Example:
```javascript
// Spread operator
const arr1 = [1, 2, 3];
const arr2 = [4, 5, ...arr1];

console.log(arr2); // Output: [4, 5, 1, 2, 3]

// Rest operator
function sum(...numbers) {
    return numbers.reduce((acc, curr) => acc + curr, 0);
}

console.log(sum(1, 2, 3, 4)); // Output: 10
```

**Useful Resources**:
- [MDN Spread and Rest](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax)
- [JavaScript.info Spread and Rest](https://javascript.info/rest-parameter)

---

#### 11.6 Classes

ES6 introduces classes as a syntactical sugar over JavaScript's existing prototype-based inheritance. This provides a clearer and more elegant way to create objects and handle inheritance.

##### Example:
```javascript
class Animal {
    constructor(name) {
        this.name = name;
    }

    speak() {
        console.log(`${this.name} makes a noise.`);
    }
}

class Dog extends Animal {
    speak() {
        console.log(`${this.name} barks.`);
    }
}

const dog = new Dog('Rex');
dog.speak(); // Output: Rex barks.
```

**Useful Resources**:
- [MDN Classes](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes)
- [JavaScript.info Classes](https://javascript.info/class)

---

#### 11.7 Modules

ES6 introduces a module system that allows you to export and import code between files, helping to organize and encapsulate code.

##### Example:
**math.js**:
```javascript
export const add = (a, b) => a + b;
export const subtract = (a, b) => a - b;
```

**main.js**:
```javascript
import { add, subtract } from './math.js';

console.log(add(5, 3)); // Output: 8
console.log(subtract(5, 3)); // Output: 2
```

**Useful Resources**:
- [MDN Modules](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Modules)
- [JavaScript.info Modules](https://javascript.info/modules-intro)

---

Let me know if you'd like to explore any topic further or if you're ready to move on to the next section!