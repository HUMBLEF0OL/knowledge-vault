---
tags:
  - Programming
  - Javascript
Date: 2024-10-12
Title: Objects and Object-Oriented Programming
References:
  - https://developer.mozilla.org/en-US
---
### Section 3: **Objects and Object-Oriented Programming (OOP)**

In JavaScript, objects are a fundamental part of the language. They allow you to store collections of data and more complex entities.

#### 3.1 Creating Objects

There are multiple ways to create objects in JavaScript:

##### Object Literal:
```javascript
const person = {
    name: "Alice",
    age: 30,
    greet: function() {
        console.log(`Hello, my name is ${this.name}.`);
    }
};
person.greet(); // Output: Hello, my name is Alice.
```

##### Constructor Function:
```javascript
function Person(name, age) {
    this.name = name;
    this.age = age;
    this.greet = function() {
        console.log(`Hello, my name is ${this.name}.`);
    };
}

const john = new Person("John", 25);
john.greet(); // Output: Hello, my name is John.
```

##### ES6 Class Syntax:
```javascript
class Person {
    constructor(name, age) {
        this.name = name;
        this.age = age;
    }

    greet() {
        console.log(`Hello, my name is ${this.name}.`);
    }
}

const jane = new Person("Jane", 28);
jane.greet(); // Output: Hello, my name is Jane.
```

**Useful Resources**:
- [MDN Working with Objects](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Working_with_Objects)
- [JavaScript.info Objects](https://javascript.info/object)

##### Diagram: Object Structure

```plaintext
+-----------------------+
|         Object        |
|-----------------------|
| name: "Alice"        |
| age: 30              |
| greet: function() {} |
+-----------------------+
```

---

#### 3.2 Object Properties and Methods

Objects can have properties (data) and methods (functions). You can access or modify these using dot notation or bracket notation.

##### Example:
```javascript
const car = {
    brand: "Toyota",
    year: 2020,
    start: function() {
        console.log("Car started");
    }
};

// Accessing properties
console.log(car.brand); // Output: Toyota
car.start();            // Output: Car started

// Adding a new property
car.model = "Corolla";
console.log(car.model); // Output: Corolla
```

**Useful Resources**:
- [MDN Object Properties](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Working_with_Objects#properties)
- [JavaScript.info Object Methods](https://javascript.info/object-methods)

---

#### 3.3 Prototypes

JavaScript uses prototypes for inheritance. Every object can have a prototype object from which it can inherit properties and methods.

##### Example:
```javascript
function Animal(name) {
    this.name = name;
}

Animal.prototype.speak = function() {
    console.log(`${this.name} makes a noise.`);
};

const dog = new Animal("Dog");
dog.speak(); // Output: Dog makes a noise.
```

**Useful Resources**:
- [MDN Prototypes](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Inheritance_and_the_prototype_chain)
- [JavaScript.info Prototypes](https://javascript.info/prototype-inheritance)

##### Diagram: Prototype Chain

```plaintext
+-------------------------+
|        Object           |
|-------------------------|
|         name            |
|        speak()          |
+-------------------------+
          ↑
+-------------------------+
|       Animal            |
|-------------------------|
|         name            |
+-------------------------+
          ↑
+-------------------------+
|         dog             |
|-------------------------|
|         name            |
+-------------------------+
```

---

#### 3.4 Object Destructuring

Destructuring allows you to unpack values from objects into distinct variables.

##### Example:
```javascript
const user = {
    id: 1,
    username: "Alice",
    email: "alice@example.com"
};

const { username, email } = user;
console.log(username); // Output: Alice
console.log(email);    // Output: alice@example.com
```

**Useful Resources**:
- [MDN Destructuring Assignment](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)
- [JavaScript.info Destructuring](https://javascript.info/destructuring-assignment)

---
