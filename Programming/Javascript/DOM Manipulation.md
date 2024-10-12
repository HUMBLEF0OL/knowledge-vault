---
tags:
  - Programming
  - Javascript
Date: 2024-10-12
Title: DOM Manipulation
References:
  - https://developer.mozilla.org/en-US
---
### Section 5: **DOM Manipulation**

The Document Object Model (DOM) is a programming interface for web documents. It represents the structure of a document as a tree of objects, enabling developers to manipulate HTML and CSS using JavaScript.

#### 5.1 Selecting Elements

JavaScript provides various methods to select elements from the DOM:

##### `getElementById`:
Selects an element by its ID.

```javascript
const header = document.getElementById("header");
header.textContent = "Welcome to My Page";
```

##### `getElementsByClassName`:
Selects elements by their class name (returns a live HTMLCollection).

```javascript
const items = document.getElementsByClassName("item");
for (let item of items) {
    item.style.color = "blue"; // Changes text color to blue
}
```

##### `getElementsByTagName`:
Selects elements by their tag name (also returns a live HTMLCollection).

```javascript
const paragraphs = document.getElementsByTagName("p");
console.log(paragraphs.length); // Outputs the number of <p> elements
```

##### `querySelector` and `querySelectorAll`:
Selects elements using CSS selectors (returns a static NodeList for `querySelectorAll`).

```javascript
const firstItem = document.querySelector(".item"); // Selects the first element with class "item"
const allItems = document.querySelectorAll(".item"); // Selects all elements with class "item"
```

**Useful Resources**:
- [MDN Selecting Elements](https://developer.mozilla.org/en-US/docs/Web/API/Document/getElementById)
- [JavaScript.info DOM](https://javascript.info/dom-nodes)

---

#### 5.2 Modifying Elements

You can modify the content, attributes, and styles of selected elements.

##### Changing Text Content:
```javascript
const title = document.querySelector("h1");
title.textContent = "New Title"; // Change the text of <h1>
```

##### Changing HTML Content:
```javascript
const list = document.querySelector("ul");
list.innerHTML += "<li>New Item</li>"; // Add new list item
```

##### Changing Attributes:
```javascript
const link = document.querySelector("a");
link.setAttribute("href", "https://example.com"); // Change link URL
```

##### Changing Styles:
```javascript
const box = document.querySelector(".box");
box.style.backgroundColor = "yellow"; // Change background color
box.style.width = "200px"; // Set width
```

**Useful Resources**:
- [MDN Element Interface](https://developer.mozilla.org/en-US/docs/Web/API/Element)
- [JavaScript.info Modifying Elements](https://javascript.info/modifying-document)

---

#### 5.3 Adding and Removing Elements

You can dynamically add and remove elements from the DOM.

##### Creating and Adding Elements:
```javascript
const newItem = document.createElement("li"); // Create a new <li> element
newItem.textContent = "Another Item";
const list = document.querySelector("ul");
list.appendChild(newItem); // Append the new item to the list
```

##### Removing Elements:
```javascript
const itemToRemove = document.querySelector(".item");
itemToRemove.remove(); // Remove the selected element
```

**Useful Resources**:
- [MDN Creating Elements](https://developer.mozilla.org/en-US/docs/Web/API/Document/createElement)
- [JavaScript.info Adding and Removing Elements](https://javascript.info/DOM-append)

---

#### 5.4 Event Handling

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

**Useful Resources**:
- [MDN Events](https://developer.mozilla.org/en-US/docs/Web/Events)
- [JavaScript.info Events](https://javascript.info/event-delegation)

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

**Useful Resources**:
- [MDN Event Bubbling](https://developer.mozilla.org/en-US/docs/Web/API/Event/bubbles)
- [JavaScript.info Bubbling and Capturing](https://javascript.info/bubbling-and-capturing)

---

Let me know if you'd like to dive deeper into any specific part of this section or if you're ready to move on to the next one!