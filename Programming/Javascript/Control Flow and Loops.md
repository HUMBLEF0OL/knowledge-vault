---
tags:
  - Programming
  - Javascript
---
### 
Section 2: **Control Flow and Loops**

JavaScript provides several control flow statements that allow you to determine how the code should behave based on different conditions.

#### 2.1 Conditional Statements

##### `if...else`:
Used to execute code based on a condition.

```javascript
let age = 20;
if (age >= 18) {
    console.log("You are an adult.");
} else {
    console.log("You are a minor.");
}
```

##### `else if`:
Multiple conditions can be evaluated.

```javascript
let score = 85;
if (score >= 90) {
    console.log("Grade A");
} else if (score >= 75) {
    console.log("Grade B");
} else {
    console.log("Grade C");
}
```

##### `switch`:
Used for multiple possible conditions of a variable.

```javascript
let fruit = "Mango";
switch (fruit) {
    case "Apple":
        console.log("Apples are sweet.");
        break;
    case "Banana":
        console.log("Bananas are yellow.");
        break;
    case "Mango":
        console.log("Mangoes are tropical.");
        break;
    default:
        console.log("Unknown fruit.");
}
```

**Useful Resources**:
- [MDN Conditional Statements](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/if...else)
- [JavaScript.info Conditionals](https://javascript.info/ifelse)

##### Diagram: Conditional Flow

```plaintext
+-------------------------------+
|      if (condition)            |
|        True    |    False      |
|      Execute   |    else       |
|      code      |    block      |
+-------------------------------+
```

---

#### 2.2 Loops

Loops in JavaScript allow you to repeat a block of code based on a condition.

##### `for` Loop:
Loops through a block of code a specific number of times.

```javascript
for (let i = 0; i < 5; i++) {
    console.log(`Iteration: ${i}`);
}
```

##### `while` Loop:
Repeats as long as the condition is `true`.

```javascript
let i = 0;
while (i < 5) {
    console.log(`Count: ${i}`);
    i++;
}
```

##### `do...while` Loop:
Similar to `while`, but runs at least once, even if the condition is `false` at the beginning.

```javascript
let i = 0;
do {
    console.log(`Count: ${i}`);
    i++;
} while (i < 5);
```

##### `for...of` Loop:
Used to loop over iterable objects (like arrays).

```javascript
const colors = ["red", "green", "blue"];
for (let color of colors) {
    console.log(color);
}
```

##### `for...in` Loop:
Used to loop through the properties of an object.

```javascript
const car = { brand: "Toyota", year: 2020 };
for (let key in car) {
    console.log(`${key}: ${car[key]}`);
}
```

**Useful Resources**:
- [MDN Loops and Iteration](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Loops_and_iteration)
- [JavaScript.info Loops](https://javascript.info/while-for)

##### Diagram: Loop Flow

```plaintext
+---------------------------+
|     for (init; cond; inc)  |
|        True       | False  |
|      Execute code | Exit   |
|      Loop back    |        |
+---------------------------+

+-------------------+
|   while (cond)    |
|    True   | False |
|  Execute  | Exit  |
|   Code    |       |
+-------------------+
```

---

#### 2.3 `break` and `continue`

These statements are used to control the flow within loops.

- `break`: Terminates the loop entirely.
- `continue`: Skips the current iteration and moves to the next one.

##### Example:
```javascript
for (let i = 0; i < 10; i++) {
    if (i === 5) {
        break; // Exits the loop when i is 5
    }
    if (i === 3) {
        continue; // Skips the iteration when i is 3
    }
    console.log(i);
}
```

**Useful Resources**:
- [MDN break](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/break)
- [MDN continue](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/continue)

---

Let me know if you’d like to dive deeper into any part of this section or if you’re ready to move on to the next one!