---
tags:
  - Javascript
Date: 2024-10-12
Title: Scope in Javascript
References:
---
### Scope in JavaScript

Scope defines the accessibility of variables and functions at various parts of the code. Understanding scope is crucial for effective variable management and avoiding naming conflicts.

#### Types of Scope

1. **Global Scope**
   - Variables declared outside any function or block can be accessed globally throughout the script.
   ```javascript
   let globalVar = "I am global";

   function showGlobalVar() {
     console.log(globalVar); // Accessible here
   }

   showGlobalVar(); // Output: I am global
   ```

2. **Function Scope**
   - Variables declared within a function are only accessible within that function.
   ```javascript
   function myFunction() {
     let functionVar = "I am local to myFunction";
     console.log(functionVar); // Accessible here
   }

   myFunction(); // Output: I am local to myFunction
   console.log(functionVar); // ReferenceError: functionVar is not defined
   ```

3. **Block Scope**
   - Variables declared with `let` or `const` inside a block (enclosed in `{}`) are only accessible within that block.
   ```javascript
   if (true) {
     let blockVar = "I am block scoped";
     console.log(blockVar); // Accessible here
   }

   console.log(blockVar); // ReferenceError: blockVar is not defined
   ```

4. **Lexical Scope**
   - Inner functions have access to variables from their outer (enclosing) functions.
   ```javascript
   function outerFunction() {
     let outerVar = "I am from outerFunction";

     function innerFunction() {
       console.log(outerVar); // Accessible here
     }

     innerFunction(); // Output: I am from outerFunction
   }

   outerFunction();
   ```

### Summary
- **Global Scope**: Accessible everywhere.
- **Function Scope**: Accessible only within the function.
- **Block Scope**: Accessible only within the block where defined.
- **Lexical Scope**: Inner functions can access outer variables.

Understanding these scopes helps in managing variables effectively and preventing naming conflicts in your JavaScript code.