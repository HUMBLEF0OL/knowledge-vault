---
tags:
  - Javascript
Date: 2024-10-12
Title: Introduction to Javascript
References:
  - https://developer.mozilla.org/en-US
---
### Section 16: **JavaScript Fetch API**

The Fetch API provides a modern interface for making HTTP requests. It allows you to make requests to servers and handle responses in a more flexible way compared to older methods like `XMLHttpRequest`. This section covers how to use the Fetch API to make various types of HTTP requests.

#### 16.1 Introduction to Fetch

The `fetch()` function is used to initiate a request to a resource and returns a promise that resolves to the response. It is designed to work with Promises and is more powerful and flexible than older techniques.

##### Example:
```javascript
fetch('https://api.example.com/data')
    .then(response => {
        if (!response.ok) {
            throw new Error('Network response was not ok');
        }
        return response.json(); // Parse JSON response
    })
    .then(data => console.log(data))
    .catch(error => console.error('There has been a problem with your fetch operation:', error));
```

**Useful Resources**:
- [MDN Fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API)
- [JavaScript.info Fetch](https://javascript.info/fetch)

---

#### 16.2 Making GET Requests

GET requests are used to retrieve data from a server. The Fetch API makes this straightforward.

##### Example:
```javascript
fetch('https://api.example.com/items')
    .then(response => response.json())
    .then(data => {
        console.log('Items:', data);
    })
    .catch(error => console.error('Error:', error));
```

**Useful Resources**:
- [MDN GET Request](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch#making_a_get_request)
- [JavaScript.info Fetch GET](https://javascript.info/fetch#fetch)

---

#### 16.3 Making POST Requests

POST requests are used to send data to a server. You can use the `body` property to send data in the request.

##### Example:
```javascript
const data = { name: 'Alice', age: 25 };

fetch('https://api.example.com/users', {
    method: 'POST',
    headers: {
        'Content-Type': 'application/json'
    },
    body: JSON.stringify(data) // Convert object to JSON string
})
    .then(response => response.json())
    .then(data => console.log('User created:', data))
    .catch(error => console.error('Error:', error));
```

**Useful Resources**:
- [MDN POST Request](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch#making_a_post_request)
- [JavaScript.info Fetch POST](https://javascript.info/fetch#post)

---

#### 16.4 Handling Response Status

It's essential to check the response status to determine whether the request was successful or if an error occurred.

##### Example:
```javascript
fetch('https://api.example.com/data')
    .then(response => {
        if (!response.ok) {
            throw new Error(`HTTP error! Status: ${response.status}`);
        }
        return response.json();
    })
    .then(data => console.log(data))
    .catch(error => console.error('Fetch error:', error));
```

**Useful Resources**:
- [MDN Response](https://developer.mozilla.org/en-US/docs/Web/API/Response)
- [JavaScript.info Response Handling](https://javascript.info/fetch#response)

---

#### 16.5 Error Handling

Use `.catch()` to handle network errors, such as when the fetch fails or the server is unreachable.

##### Example:
```javascript
fetch('https://api.example.com/data')
    .then(response => {
        if (!response.ok) {
            throw new Error('Network response was not ok');
        }
        return response.json();
    })
    .then(data => console.log(data))
    .catch(error => {
        console.error('Fetch error:', error);
    });
```

**Useful Resources**:
- [MDN Fetch Error Handling](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch#handling_errors)
- [JavaScript.info Fetch Error Handling](https://javascript.info/fetch#handling-errors)

---

#### 16.6 Async/Await with Fetch

You can use async/await syntax for a more readable approach when working with fetch requests.

##### Example:
```javascript
const fetchData = async () => {
    try {
        const response = await fetch('https://api.example.com/data');
        if (!response.ok) {
            throw new Error('Network response was not ok');
        }
        const data = await response.json();
        console.log(data);
    } catch (error) {
        console.error('Fetch error:', error);
    }
};

fetchData();
```

**Useful Resources**:
- [MDN Async/Await](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Asynchronous/Async_await)
- [JavaScript.info Async/Await](https://javascript.info/async-await)

---

#### 16.7 Fetching Text and Other Formats

The Fetch API can handle different response types, such as text, blobs, and FormData.

##### Example:
```javascript
fetch('https://api.example.com/data.txt')
    .then(response => response.text())
    .then(text => console.log('Text response:', text))
    .catch(error => console.error('Error:', error));
```

**Useful Resources**:
- [MDN Fetch Response Types](https://developer.mozilla.org/en-US/docs/Web/API/Response#response_types)
- [JavaScript.info Fetch Text](https://javascript.info/fetch#text)

---

Let me know if you'd like to explore any topic further or if you're ready to move on to the next section!