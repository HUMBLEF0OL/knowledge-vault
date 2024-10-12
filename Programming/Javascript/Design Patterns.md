---
tags:
  - Programming
  - Javascript
Date: 2024-10-12
Title: Introduction to Javascript
References:
  - https://developer.mozilla.org/en-US
---
### Section 7: **JavaScript Design Patterns**

Design patterns are reusable solutions to common problems in software design. Understanding these patterns can help you write better, more maintainable JavaScript code.

#### 7.1 Module Pattern

The module pattern helps in encapsulating private variables and methods, promoting the organization of code into modules.

##### Example:
```javascript
const Counter = (function() {
    let count = 0; // Private variable

    return {
        increment() {
            count++;
            console.log(count);
        },
        decrement() {
            count--;
            console.log(count);
        },
        getCount() {
            return count;
        }
    };
})();

Counter.increment(); // Output: 1
Counter.increment(); // Output: 2
Counter.decrement(); // Output: 1
console.log(Counter.getCount()); // Output: 1
```

**Useful Resources**:
- [MDN Module Pattern](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Modules)
- [JavaScript.info Module Pattern](https://javascript.info/module-pattern)

---

#### 7.2 Singleton Pattern

The singleton pattern ensures a class has only one instance and provides a global point of access to it. This is useful for managing shared resources.

##### Example:
```javascript
const Singleton = (function() {
    let instance;

    function createInstance() {
        const object = new Object("I am the instance");
        return object;
    }

    return {
        getInstance: function() {
            if (!instance) {
                instance = createInstance();
            }
            return instance;
        }
    };
})();

const instance1 = Singleton.getInstance();
const instance2 = Singleton.getInstance();

console.log(instance1 === instance2); // Output: true (same instance)
```

**Useful Resources**:
- [MDN Singleton Pattern](https://developer.mozilla.org/en-US/docs/Glossary/Singleton)
- [JavaScript.info Singleton Pattern](https://javascript.info/singleton)

---

#### 7.3 Factory Pattern

The factory pattern is used to create objects without specifying the exact class of object that will be created. It provides a simple way to instantiate objects.

##### Example:
```javascript
function Car(make, model) {
    this.make = make;
    this.model = model;
}

function Bike(make, model) {
    this.make = make;
    this.model = model;
}

function VehicleFactory() {
    this.createVehicle = function(type, make, model) {
        switch (type) {
            case "car":
                return new Car(make, model);
            case "bike":
                return new Bike(make, model);
            default:
                throw new Error("Vehicle type not supported");
        }
    };
}

const factory = new VehicleFactory();
const car = factory.createVehicle("car", "Toyota", "Corolla");
const bike = factory.createVehicle("bike", "Yamaha", "FZ");

console.log(car); // Output: Car { make: 'Toyota', model: 'Corolla' }
console.log(bike); // Output: Bike { make: 'Yamaha', model: 'FZ' }
```

**Useful Resources**:
- [MDN Factory Pattern](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Objects#factories)
- [JavaScript.info Factory Pattern](https://javascript.info/factory-pattern)

---

#### 7.4 Observer Pattern

The observer pattern is a design pattern in which an object (the subject) maintains a list of its dependents (observers) and notifies them automatically of any state changes.

##### Example:
```javascript
class Subject {
    constructor() {
        this.observers = [];
    }

    addObserver(observer) {
        this.observers.push(observer);
    }

    notifyObservers(data) {
        this.observers.forEach(observer => observer.update(data));
    }
}

class Observer {
    update(data) {
        console.log("Observer notified with data:", data);
    }
}

const subject = new Subject();
const observer1 = new Observer();
const observer2 = new Observer();

subject.addObserver(observer1);
subject.addObserver(observer2);

subject.notifyObservers("Some data"); // Notifies all observers
// Output:
// Observer notified with data: Some data
// Observer notified with data: Some data
```

**Useful Resources**:
- [MDN Observer Pattern](https://developer.mozilla.org/en-US/docs/Glossary/Observer_pattern)
- [JavaScript.info Observer Pattern](https://javascript.info/observer-pattern)

---

#### 7.5 Promise Design Pattern

Using promises can help you handle asynchronous operations in a more manageable way. The promise design pattern enables cleaner and more readable asynchronous code.

##### Example:
```javascript
const fetchData = (url) => {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            if (url) {
                resolve(`Data from ${url}`);
            } else {
                reject("No URL provided");
            }
        }, 2000);
    });
};

fetchData("https://example.com")
    .then(data => {
        console.log(data); // Output: Data from https://example.com
    })
    .catch(error => {
        console.error(error);
    });
```

**Useful Resources**:
- [MDN Promise Design Pattern](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Using_promises)
- [JavaScript.info Promise Design Pattern](https://javascript.info/promise-basics)

---

Let me know if you'd like to explore any topic further or if you're ready to move on to the next section!