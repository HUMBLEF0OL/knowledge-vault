---
tags:
  - Javascript
Date: 2024-10-15
Title: Strict Mode
References:
---
**Strict mode** in JavaScript is a way to opt into a more restricted variant of JavaScript. It helps catch common coding errors and "unsafe" actions, making your code more reliable, readable, and secure. It was introduced in ECMAScript 5 (ES5) and can be applied to entire scripts or individual functions.

### Enabling Strict Mode

Strict mode can be enabled by adding the following line at the beginning of a script or a function:

- For an entire script:
  ```javascript
  'use strict';
  ```

- For a specific function:
  ```javascript
  function myFunction() {
    'use strict';
    // Function code here
  }
  ```

Once strict mode is enabled, it changes the way JavaScript behaves in several ways.

### Key Features and Changes in Strict Mode

1. **Elimination of `this` Binding to `undefined`**:
   - In non-strict mode, if a function is called without an explicit context (e.g., as `myFunction()`), `this` will default to the global object (`window` in browsers).
   - In strict mode, `this` inside such functions will remain `undefined`, preventing accidental modification of the global object.
   ```javascript
   'use strict';
   function showThis() {
       console.log(this);  // undefined in strict mode, window in non-strict mode
   }
   showThis();
   ```

2. **Prevention of Accidental Global Variable Creation**:
   - In non-strict mode, assigning a value to an undeclared variable automatically creates a global variable. This can lead to unexpected behavior and bugs.
   - In strict mode, trying to assign to an undeclared variable throws a `ReferenceError`.
   ```javascript
   'use strict';
   function myFunc() {
       x = 10;  // ReferenceError: x is not defined
   }
   ```

3. **Disallows Duplicates in Object Literals or Function Parameters**:
   - In non-strict mode, you can accidentally declare duplicate property names or function parameters, which can cause confusion.
   - In strict mode, duplicate property names or parameters in functions are not allowed and will throw a `SyntaxError`.
   ```javascript
   'use strict';
   let obj = {
       name: 'John',
       name: 'Doe'  // SyntaxError: Duplicate data property in object literal
   };
   ```

4. **Elimination of `with` Statement**:
   - The `with` statement in JavaScript allows you to extend the scope chain to include an object’s properties. This can lead to confusing code and poor optimization.
   - Strict mode completely disallows the use of `with`, throwing a `SyntaxError` if used.
   ```javascript
   'use strict';
   with (Math) {  // SyntaxError: Strict mode code may not include a with statement
       console.log(sin(90));
   }
   ```

5. **Disallows Deleting Variables or Functions**:
   - In non-strict mode, you can use the `delete` operator to delete variables or functions, which can lead to bugs.
   - In strict mode, deleting variables or functions throws a `SyntaxError`.
   ```javascript
   'use strict';
   let x = 5;
   delete x;  // SyntaxError: Delete of an unqualified identifier in strict mode
   ```

6. **Securing `eval()`**:
   - In strict mode, `eval()` behaves more securely:
     - Variables or functions declared inside `eval()` do not affect the surrounding scope.
     - The use of `eval` to introduce new variables into the surrounding scope is disallowed.
   ```javascript
   'use strict';
   eval('var x = 10'); 
   console.log(x);  // ReferenceError: x is not defined
   ```

7. **Prohibits Octal Literals**:
   - In non-strict mode, numbers with leading `0` are interpreted as octal (base-8) literals.
   - Strict mode disallows octal literals and throws a `SyntaxError` if you try to use them.
   ```javascript
   'use strict';
   let num = 010;  // SyntaxError: Octal literals are not allowed in strict mode
   ```

8. **More Reserved Keywords**:
   - Strict mode reserves certain future keywords for later use in ECMAScript versions. These include `implements`, `interface`, `let`, `package`, `private`, `protected`, `public`, `static`, `yield`.
   - Using them as variable names or function names in strict mode will result in a `SyntaxError`.
   ```javascript
   'use strict';
   let implements = 5;  // SyntaxError: Unexpected strict mode reserved word
   ```

9. **Restricting Function Behavior**:
   - In strict mode, a function cannot have the same name for a parameter and a variable declared inside the function.
   - Attempting to write to read-only properties, get-only properties, or properties with setters but no corresponding getters will throw a `TypeError`.

10. **Securing `arguments` Object**:
   - In non-strict mode, the `arguments` object and the function parameters are linked, meaning that changing one changes the other.
   - In strict mode, the `arguments` object is not linked to the function parameters.
   ```javascript
   'use strict';
   function myFunc(a) {
       a = 10;
       console.log(arguments[0]);  // In strict mode, arguments[0] is still the original value, not 10
   }
   myFunc(5);  // Output: 5
   ```

### Benefits of Using Strict Mode:
1. **Improves Code Quality**: By catching common mistakes (like undeclared variables) and disallowing problematic syntax, strict mode helps you write better, cleaner code.
   
2. **Easier Debugging**: Errors are thrown where they occur, and potential issues like accidental global variable declarations are avoided.
   
3. **Improved Security**: By making certain operations illegal (such as using `with` or making certain references), strict mode helps make the code more secure and avoids unintended side effects.

4. **Better Performance**: JavaScript engines can optimize code better in strict mode since it removes certain features that inhibit performance, like the `with` statement or the dynamic scoping of variables in `eval`.

### Conclusion:
Strict mode is a powerful tool that helps you avoid common pitfalls in JavaScript development, leading to cleaner, safer, and more optimized code. It should be used in modern development practices, and when writing ES6+ code, it is often implicitly enabled in modules or classes, ensuring that you benefit from its advantages.