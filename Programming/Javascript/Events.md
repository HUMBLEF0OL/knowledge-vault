---
tags:
  - Programming
  - Javascript
Date: 2024-10-12
Title: Introduction to Javascript
References:
  - https://developer.mozilla.org/en-US
---
### Section 20: **JavaScript Events**

Events are actions or occurrences that happen in the browser, which the user can trigger or which can be triggered by the JavaScript code itself. Understanding events is crucial for creating interactive web applications. This section covers the basics of events, event handling, and event propagation.

#### 20.1 Introduction to Events

An event is an occurrence that can be detected by the browser, such as a user clicking a button, pressing a key, or submitting a form. JavaScript allows you to respond to these events by executing specific code.

**Common Events**:
- Mouse events: `click`, `dblclick`, `mouseover`, `mouseout`
- Keyboard events: `keydown`, `keyup`, `keypress`
- Form events: `submit`, `change`, `focus`, `blur`
- Window events: `load`, `resize`, `scroll`

**Useful Resources**:
- [MDN Introduction to Events](https://developer.mozilla.org/en-US/docs/Web/Events)
- [JavaScript.info Introduction to Events](https://javascript.info/introduction-browser-events)

---
####  Event Handling

JavaScript can listen for events and respond when they occur. This is crucial for interactivity in web applications.

##### Adding an Event Listener:
```javascript
const button = document.querySelector("button");
button.addEventListener("click", () => {
    alert("Button clicked!");
});
```

##### Removing an Event Listener:
```javascript
const handleClick = () => {
    alert("Button clicked!");
};

button.addEventListener("click", handleClick);
// To remove the event listener
button.removeEventListener("click", handleClick);
```

**Event Object**:
The event object provides information about the event that occurred.

```javascript
button.addEventListener("click", (event) => {
    console.log(event.target); // The element that triggered the event
});
```


---

#### 5.5 Event Bubbling and Capturing

Events in the DOM can bubble up from the target element to its parents or be captured from the parent to the target.

- **Bubbling**: The event starts from the target element and propagates upward.
- **Capturing**: The event starts from the root and goes down to the target element.

##### Example of Event Bubbling:
```javascript
document.querySelector("ul").addEventListener("click", () => {
    console.log("List clicked!");
});

document.querySelector("li").addEventListener("click", (event) => {
    console.log("Item clicked!");
    event.stopPropagation(); // Prevents further propagation
});
```

The default event propagation mechanism in JavaScript is **event bubbling**.


*To use event capturing in JavaScript, you can set up an event listener with the `useCapture` parameter set to `true`.* This tells the browser to handle the event in the capturing phase.

Here’s a step-by-step example:

1. **HTML Structure:**
   ```html
   <div id="parent">
       <button id="child">Click Me</button>
   </div>
   ```

2. **JavaScript Code:**
   ```javascript
   const parent = document.getElementById('parent');
   const child = document.getElementById('child');

   // Event listener on the parent for capturing
   parent.addEventListener('click', () => {
       console.log('Parent clicked (capturing)');
   }, true); // 'true' indicates capturing phase

   // Event listener on the child
   child.addEventListener('click', () => {
       console.log('Child clicked');
   });
   ```

### How It Works:
- When the button is clicked, the event goes through the capturing phase first, triggering the parent's event listener before the child's. The console output would be:
  ```
  Parent clicked (capturing)
  Child clicked
  ```

#### 20.2 Adding Event Listeners

You can add event listeners to elements using the `addEventListener` method. This method allows you to specify the event type and a callback function to execute when the event occurs.

##### Example:
```javascript
const button = document.getElementById("myButton");
button.addEventListener("click", () => {
    alert("Button was clicked!");
});
```

**Useful Resources**:
- [MDN addEventListener](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/addEventListener)
- [JavaScript.info addEventListener](https://javascript.info/event-details#event-listeners)

---

#### 20.3 Event Object

When an event occurs, an event object is created and passed to the event handler. This object contains information about the event, such as the type of event, the target element, and more.

##### Example:
```javascript
const button = document.getElementById("myButton");
button.addEventListener("click", (event) => {
    console.log(event.type); // Output: "click"
    console.log(event.target); // Output: <button id="myButton">...</button>
});
```

**Useful Resources**:
- [MDN Event Object](https://developer.mozilla.org/en-US/docs/Web/API/Event)
- [JavaScript.info Event Object](https://javascript.info/event-object)

---

#### 20.4 Removing Event Listeners

You can remove an event listener using the `removeEventListener` method. To remove an event listener, you need to pass the same parameters that were used when it was added.

##### Example:
```javascript
const handleClick = () => {
    alert("Button was clicked!");
};

const button = document.getElementById("myButton");
button.addEventListener("click", handleClick);

// Later in the code
button.removeEventListener("click", handleClick);
```

**Useful Resources**:
- [MDN removeEventListener](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/removeEventListener)
- [JavaScript.info removeEventListener](https://javascript.info/event-details#removing-event-listeners)

---

#### 20.5 Event Propagation

Events in the DOM can propagate in two phases: **capturing** and **bubbling**. 

- **Capturing phase**: The event starts from the root and goes down to the target element.
- **Bubbling phase**: The event starts from the target element and bubbles up to the root.

You can control the event propagation using the `stopPropagation` method to prevent the event from bubbling or capturing.

##### Example:
```html
<div id="parent">
    <button id="child">Click me!</button>
</div>

<script>
const parent = document.getElementById("parent");
const child = document.getElementById("child");

parent.addEventListener("click", () => {
    alert("Parent clicked!");
});

child.addEventListener("click", (event) => {
    alert("Child clicked!");
    event.stopPropagation(); // Prevents the parent click event from firing
});
</script>
```

**Useful Resources**:
- [MDN Event Propagation](https://developer.mozilla.org/en-US/docs/Web/JavaScript/EventLoop#event_propagation)
- [JavaScript.info Event Bubbling and Capturing](https://javascript.info/bubbling-and-capturing)

---

#### 20.6 Delegated Event Handling

Event delegation is a technique where a single event listener is added to a parent element instead of multiple listeners to individual child elements. This is useful for dynamically created elements.

##### Example:
```html
<ul id="list">
    <li>Item 1</li>
    <li>Item 2</li>
    <li>Item 3</li>
</ul>

<script>
const list = document.getElementById("list");

list.addEventListener("click", (event) => {
    if (event.target.tagName === "LI") {
        alert("List item clicked: " + event.target.textContent);
    }
});
</script>
```

**Useful Resources**:
- [MDN Event Delegation](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building_blocks/Events#event_delegation)
- [JavaScript.info Event Delegation](https://javascript.info/event-delegation)

---

#### 20.7 Best Practices for Handling Events

- **Use `addEventListener`**: This allows multiple listeners for the same event and better control over event propagation.
- **Detach listeners when not needed**: Use `removeEventListener` to prevent memory leaks.
- **Use event delegation**: Apply listeners to parent elements for efficiency, especially with dynamic content.
- **Avoid inline event handlers**: Keep JavaScript separate from HTML for better maintainability.

**Useful Resources**:
- [MDN Best Practices for Events](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Events#best_practices)
- [JavaScript.info Best Practices for Events](https://javascript.info/event-details#best-practices)

---

Let me know if you'd like to explore any topic further or if you're ready to move on to the next section!