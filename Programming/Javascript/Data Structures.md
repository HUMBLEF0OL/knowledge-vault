---
tags:
  - Javascript
Date: 2024-10-12
Title: Introduction to Javascript
References:
  - https://developer.mozilla.org/en-US
---
### Section 13: **JavaScript Data Structures**

JavaScript provides several built-in data structures that can be utilized to store and manage collections of data. This section covers the most commonly used data structures, their properties, and how to work with them effectively.

#### 13.1 Arrays

Arrays are ordered collections of values. They can hold any type of data, including objects and other arrays. Arrays are zero-indexed, meaning the first element is at index 0.

##### Example:
```javascript
const fruits = ['Apple', 'Banana', 'Cherry'];
console.log(fruits[0]); // Output: Apple
console.log(fruits.length); // Output: 3

// Adding an item
fruits.push('Date');
console.log(fruits); // Output: ['Apple', 'Banana', 'Cherry', 'Date']

// Removing an item
fruits.pop();
console.log(fruits); // Output: ['Apple', 'Banana', 'Cherry']
```

**Useful Resources**:
- [MDN Arrays](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)
- [JavaScript.info Arrays](https://javascript.info/array)

---

#### 13.2 Objects

Objects are collections of key-value pairs, where keys are strings (or Symbols) and values can be any data type. Objects are unordered and mutable.

##### Example:
```javascript
const person = {
    name: 'Alice',
    age: 25,
    greet: function() {
        console.log(`Hello, my name is ${this.name}.`);
    }
};

console.log(person.name); // Output: Alice
person.greet(); // Output: Hello, my name is Alice.
```

**Useful Resources**:
- [MDN Objects](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Working_with_Objects)
- [JavaScript.info Objects](https://javascript.info/object)

---

#### 13.3 Sets

A `Set` is a collection of unique values. Sets are useful when you want to ensure that no duplicate values are stored. They maintain the insertion order of elements.

##### Example:
```javascript
const uniqueNumbers = new Set([1, 2, 3, 2, 1]);
console.log(uniqueNumbers); // Output: Set { 1, 2, 3 }

// Adding a value
uniqueNumbers.add(4);
console.log(uniqueNumbers); // Output: Set { 1, 2, 3, 4 }

// Checking existence
console.log(uniqueNumbers.has(2)); // Output: true
console.log(uniqueNumbers.has(5)); // Output: false
```

**Useful Resources**:
- [MDN Sets](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Set)
- [JavaScript.info Set](https://javascript.info/set)

---

#### 13.4 Maps

A `Map` is a collection of key-value pairs where keys can be of any data type, including objects. Maps maintain the insertion order of elements.

##### Example:
```javascript
const map = new Map();
map.set('name', 'Alice');
map.set('age', 25);
map.set('isStudent', true);

console.log(map.get('name')); // Output: Alice
console.log(map.has('age')); // Output: true

// Iterating over a Map
map.forEach((value, key) => {
    console.log(`${key}: ${value}`);
});
// Output:
// name: Alice
// age: 25
// isStudent: true
```

**Useful Resources**:
- [MDN Maps](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map)
- [JavaScript.info Map](https://javascript.info/map-set)

---

#### 13.5 WeakSets

A `WeakSet` is similar to a `Set`, but it only holds weak references to its elements. This means that if there are no other references to an object, it can be garbage collected. WeakSets can only hold objects.

##### Example:
```javascript
const weakSet = new WeakSet();
let obj = { name: 'Alice' };
weakSet.add(obj);

console.log(weakSet.has(obj)); // Output: true

obj = null; // Now the object is eligible for garbage collection
```

**Useful Resources**:
- [MDN WeakSets](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/WeakSet)
- [JavaScript.info WeakSet](https://javascript.info/weakset)

---

#### 13.6 WeakMaps

A `WeakMap` is similar to a `Map`, but its keys must be objects, and the references to the keys are weak. This allows objects to be garbage collected if there are no other references to them.

##### Example:
```javascript
const weakMap = new WeakMap();
let obj = {};
weakMap.set(obj, 'some value');

console.log(weakMap.get(obj)); // Output: some value

obj = null; // Now the object is eligible for garbage collection
```

**Useful Resources**:
- [MDN WeakMaps](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/WeakMap)
- [JavaScript.info WeakMap](https://javascript.info/weakmap)

---

Let me know if you'd like to explore any topic further or if you're ready to move on to the next section!