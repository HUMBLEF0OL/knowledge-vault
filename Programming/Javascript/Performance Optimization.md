---
tags:
  - Programming
  - Javascript
Date: 2024-10-12
Title: Introduction to Javascript
References:
  - https://developer.mozilla.org/en-US
---
### Section 8: **JavaScript Performance Optimization**

Optimizing performance in JavaScript is crucial for creating responsive applications. This section covers techniques and best practices for improving the performance of your JavaScript code.

#### 8.1 Minification and Bundling

Minification reduces the size of JavaScript files by removing whitespace, comments, and unnecessary characters, leading to faster load times. Bundling combines multiple files into a single file, reducing the number of HTTP requests.

- **Tools**:
  - **Webpack**: A popular module bundler that can minify JavaScript.
  - **Terser**: A JavaScript parser and minifier.

**Useful Resources**:
- [MDN Minification](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Minification)
- [JavaScript.info Bundling](https://javascript.info/webpack)

---

#### 8.2 Debouncing and Throttling

Both debouncing and throttling are techniques to optimize performance by limiting the rate at which a function is called, especially during events like scrolling or resizing.

##### Debouncing
Debouncing delays the execution of a function until a certain amount of time has passed since the last time it was invoked.

```javascript
function debounce(func, delay) {
    let timeout;
    return function(...args) {
        clearTimeout(timeout);
        timeout = setTimeout(() => func.apply(this, args), delay);
    };
}

const handleResize = debounce(() => {
    console.log("Window resized");
}, 300);

window.addEventListener("resize", handleResize);
```

##### Throttling
Throttling ensures that a function is called at most once in a specified amount of time.

```javascript
function throttle(func, limit) {
    let lastFunc;
    let lastRan;
    return function(...args) {
        if (!lastRan) {
            func.apply(this, args);
            lastRan = Date.now();
        } else {
            clearTimeout(lastFunc);
            lastFunc = setTimeout(() => {
                if ((Date.now() - lastRan) >= limit) {
                    func.apply(this, args);
                    lastRan = Date.now();
                }
            }, limit - (Date.now() - lastRan));
        }
    };
}

const handleScroll = throttle(() => {
    console.log("Window scrolled");
}, 200);

window.addEventListener("scroll", handleScroll);
```

**Useful Resources**:
- [MDN Debounce](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Functions#debounce)
- [JavaScript.info Debounce and Throttle](https://javascript.info/task/debounce)

---

#### 8.3 Efficient DOM Manipulation

Minimizing direct DOM manipulations can greatly enhance performance. Instead, use techniques like batching updates and reducing reflows.

##### Example:
Instead of changing styles one by one, batch updates using a document fragment or set all at once.

```javascript
const list = document.createElement("ul");
const fragment = document.createDocumentFragment();

for (let i = 0; i < 1000; i++) {
    const li = document.createElement("li");
    li.textContent = `Item ${i + 1}`;
    fragment.appendChild(li);
}

list.appendChild(fragment); // Appending once to the DOM
document.body.appendChild(list);
```

**Useful Resources**:
- [MDN Efficient DOM Manipulation](https://developer.mozilla.org/en-US/docs/Web/API/Document/createDocumentFragment)
- [JavaScript.info DOM Performance](https://javascript.info/reflow)

---

#### 8.4 Memory Management

JavaScript automatically manages memory using garbage collection, but you can help optimize it by following best practices.

- **Avoid Global Variables**: Limit the use of global variables to reduce memory usage and conflicts.
- **Use Local Variables**: Prefer local variables inside functions to allow garbage collection to reclaim memory when the function is done.
- **Nullify References**: Set variables to `null` when they are no longer needed to help the garbage collector reclaim memory.

**Useful Resources**:
- [MDN Memory Management](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Memory_Management)
- [JavaScript.info Memory Management](https://javascript.info/garbage-collection)

---

#### 8.5 Web Workers

Web Workers allow you to run scripts in the background, separate from the main execution thread. This is useful for performing heavy computations without freezing the UI.

##### Example:
```javascript
// worker.js
self.onmessage = function(e) {
    const result = e.data * 2; // Heavy computation
    self.postMessage(result);
};

// main.js
const worker = new Worker("worker.js");
worker.onmessage = function(e) {
    console.log("Result from worker:", e.data);
};
worker.postMessage(10); // Send data to the worker
```

**Useful Resources**:
- [MDN Web Workers](https://developer.mozilla.org/en-US/docs/Web/API/Web_Workers_API/Using_web_workers)
- [JavaScript.info Web Workers](https://javascript.info/web-workers)

---

Let me know if you'd like to explore any topic further or if you're ready to move on to the next section!