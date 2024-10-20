---
tags:
  - ReactJs
Date: 2024-10-12
Title: Redux
References:
---
## React Redux

  

**[⬆ Back to Top](#table-of-contents)**

  

102. ### What is flux?

  

     _Flux_ is an _application design paradigm_ used as a replacement for the more traditional MVC pattern. It is not a framework or a library but a new kind of architecture that complements React and the concept of Unidirectional Data Flow. Facebook uses this pattern internally when working with React.

  

     The workflow between dispatcher, stores and views components with distinct inputs and outputs as follows:

  

     ![flux](images/flux.png)

  

**[⬆ Back to Top](#table-of-contents)**

  

103. ### What is Redux?

  

     _Redux_ is a predictable state container for JavaScript apps based on the _Flux design pattern_. Redux can be used together with React, or with any other view library. It is tiny (about 2kB) and has no dependencies.

  

**[⬆ Back to Top](#table-of-contents)**

  

104. ### What are the core principles of Redux?

  

     Redux follows three fundamental principles:

  

     1. **Single source of truth:** The state of your whole application is stored in an object tree within a single store. The single state tree makes it easier to keep track of changes over time and debug or inspect the application.

     2. **State is read-only:** The only way to change the state is to emit an action, an object describing what happened. This ensures that neither the views nor the network callbacks will ever write directly to the state.

     3. **Changes are made with pure functions:** To specify how the state tree is transformed by actions, you write reducers. Reducers are just pure functions that take the previous state and an action as parameters, and return the next state.

  

**[⬆ Back to Top](#table-of-contents)**

  

105. ### What are the downsides of Redux compared to Flux?

  

     Instead of saying downsides we can say that there are few compromises of using Redux over Flux. Those are as follows:

  

     1. **You will need to learn to avoid mutations:** Flux is un-opinionated about mutating data, but Redux doesn't like mutations and many packages complementary to Redux assume you never mutate the state. You can enforce this with dev-only packages like `redux-immutable-state-invariant`, Immutable.js, or instructing your team to write non-mutating code.

     2. **You're going to have to carefully pick your packages:** While Flux explicitly doesn't try to solve problems such as undo/redo, persistence, or forms, Redux has extension points such as middleware and store enhancers, and it has spawned a rich ecosystem.

     3. **There is no nice Flow integration yet:** Flux currently lets you do very impressive static type checks which Redux doesn't support yet.

  

**[⬆ Back to Top](#table-of-contents)**

  

106. ### What is the difference between `mapStateToProps()` and `mapDispatchToProps()`?

  

     `mapStateToProps()` is a utility which helps your component get updated state (which is updated by some other components):

  

     ```javascript

     const mapStateToProps = (state) => {

       return {

         todos: getVisibleTodos(state.todos, state.visibilityFilter),

       };

     };

     ```

  

     `mapDispatchToProps()` is a utility which will help your component to fire an action event (dispatching action which may cause change of application state):

  

     ```javascript

     const mapDispatchToProps = (dispatch) => {

       return {

         onTodoClick: (id) => {

           dispatch(toggleTodo(id));

         },

       };

     };

     ```

  

     It is recommended to always use the “object shorthand” form for the `mapDispatchToProps`.

  

     Redux wraps it in another function that looks like (…args) => dispatch(onTodoClick(…args)), and pass that wrapper function as a prop to your component.

  

     ```javascript

     const mapDispatchToProps = {

       onTodoClick,

     };

     ```

  

**[⬆ Back to Top](#table-of-contents)**

  

107. ### Can I dispatch an action in reducer?

  

     Dispatching an action within a reducer is an **anti-pattern**. Your reducer should be _without side effects_, simply digesting the action payload and returning a new state object. Adding listeners and dispatching actions within the reducer can lead to chained actions and other side effects.

  

**[⬆ Back to Top](#table-of-contents)**

  

108. ### How to access Redux store outside a component?

  

     You just need to export the store from the module where it created with `createStore()`. Also, it shouldn't pollute the global window object.

  

     ```javascript

     store = createStore(myReducer);

  

     export default store;

     ```

  

**[⬆ Back to Top](#table-of-contents)**

  

109. ### What are the drawbacks of MVW pattern?

  

     1. DOM manipulation is very expensive which causes applications to behave slow and inefficient.

     2. Due to circular dependencies, a complicated model was created around models and views.

     3. Lot of data changes happens for collaborative applications(like Google Docs).

     4. No way to do undo (travel back in time) easily without adding so much extra code.

  

**[⬆ Back to Top](#table-of-contents)**

  

110. ### Are there any similarities between Redux and RxJS?

  

     These libraries are very different for very different purposes, but there are some vague similarities.

  

     Redux is a tool for managing state throughout the application. It is usually used as an architecture for UIs. Think of it as an alternative to (half of) Angular. RxJS is a reactive programming library. It is usually used as a tool to accomplish asynchronous tasks in JavaScript. Think of it as an alternative to Promises. Redux uses the Reactive paradigm because the Store is reactive. The Store observes actions from a distance, and changes itself. RxJS also uses the Reactive paradigm, but instead of being an architecture, it gives you basic building blocks, Observables, to accomplish this pattern.

  

**[⬆ Back to Top](#table-of-contents)**

  

111. ### How to reset state in Redux?

  

     You need to write a _root reducer_ in your application which delegate handling the action to the reducer generated by `combineReducers()`.

  

     For example, let us take `rootReducer()` to return the initial state after `USER_LOGOUT` action. As we know, reducers are supposed to return the initial state when they are called with `undefined` as the first argument, no matter the action.

  

     ```javascript

     const appReducer = combineReducers({

       /* your app's top-level reducers */

     });

  

     const rootReducer = (state, action) => {

       if (action.type === "USER_LOGOUT") {

         state = undefined;

       }

  

       return appReducer(state, action);

     };

     ```

  

     In case of using `redux-persist`, you may also need to clean your storage. `redux-persist` keeps a copy of your state in a storage engine. First, you need to import the appropriate storage engine and then, to parse the state before setting it to undefined and clean each storage state key.

  

     ```javascript

     const appReducer = combineReducers({

       /* your app's top-level reducers */

     });

  

     const rootReducer = (state, action) => {

       if (action.type === "USER_LOGOUT") {

         Object.keys(state).forEach((key) => {

           storage.removeItem(`persist:${key}`);

         });

  

         state = undefined;

       }

  

       return appReducer(state, action);

     };

     ```

  

**[⬆ Back to Top](#table-of-contents)**

  

112. ### What is the difference between React context and React Redux?

  

     You can use **Context** in your application directly and is going to be great for passing down data to deeply nested components which what it was designed for.

  

     Whereas **Redux** is much more powerful and provides a large number of features that the Context API doesn't provide. Also, React Redux uses context internally but it doesn't expose this fact in the public API.

  

**[⬆ Back to Top](#table-of-contents)**

  

113. ### Why are Redux state functions called reducers?

  

     Reducers always return the accumulation of the state (based on all previous and current actions). Therefore, they act as a reducer of state. Each time a Redux reducer is called, the state and action are passed as parameters. This state is then reduced (or accumulated) based on the action, and then the next state is returned. You could _reduce_ a collection of actions and an initial state (of the store) on which to perform these actions to get the resulting final state.

  

**[⬆ Back to Top](#table-of-contents)**

  

114. ### How to make AJAX request in Redux?

  

     You can use `redux-thunk` middleware which allows you to define async actions.

  

     Let's take an example of fetching specific account as an AJAX call using _fetch API_:

  

     ```javascript

     export function fetchAccount(id) {

       return (dispatch) => {

         dispatch(setLoadingAccountState()); // Show a loading spinner

         fetch(`/account/${id}`, (response) => {

           dispatch(doneFetchingAccount()); // Hide loading spinner

           if (response.status === 200) {

             dispatch(setAccount(response.json)); // Use a normal function to set the received state

           } else {

             dispatch(someError);

           }

         });

       };

     }

  

     function setAccount(data) {

       return { type: "SET_Account", data: data };

     }

     ```

  

**[⬆ Back to Top](#table-of-contents)**

  

115. ### Should I keep all component's state in Redux store?

  

     Keep your data in the Redux store, and the UI related state internally in the component.

  

**[⬆ Back to Top](#table-of-contents)**

  

116. ### What is the proper way to access Redux store?

  

     The best way to access your store in a component is to use the `connect()` function, that creates a new component that wraps around your existing one. This pattern is called _Higher-Order Components_, and is generally the preferred way of extending a component's functionality in React. This allows you to map state and action creators to your component, and have them passed in automatically as your store updates.

  

     Let's take an example of `<FilterLink>` component using connect:

  

     ```javascript

     import { connect } from "react-redux";

     import { setVisibilityFilter } from "../actions";

     import Link from "../components/Link";

  

     const mapStateToProps = (state, ownProps) => ({

       active: ownProps.filter === state.visibilityFilter,

     });

  

     const mapDispatchToProps = (dispatch, ownProps) => ({

       onClick: () => dispatch(setVisibilityFilter(ownProps.filter)),

     });

  

     const FilterLink = connect(mapStateToProps, mapDispatchToProps)(Link);

  

     export default FilterLink;

     ```

  

     Due to it having quite a few performance optimizations and generally being less likely to cause bugs, the Redux developers almost always recommend using `connect()` over accessing the store directly (using context API).

  

     ```javascript

     function MyComponent {

       someMethod() {

         doSomethingWith(this.context.store);

       }

     }

     ```

  

**[⬆ Back to Top](#table-of-contents)**

  

117. ### What is the difference between component and container in React Redux?

  

     **Component** is a class or function component that describes the presentational part of your application.

  

     **Container** is an informal term for a component that is connected to a Redux store. Containers _subscribe_ to Redux state updates and _dispatch_ actions, and they usually don't render DOM elements; they delegate rendering to presentational child components.

  

**[⬆ Back to Top](#table-of-contents)**

  

118. ### What is the purpose of the constants in Redux?

  

     Constants allows you to easily find all usages of that specific functionality across the project when you use an IDE. It also prevents you from introducing silly bugs caused by typos – in which case, you will get a `ReferenceError` immediately.

  

     Normally we will save them in a single file (`constants.js` or `actionTypes.js`).

  

     ```javascript

     export const ADD_TODO = "ADD_TODO";

     export const DELETE_TODO = "DELETE_TODO";

     export const EDIT_TODO = "EDIT_TODO";

     export const COMPLETE_TODO = "COMPLETE_TODO";

     export const COMPLETE_ALL = "COMPLETE_ALL";

     export const CLEAR_COMPLETED = "CLEAR_COMPLETED";

     ```

  

     In Redux, you use them in two places:

  

     1. **During action creation:**

  

        Let's take `actions.js`:

  

        ```javascript

        import { ADD_TODO } from "./actionTypes";

  

        export function addTodo(text) {

          return { type: ADD_TODO, text };

        }

        ```

  

     2. **In reducers:**

  

        Let's create `reducer.js`:

  

        ```javascript

        import { ADD_TODO } from "./actionTypes";

  

        export default (state = [], action) => {

          switch (action.type) {

            case ADD_TODO:

              return [

                ...state,

                {

                  text: action.text,

                  completed: false,

                },

              ];

            default:

              return state;

          }

        };

        ```

  

**[⬆ Back to Top](#table-of-contents)**

  

119. ### What are the different ways to write `mapDispatchToProps()`?

  

     There are a few ways of binding _action creators_ to `dispatch()` in `mapDispatchToProps()`.

  

     Below are the possible options:

  

     ```javascript

     const mapDispatchToProps = (dispatch) => ({

       action: () => dispatch(action()),

     });

     ```

  

     ```javascript

     const mapDispatchToProps = (dispatch) => ({

       action: bindActionCreators(action, dispatch),

     });

     ```

  

     ```javascript

     const mapDispatchToProps = { action };

     ```

  

     The third option is just a shorthand for the first one.

  

**[⬆ Back to Top](#table-of-contents)**

  

120. ### What is the use of the `ownProps` parameter in `mapStateToProps()` and `mapDispatchToProps()`?

  

     If the `ownProps` parameter is specified, React Redux will pass the props that were passed to the component into your _connect_ functions. So, if you use a connected component:

  

     ```jsx harmony

     import ConnectedComponent from "./containers/ConnectedComponent";

  

     <ConnectedComponent user={"john"} />;

     ```

  

     The `ownProps` inside your `mapStateToProps()` and `mapDispatchToProps()` functions will be an object:

  

     ```javascript

     {

       user: "john";

     }

     ```

  

     You can use this object to decide what to return from those functions.

  

**[⬆ Back to Top](#table-of-contents)**

  

121. ### How to structure Redux top level directories?

  

     Most of the applications has several top-level directories as below:

  

     1. **Components**: Used for _dumb_ components unaware of Redux.

     2. **Containers**: Used for _smart_ components connected to Redux.

     3. **Actions**: Used for all action creators, where file names correspond to part of the app.

     4. **Reducers**: Used for all reducers, where files name correspond to state key.

     5. **Store**: Used for store initialization.

  

     This structure works well for small and medium size apps.

  

**[⬆ Back to Top](#table-of-contents)**

  

122. ### What is redux-saga?

  

     `redux-saga` is a library that aims to make side effects (asynchronous things like data fetching and impure things like accessing the browser cache) in React/Redux applications easier and better.

  

     It is available in NPM:

  

     ```console

     $ npm install --save redux-saga

     ```

  

**[⬆ Back to Top](#table-of-contents)**

  

123. ### What is the mental model of redux-saga?

  

     _Saga_ is like a separate thread in your application, that's solely responsible for side effects. `redux-saga` is a redux _middleware_, which means this thread can be started, paused and cancelled from the main application with normal Redux actions, it has access to the full Redux application state and it can dispatch Redux actions as well.

  

**[⬆ Back to Top](#table-of-contents)**

  

124. ### What are the differences between `call()` and `put()` in redux-saga?

  

     Both `call()` and `put()` are effect creator functions. `call()` function is used to create effect description, which instructs middleware to call the promise. `put()` function creates an effect, which instructs middleware to dispatch an action to the store.

  

     Let's take example of how these effects work for fetching particular user data.

  

     ```javascript

     function* fetchUserSaga(action) {

       // `call` function accepts rest arguments, which will be passed to `api.fetchUser` function.

       // Instructing middleware to call promise, it resolved value will be assigned to `userData` variable

       const userData = yield call(api.fetchUser, action.userId);

  

       // Instructing middleware to dispatch corresponding action.

       yield put({

         type: "FETCH_USER_SUCCESS",

         userData,

       });

     }

     ```

  

**[⬆ Back to Top](#table-of-contents)**

  

125. ### What is Redux Thunk?

  

     _Redux Thunk_ middleware allows you to write action creators that return a function instead of an action. The thunk can be used to delay the dispatch of an action, or to dispatch only if a certain condition is met. The inner function receives the store methods `dispatch()` and `getState()` as parameters.

  

**[⬆ Back to Top](#table-of-contents)**

  

126. ### What are the differences between `redux-saga` and `redux-thunk`?

  

     Both _Redux Thunk_ and _Redux Saga_ take care of dealing with side effects. In most of the scenarios, Thunk uses _Promises_ to deal with them, whereas Saga uses _Generators_. Thunk is simple to use and Promises are familiar to many developers, Sagas/Generators are more powerful but you will need to learn them. But both middleware can coexist, so you can start with Thunks and introduce Sagas when/if you need them.

  

**[⬆ Back to Top](#table-of-contents)**

  

127. ### What is Redux DevTools?

  

     _Redux DevTools_ is a live-editing time travel environment for Redux with hot reloading, action replay, and customizable UI. If you don't want to bother with installing Redux DevTools and integrating it into your project, consider using Redux DevTools Extension for Chrome and Firefox.

  

**[⬆ Back to Top](#table-of-contents)**

  

128. ### What are the features of Redux DevTools?

  

     Some of the main features of Redux DevTools are below,

  

     1. Lets you inspect every state and action payload.

     2. Lets you go back in time by _cancelling_ actions.

     3. If you change the reducer code, each _staged_ action will be re-evaluated.

     4. If the reducers throw, you will see during which action this happened, and what the error was.

     5. With `persistState()` store enhancer, you can persist debug sessions across page reloads.

  

**[⬆ Back to Top](#table-of-contents)**

  

129. ### What are Redux selectors and why use them?

  

     _Selectors_ are functions that take Redux state as an argument and return some data to pass to the component.

  

     For example, to get user details from the state:

  

     ```javascript

     const getUserData = (state) => state.user.data;

     ```

  

     These selectors have two main benefits,

  

     1. The selector can compute derived data, allowing Redux to store the minimal possible state

     2. The selector is not recomputed unless one of its arguments changes

  

**[⬆ Back to Top](#table-of-contents)**

  

130. ### What is Redux Form?

  

     _Redux Form_ works with React and Redux to enable a form in React to use Redux to store all of its state. Redux Form can be used with raw HTML5 inputs, but it also works very well with common UI frameworks like Material UI, React Widgets and React Bootstrap.

  

**[⬆ Back to Top](#table-of-contents)**

  

131. ### What are the main features of Redux Form?

  

     Some of the main features of Redux Form are:

  

     1. Field values persistence via Redux store.

     2. Validation (sync/async) and submission.

     3. Formatting, parsing and normalization of field values.

  

**[⬆ Back to Top](#table-of-contents)**

  

132. ### How to add multiple middlewares to Redux?

  

     You can use `applyMiddleware()`.

  

     For example, you can add `redux-thunk` and `logger` passing them as arguments to `applyMiddleware()`:

  

     ```javascript

     import { createStore, applyMiddleware } from "redux";

     const createStoreWithMiddleware = applyMiddleware(

       ReduxThunk,

       logger

     )(createStore);

     ```

  

**[⬆ Back to Top](#table-of-contents)**

  

133. ### How to set initial state in Redux?

  

     You need to pass initial state as second argument to createStore:

  

     ```javascript

     const rootReducer = combineReducers({

       todos: todos,

       visibilityFilter: visibilityFilter,

     });

  

     const initialState = {

       todos: [{ id: 123, name: "example", completed: false }],

     };

  

     const store = createStore(rootReducer, initialState);

     ```

  

**[⬆ Back to Top](#table-of-contents)**

  

134. ### How Relay is different from Redux?

  

     Relay is similar to Redux in that they both use a single store. The main difference is that relay only manages state originated from the server, and all access to the state is used via _GraphQL_ queries (for reading data) and mutations (for changing data). Relay caches the data for you and optimizes data fetching for you, by fetching only changed data and nothing more.

  

135. ### What is an action in Redux?

  

     _Actions_ are plain JavaScript objects or payloads of information that send data from your application to your store. They are the only source of information for the store. Actions must have a type property that indicates the type of action being performed.

  

     For example, let's take an action which represents adding a new todo item:

  

     ```

     {

       type: ADD_TODO,

       text: 'Add todo item'

     }

     ```

  

**[⬆ Back to Top](#table-of-contents)**