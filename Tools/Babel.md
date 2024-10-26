---
tags:
  - Tools
Date: 2024-10-26
Title: Babel
References:
  - https://dev.to/alexeagleson/building-a-modern-web-stack-babel-3hfp
---
Certainly! Let's dive into a more detailed look at how Babel integrates with React in a modern web development environment. By the end, you’ll have a deep understanding of how to set up Babel with React from scratch, including necessary configurations, integration with Webpack, and optimizing your setup for both development and production.

---

### What is Babel?

**Babel** is a powerful JavaScript compiler that helps you write code with the latest features without worrying about browser compatibility. Babel translates JavaScript code written in **ES6+** (or ECMAScript 2015 and beyond) to an older version of JavaScript so that it can run in any environment, including older browsers. Additionally, it can convert **JSX**, the syntax used in React, to standard JavaScript.

### Why Use Babel with React?

React uses JSX, a syntax extension that allows us to write HTML-like code directly in JavaScript. Babel is crucial in transforming this JSX into JavaScript, allowing browsers to understand and render it. This setup provides the flexibility to use modern JavaScript features and JSX without compatibility issues.

---

## Step-By-Step Setup of Babel in a React Project

Let's create a basic React project with Babel, Webpack, and an initial configuration to ensure everything runs smoothly.

---

### Step 1: Initialize a New Project

Start by setting up a new project directory and initializing it as a Node.js project:

1. **Create the Project Directory**:
   ```bash
   mkdir my-react-app
   cd my-react-app
   ```

2. **Initialize npm**:
   - Run `npm init -y` to create a `package.json` file automatically, which keeps track of project dependencies and scripts.

---

### Step 2: Install Babel and Related Packages

We’ll need to install several Babel packages to handle modern JavaScript and React’s JSX syntax:

1. **Install Core Babel Packages**:
   ```bash
   npm install --save-dev @babel/core @babel/preset-env @babel/preset-react
   ```

   - **`@babel/core`**: This is the core Babel library.
   - **`@babel/preset-env`**: This preset configures Babel to transpile modern JavaScript into a version that’s widely compatible.
   - **`@babel/preset-react`**: This preset specifically converts JSX into JavaScript so React code can run in the browser.

2. **Install Babel Loader for Webpack**:
   ```bash
   npm install --save-dev babel-loader
   ```

   - **`babel-loader`**: This integrates Babel with Webpack, allowing Webpack to process JavaScript files through Babel during the build process.

---

### Step 3: Set Up Babel Configuration

Babel requires a configuration file where we specify the presets we installed above. In the root directory of your project, create a file named `.babelrc`:

1. **Create `.babelrc`**:
   - This file tells Babel which presets and plugins to use.
   - Add the following configuration:

   ```json
   {
     "presets": ["@babel/preset-env", "@babel/preset-react"]
   }
   ```

   This configuration enables Babel to understand both ES6+ features and JSX syntax.

---

### Step 4: Set Up Webpack

Webpack is a module bundler commonly used with Babel and React to compile and bundle JavaScript, CSS, images, and other assets. Here, we’ll install Webpack and configure it to work with Babel.

1. **Install Webpack and Webpack Dev Server**:
   ```bash
   npm install --save-dev webpack webpack-cli webpack-dev-server
   ```

   - **`webpack`**: The main Webpack library.
   - **`webpack-cli`**: A command-line interface for Webpack.
   - **`webpack-dev-server`**: Provides a local server with hot reloading for development.

2. **Create `webpack.config.js`**:
   - In the root directory, create a `webpack.config.js` file for Webpack’s configuration:

   ```javascript
   const path = require('path');

   module.exports = {
     entry: './src/index.js',  // entry point for our React app
     output: {
       path: path.resolve(__dirname, 'dist'),
       filename: 'bundle.js'
     },
     module: {
       rules: [
         {
           test: /\.js$/,
           exclude: /node_modules/,
           use: {
             loader: 'babel-loader'
           }
         }
       ]
     },
     devServer: {
       contentBase: './dist',  // directory where Webpack Dev Server will serve files
       port: 3000  // change the port if 3000 is occupied
     }
   };
   ```

   - **`entry`**: Specifies the entry file for Webpack. This is typically `index.js` in the `src` directory.
   - **`output`**: Specifies the output path and filename for the compiled JavaScript.
   - **`module.rules`**: Tells Webpack to use `babel-loader` for `.js` files, excluding files in `node_modules`.

---

### Step 5: Write React Code

Now that Babel and Webpack are set up, let’s create a simple React app to test the setup.

1. **Create the `src` Directory**:
   - Inside your project, create a `src` folder to store source files:
     ```bash
     mkdir src
     ```

2. **Create `App.js`**:
   - In the `src` folder, create `App.js` to define a simple React component:

     ```javascript
     import React from 'react';

     const App = () => <h1>Hello, Babel with React!</h1>;

     export default App;
     ```

3. **Create `index.js`**:
   - Also in the `src` folder, create `index.js` as the entry file for Webpack:

     ```javascript
     import React from 'react';
     import ReactDOM from 'react-dom';
     import App from './App';

     ReactDOM.render(<App />, document.getElementById('root'));
     ```

4. **Create `index.html`**:
   - Create an `index.html` file in a new `dist` folder as the main HTML file:

     ```html
     <!DOCTYPE html>
     <html lang="en">
       <head>
         <meta charset="UTF-8">
         <meta name="viewport" content="width=device-width, initial-scale=1.0">
         <title>My React App</title>
       </head>
       <body>
         <div id="root"></div>
         <script src="bundle.js"></script>
       </body>
     </html>
     ```

---

### Step 6: Add Scripts in `package.json`

To make it easier to build and serve the app, add scripts to `package.json`:

```json
"scripts": {
  "build": "webpack --mode production",
  "start": "webpack serve --mode development --open"
}
```

- **`build`**: Builds the project for production.
- **`start`**: Starts the development server.

---

### Step 7: Test the Setup

1. **Start the Development Server**:
   - Run the following command to start Webpack Dev Server and open the app in your browser:
     ```bash
     npm start
     ```

2. **Build for Production**:
   - To test the production build, run:
     ```bash
     npm run build
     ```

   - This command creates an optimized bundle in the `dist` folder, ready for deployment.

---

### Additional Tips for Babel and React

- **Using Babel Plugins**: Plugins add extra functionality to Babel, such as additional transformations or optimizations. Explore plugins like `@babel/plugin-transform-runtime` for optimizing code.
  
- **Environment-specific Configurations**: Customize Babel’s `.babelrc` or Webpack config based on environment (development or production) for optimized performance and debugging.

Using polyfills with Babel helps ensure that modern JavaScript features (like Promises, Array methods, or newer APIs like `fetch`) are supported in older browsers. Here’s a comprehensive guide on how to integrate polyfills into a project using Babel.

### What is a Polyfill?

A **polyfill** is code that provides modern functionality on older browsers that do not natively support it. For example, older browsers may not support ES6 methods like `Array.prototype.includes()`, so a polyfill fills in that gap.

---

## Adding Polyfills with Babel

Babel itself can handle some syntax transformations, but it doesn't add APIs like `Promise` or `fetch` by default. For that, we need to use **Babel’s polyfill solution** through `core-js` and `@babel/preset-env`.

### Step 1: Install `core-js` and `@babel/preset-env`

1. **Install `core-js`**:
   - `core-js` provides many modern JavaScript features in the form of polyfills.
   ```bash
   npm install core-js
   ```

2. **Install `@babel/runtime`** (optional but recommended for optimization):
   - This helps reduce code duplication by automatically including only necessary polyfills.
   ```bash
   npm install --save @babel/runtime
   ```

3. **Install `@babel/preset-env`**:
   - You may already have this installed if you set up Babel following the earlier guide, but this preset manages which polyfills are needed based on browser targets.
   ```bash
   npm install --save-dev @babel/preset-env
   ```

---

### Step 2: Configure Babel to Use Polyfills

Babel's `@babel/preset-env` allows you to specify which environments (browsers) you want to support. Based on this configuration, it can automatically include necessary polyfills from `core-js`.

#### Update `.babelrc`

In your `.babelrc` file, configure `@babel/preset-env` to use `core-js`:

```json
{
  "presets": [
    [
      "@babel/preset-env",
      {
        "useBuiltIns": "usage",
        "corejs": 3
      }
    ],
    "@babel/preset-react"
  ]
}
```

Here’s a breakdown:
- **`useBuiltIns`**: Controls how Babel injects polyfills.
  - **`"usage"`**: Only includes polyfills for features that you actually use in your code.
  - **`"entry"`**: Includes polyfills for all features required by your specified environment, regardless of whether they are used.
- **`corejs: 3`**: Specifies the version of `core-js` to use. `core-js@3` is the most recent, providing better support for new JavaScript features.

---

### Step 3: Add a Polyfill Entry Point (if using `"entry"`)

If you set `"useBuiltIns"` to `"entry"`, you need to import `core-js` at the top of your main entry file (`src/index.js` or similar):

```javascript
import "core-js/stable";
import "regenerator-runtime/runtime"; // for async/await support if needed
```

### Choosing Between `"usage"` and `"entry"`

- **`"usage"`** (recommended for most projects): Only includes polyfills for features you’re actually using, leading to a smaller bundle.
- **`"entry"`**: Includes all polyfills needed for the environment you’re targeting. This can increase the bundle size but is useful if you want to ensure complete compatibility.

---

### Example: Using Polyfills in a Project

Imagine you’re using `Array.prototype.includes` in a React component, which isn't supported by older browsers like Internet Explorer.

1. **React Component Example**:
   ```javascript
   // src/App.js
   import React from "react";

   const App = () => {
     const arr = [1, 2, 3];
     const hasTwo = arr.includes(2); // Modern JS feature needing polyfill in older browsers

     return <h1>{hasTwo ? "Array includes 2" : "Array does not include 2"}</h1>;
   };

   export default App;
   ```

2. **With `"useBuiltIns": "usage"` in `.babelrc`**, Babel will detect `Array.prototype.includes` and only include the necessary polyfill code for that feature.

---

### Step 4: Testing Polyfills

1. **Build the Project**:
   ```bash
   npm run build
   ```

2. **Testing in Older Browsers**:
   - Use a tool like **BrowserStack** or **Sauce Labs** to run your code in older browsers.
   - You can also use browser dev tools (in Chrome or Firefox) to simulate older environments.

---

### Optional Step: Optimizing Polyfills with `@babel/plugin-transform-runtime`

The `@babel/plugin-transform-runtime` plugin helps to:
- Avoid duplicating polyfills in multiple files.
- Optimize code by reusing helper functions across files.

1. **Install the Plugin**:
   ```bash
   npm install --save-dev @babel/plugin-transform-runtime
   ```

2. **Configure `.babelrc`**:
   ```json
   {
     "presets": [
       [
         "@babel/preset-env",
         {
           "useBuiltIns": "usage",
           "corejs": 3
         }
       ],
       "@babel/preset-react"
     ],
     "plugins": ["@babel/plugin-transform-runtime"]
   }
   ```

   This ensures that Babel doesn’t duplicate polyfills or helper functions across files, reducing the overall bundle size.

---

By using `core-js`, `@babel/preset-env`, and configuring Babel correctly, you can ensure that your React app will support modern JavaScript features even in older browsers. Let me know if you’d like further information on testing polyfills or optimizing bundles!