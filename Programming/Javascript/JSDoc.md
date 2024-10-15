---
tags:
  - Javascript
Date: 2024-10-12
Title: JSDoc
References:
---
**JSDoc** is a documentation tool used to generate HTML documentation from comments in JavaScript code. It helps in making your code more understandable by providing structured annotations for functions, methods, classes, parameters, and more. It’s particularly useful in large projects or collaborative environments to describe how the code is supposed to work.

Here’s a step-by-step guide to understanding and using **JSDoc**:

### 1. Basic Syntax

JSDoc comments start with `/**` and end with `*/`. Inside, you can use various tags to document different aspects of your code.

```javascript
/**
 * A brief description of the function.
 *
 * @param {Type} paramName - Description of the parameter.
 * @returns {Type} Description of the return value.
 */
function exampleFunction(paramName) {
    // Function logic
}
```

### 2. Installation

You can install JSDoc using npm:

```bash
npm install -g jsdoc
```

This installs JSDoc globally, allowing you to generate documentation from your code.

### 3. Generating Documentation

Once you have written JSDoc comments, you can generate HTML documentation using the command:

```bash
jsdoc yourfile.js
```

This will create a `docs` folder with HTML files that you can open in a browser.

---

### 4. Common JSDoc Tags

#### 4.1. `@param`

Documents a parameter for a function. You specify the type, the name, and a description.

```javascript
/**
 * Adds two numbers together.
 * 
 * @param {number} a - The first number.
 * @param {number} b - The second number.
 * @returns {number} The sum of the two numbers.
 */
function add(a, b) {
    return a + b;
}
```

#### 4.2. `@returns`

Describes the return value of a function. Specify the type and a description.

```javascript
/**
 * Concatenates two strings.
 * 
 * @param {string} firstName - The first name.
 * @param {string} lastName - The last name.
 * @returns {string} The full name.
 */
function getFullName(firstName, lastName) {
    return `${firstName} ${lastName}`;
}
```

#### 4.3. `@type`

Used to define the type of a variable, constant, or object.

```javascript
/**
 * @type {number}
 */
let count = 0;
```

#### 4.4. `@example`

Provides examples of how to use the function or method.

```javascript
/**
 * Multiplies two numbers.
 *
 * @param {number} a - The first number.
 * @param {number} b - The second number.
 * @returns {number} The product of `a` and `b`.
 *
 * @example
 * let result = multiply(3, 4);
 * console.log(result); // 12
 */
function multiply(a, b) {
    return a * b;
}
```

#### 4.5. `@constructor`

Indicates that a function is intended to be used as a constructor for creating objects.

```javascript
/**
 * Represents a person.
 *
 * @constructor
 * @param {string} name - The name of the person.
 * @param {number} age - The age of the person.
 */
function Person(name, age) {
    this.name = name;
    this.age = age;
}
```

#### 4.6. `@class`

Used to document classes in JavaScript, particularly in ES6.

```javascript
/**
 * Represents a car.
 *
 * @class
 */
class Car {
    /**
     * Create a car.
     * @param {string} model - The model of the car.
     * @param {number} year - The year the car was manufactured.
     */
    constructor(model, year) {
        this.model = model;
        this.year = year;
    }

    /**
     * Get the car's information.
     * @returns {string} The car's model and year.
     */
    getInfo() {
        return `${this.model} (${this.year})`;
    }
}
```

#### 4.7. `@property`

Describes a property of an object or a class.

```javascript
/**
 * Represents a book.
 *
 * @property {string} title - The title of the book.
 * @property {string} author - The author of the book.
 */
let book = {
    title: "1984",
    author: "George Orwell"
};
```

#### 4.8. `@deprecated`

Marks a method or property as deprecated, warning other developers not to use it.

```javascript
/**
 * This method is deprecated. Use `newMethod` instead.
 *
 * @deprecated
 */
function oldMethod() {
    // Old implementation
}

/**
 * The new and improved method.
 */
function newMethod() {
    // New implementation
}
```

#### 4.9. `@async`

Marks a function as asynchronous.

```javascript
/**
 * Fetches user data from an API.
 *
 * @async
 * @param {number} userId - The ID of the user.
 * @returns {Promise<Object>} The user data.
 */
async function fetchUserData(userId) {
    let response = await fetch(`/api/users/${userId}`);
    return response.json();
}
```

---

### 5. Advanced JSDoc Usage

#### 5.1. Documenting ES6 Modules

When using ES6 modules, you can document imports and exports.

```javascript
/**
 * @module myModule
 */

/**
 * Adds two numbers.
 * @param {number} a - The first number.
 * @param {number} b - The second number.
 * @returns {number} The sum of the two numbers.
 */
export function add(a, b) {
    return a + b;
}
```

#### 5.2. Typedefs and Custom Types

You can create custom types using `@typedef` to describe complex data structures.

```javascript
/**
 * A point in 2D space.
 * @typedef {Object} Point
 * @property {number} x - The x-coordinate.
 * @property {number} y - The y-coordinate.
 */

/**
 * Get the distance between two points.
 * 
 * @param {Point} pointA - The first point.
 * @param {Point} pointB - The second point.
 * @returns {number} The distance between the points.
 */
function getDistance(pointA, pointB) {
    // Compute distance
}
```

---

### 6. Best Practices for Writing JSDoc

- **Be descriptive**: Write clear and concise descriptions for parameters, return values, and functions. Explain the purpose and behavior of your code.
  
- **Use correct types**: Always specify the correct type for parameters and return values (`number`, `string`, `boolean`, `Array`, `Object`, etc.).

- **Use examples**: Include usage examples to make it easier for other developers to understand how to use your functions.

- **Be consistent**: Use JSDoc consistently across your codebase to maintain uniform documentation.

---

### 7. Generating Documentation with JSDoc

After adding JSDoc comments to your code, you can generate HTML documentation using the command line:

```bash
jsdoc myfile.js
```

This will generate a set of HTML files that you can view in a browser. You can also specify a custom output directory and include multiple files:

```bash
jsdoc -d docs src/
```

---

