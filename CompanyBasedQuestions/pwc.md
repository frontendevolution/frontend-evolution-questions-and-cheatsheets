---
title: "FE Questions asked in PWC"
topic: "generic"
format: "interview-questions"
difficulty: "medium"
companies: 
    -PwC
---


1. Code splitting in react
    
    Code splitting is a technique used in modern web development, especially in frameworks like React, to optimize the loading performance of web applications. It involves breaking down your application's code into smaller chunks (bundles) that can be loaded on-demand, rather than all at once when the application is initially loaded. This helps reduce the initial load time and improve the user experience.
    
    In React, code splitting is often achieved using dynamic imports. Dynamic imports allow you to load modules asynchronously, which means you can split your code into different chunks and load them only when they are actually needed. This is particularly useful for large libraries, components, or features that are not required immediately upon app startup.
    
    Here's how you can perform code splitting in React:
    
    1. **Using `React.lazy()` and `Suspense`:**
        
        The `React.lazy()` function allows you to create a dynamic import of a component. You can use it along with the `Suspense` component to handle the loading state while the component is being fetched. This approach is primarily used for splitting components.
        
        ```jsx
        import React, { lazy, Suspense } from 'react';
        
        const MyLazyComponent = lazy(() => import('./MyLazyComponent'));
        
        function App() {
          return (
            <div>
              <Suspense fallback={<div>Loading...</div>}>
                <MyLazyComponent />
              </Suspense>
            </div>
          );
        }
        
        ```
        
    2. **Using `import()` function:**
        
        You can also use the `import()` function directly to perform code splitting. This is more flexible than `React.lazy()` and can be used for splitting not just components but any part of your code.
        
        ```jsx
        import React, { Component } from 'react';
        
        class App extends Component {
          handleClick = async () => {
            const { default: MyLazyComponent } = await import('./MyLazyComponent');
            // Use MyLazyComponent here
          };
        
          render() {
            return (
              <div>
                <button onClick={this.handleClick}>Load Lazy Component</button>
              </div>
            );
          }
        }
        
        ```
        
    3. **Named Exports:**
        
        If you're exporting multiple components or objects from a module, you can also use named exports for code splitting.
        
        ```jsx
        // module.js
        export const ComponentA = /* ... */;
        export const ComponentB = /* ... */;
        
        // In your React component
        import React, { Component } from 'react';
        
        class App extends Component {
          async componentDidMount() {
            const { ComponentA, ComponentB } = await import('./module');
            // Use ComponentA and ComponentB here
          }
        
          // ...
        }
        
        ```
        
    
    Remember that while code splitting is a powerful technique, it should be used judiciously. Over-splitting your code can lead to excessive network requests, which might negatively impact performance. It's essential to find a balance between optimizing load times and minimizing the complexity introduced by asynchronous loading.
    
2. dynamic imports in react
    
    Dynamic imports in React are a way to load JavaScript modules (files) on-demand, which can help improve the performance and load times of your web application. Dynamic imports are particularly useful for splitting your code into smaller chunks that are loaded only when they are needed, reducing the initial bundle size and improving the user experience.
    
    In React, you can achieve dynamic imports using the `import()` function. This function returns a promise that resolves to the module you're importing, allowing you to use the imported module in your code.
    
    Here's how you can use dynamic imports in React:
    
    ```jsx
    import React, { Component } from 'react';
    
    class App extends Component {
      state = {
        dynamicComponent: null,
      };
    
      async componentDidMount() {
        // Dynamically import a module
        const dynamicModule = await import('./DynamicComponent');
    
        // Assuming DynamicComponent is the default export of './DynamicComponent'
        this.setState({ dynamicComponent: dynamicModule.default });
      }
    
      render() {
        const DynamicComponent = this.state.dynamicComponent;
    
        return (
          <div>
            <h1>My App</h1>
            {DynamicComponent ? <DynamicComponent /> : <p>Loading...</p>}
          </div>
        );
      }
    }
    
    export default App;
    
    ```
    
    In the above example, `DynamicComponent` is dynamically imported using the `import()` function. Once the import is resolved, the imported module can be accessed through the `default` property of the module object. We use the component when it's loaded, and until then, we show a loading indicator.
    
    Dynamic imports can be especially beneficial when combined with tools like Webpack or other bundlers that support code splitting. This allows you to create smaller bundles for different parts of your application, which can be loaded on-demand. However, remember that excessive code splitting can lead to a higher number of network requests, so it's important to find the right balance for your application's architecture.
    
    Also, note that dynamic imports are part of ECMAScript (ES) modules, so they might require a transpiler or specific configuration in older environments or browsers that don't fully support ES modules natively.
    
3. Memory leak in react
    
    A memory leak is a situation in computer programming where a program inadvertently uses more memory than it should, leading to a gradual consumption of system resources and potential performance degradation. Memory leaks can occur in any programming language, including in web development with languages like JavaScript (which is used in React).
    
    In the context of React applications, memory leaks can occur due to improper handling of memory and references, especially in long-running applications. Here are a few common scenarios that might lead to memory leaks in React:
    
    1. **Uncleared Event Listeners:** If you attach event listeners to DOM elements within your components, and these listeners are not properly removed when the component is unmounted, they can lead to memory leaks. This is because the event listeners still hold references to the component, preventing it from being garbage-collected.
    2. **Incorrect State Management:** If you retain references to objects or components in your state that are no longer needed, those references can prevent garbage collection, causing a memory leak.
    3. **Circular References:** Creating circular references, where one object references another and vice versa, can prevent both objects from being properly garbage-collected, leading to memory leaks.
    4. **Long-Lived Timers or Intervals:** If you set up timers or intervals that are not properly cleared when a component unmounts, they can continue running and keeping the component's context alive.
    5. **Improper Use of Closures:** Closures can inadvertently capture variables and keep them in memory longer than necessary, especially if they are not correctly managed.
    
    To prevent memory leaks in your React applications, here are some best practices:
    
    - **Properly manage subscriptions and event listeners:** Make sure to remove event listeners and cancel subscriptions when a component unmounts. This can be done using lifecycle methods (`componentWillUnmount` in class components) or hooks like `useEffect` with a cleanup function.
    - **Use state management libraries:** Libraries like Redux or MobX provide controlled ways to manage application state, which can help prevent unnecessary retention of data.
    - **Be cautious with closures:** Be mindful of what variables your closures capture, as they can lead to unexpected memory retention.
    - **Use the `useEffect` hook correctly:** Make sure to handle any necessary cleanup within the `useEffect` cleanup function.
    - **Avoid circular references:** Design your application architecture to avoid circular dependencies and references between objects.
    - **Use browser development tools:** Modern browsers' development tools often provide memory profiling and leak detection tools that can help identify memory leaks in your application.
    
    By following these best practices and carefully managing your application's resources, you can minimize the risk of memory leaks and maintain good performance in your React applications.
    
4. How to handle error in functional components
    
    In functional components in React, you can handle errors using the `try...catch` block within the component's body or by utilizing the `ErrorBoundary` component. Here's how you can handle errors in both ways:
    
    **1. Using `try...catch` inside the component:**
    
    ```jsx
    import React, { useState } from 'react';
    
    function MyComponent() {
      const [data, setData] = useState(null);
    
      const fetchData = async () => {
        try {
          const response = await fetch('https://api.example.com/data');
          const jsonData = await response.json();
          setData(jsonData);
        } catch (error) {
          console.error('Error fetching data:', error);
          // Handle the error, show an error message, etc.
        }
      };
    
      return (
        <div>
          <button onClick={fetchData}>Fetch Data</button>
          {/* Render the fetched data */}
        </div>
      );
    }
    
    export default MyComponent;
    
    ```
    
    **2. Using an `ErrorBoundary` component:**
    
    An `ErrorBoundary` is a higher-order component that catches errors occurring in its child components. It's a way to encapsulate components that might throw errors and provide a fallback UI to display in case of an error. Here's how you can create an `ErrorBoundary`:
    
    ```jsx
    import React, { Component } from 'react';
    
    class ErrorBoundary extends Component {
      constructor(props) {
        super(props);
        this.state = { hasError: false };
      }
    
      static getDerivedStateFromError(error) {
        return { hasError: true };
      }
    
      componentDidCatch(error, errorInfo) {
        console.error('Error caught by ErrorBoundary:', error, errorInfo);
        // You can log the error or perform other actions here
      }
    
      render() {
        if (this.state.hasError) {
          return <div>Something went wrong.</div>; // Fallback UI for errors
        }
        return this.props.children;
      }
    }
    
    export default ErrorBoundary;
    
    ```
    
    Now, you can wrap any component with the `ErrorBoundary` to catch errors:
    
    ```jsx
    import React from 'react';
    import ErrorBoundary from './ErrorBoundary';
    
    function MyComponent() {
      // Component code here
    }
    
    export default () => (
      <ErrorBoundary>
        <MyComponent />
      </ErrorBoundary>
    );
    
    ```
    
    Remember that error boundaries can only catch errors that occur during rendering, in lifecycle methods, and in the constructor of the components they wrap. They do not catch errors that happen inside event handlers, asynchronous code (like `setTimeout` or `fetch`), or during server side rendering.
    
5. Function Hoisting
    
    Hoisting is a concept in JavaScript where variable and function declarations are moved to the top of their containing scope during the compilation phase. This allows you to use variables and functions before they are actually declared in your code.
    
    However, it's important to note that only the declarations are hoisted, not the initializations. This means that while the declarations are moved to the top, the assignments or initializations remain in place.
    
    Function hoisting specifically refers to the behavior of moving function declarations to the top of their containing scope, allowing you to call functions before they are defined in your code.
    
    Here's an example to illustrate hoisting:
    
    ```jsx
    console.log(myVariable); // Output: undefined
    myFunction(); // Output: "Hello"
    
    var myVariable = "Hello";
    
    function myFunction() {
      console.log("Hello");
    }
    
    ```
    
    In this example, both the variable `myVariable` and the function `myFunction` are hoisted to the top of their containing scope. However, the variable is initialized to `undefined` because only the declaration is hoisted, not the assignment. The function can be called before its actual declaration due to function hoisting.
    
    It's important to understand hoisting, but it's generally considered good practice to declare your variables and functions before using them to avoid confusion and potential bugs. Here are a few best practices:
    
    1. **Declare variables and functions before using them:** Even though hoisting allows you to use variables and functions before their declarations, it's clearer and less error-prone to declare them first.
    2. **Avoid relying on hoisting:** Relying heavily on hoisting can make your code harder to understand and maintain. Declare your variables and functions in a logical order.
    3. **Use `let` and `const`:** Variables declared with `let` and `const` are hoisted, but they are not initialized with `undefined`. They remain in the "temporal dead zone" until the actual declaration, which can help catch potential issues.
    4. **Use function expressions:** Using function expressions (assigning functions to variables) instead of function declarations can make your code more predictable and easier to reason about.
    
    In summary, function hoisting is a behavior in JavaScript that moves function declarations to the top of their scope during compilation. While this behavior can be useful, it's recommended to write code that is clear, organized, and easy to understand, rather than relying on hoisting.
    
6. Currying
    
    Currying is a functional programming concept in which a function that takes multiple arguments is transformed into a series of functions that each take a single argument. The curried functions can be called one by one, each accepting an argument, and they return new functions until all the required arguments are provided. Once all the arguments are provided, the final result is returned.
    
    Currying is a way to achieve partial function application, where you fix a number of arguments to a function and create a new function that takes the remaining arguments. It can help in creating more reusable and flexible code.
    
    Here's an example to illustrate currying:
    
    ```jsx
    // A regular function that takes three arguments
    function add(a, b, c) {
      return a + b + c;
    }
    
    // Curried version of the same function
    function curriedAdd(a) {
      return function(b) {
        return function(c) {
          return a + b + c;
        };
      };
    }
    
    const result = curriedAdd(1)(2)(3); // Returns 6
    
    ```
    
    In this example, the `add` function takes three arguments. The `curriedAdd` function is a curried version of `add`, where each argument is taken step by step, returning new functions until all arguments are provided, and the final result is returned.
    
    Currying can be very useful in functional programming, and it has several benefits:
    
    1. **Partial Application:** You can create specialized functions by fixing some of the arguments in advance, which can lead to cleaner and more modular code.
    2. **Reusability:** Curried functions allow you to reuse smaller functions in different contexts, making your code more flexible and DRY (Don't Repeat Yourself).
    3. **Function Composition:** Currying facilitates function composition, where you can create complex functions by combining simpler functions.
    
    In modern JavaScript, you can also achieve currying using arrow functions and libraries that provide utility functions for currying, like `lodash` or `ramda`. Here's an example using arrow functions:
    
    ```jsx
    const curriedAdd = a => b => c => a + b + c;
    const result = curriedAdd(1)(2)(3); // Returns 6
    
    ```
    
    Overall, currying is a powerful technique that can enhance the modularity, reusability, and composability of your code, especially in functional programming paradigms.
    
7. Event loop
    
    The event loop is a fundamental concept in JavaScript, particularly in the context of asynchronous programming. It's a mechanism that allows JavaScript to efficiently handle asynchronous operations like timers, network requests, and user interactions while maintaining a single-threaded execution model.
    
    JavaScript is single-threaded, which means it has only one main execution thread. However, many tasks in web development are not instantaneous and might block the execution of other code. To prevent this blocking behavior, JavaScript uses the event loop to manage asynchronous tasks and ensure that the program remains responsive.
    
    Here's how the event loop works:
    
    1. **Call Stack:** JavaScript maintains a call stack, which is a data structure that keeps track of the currently executing functions. When a function is called, it's added to the top of the stack. When a function finishes executing, it's removed from the stack.
    2. **Web APIs and Callback Queue:** Asynchronous tasks like timers, DOM events, and network requests are handed off to the browser's Web APIs. These APIs are responsible for handling these tasks outside of the JavaScript runtime.
    3. **Callback Queue:** When an asynchronous task is completed, a callback function related to that task is placed in the callback queue.
    4. **Event Loop:** The event loop continuously checks the callback queue while the call stack is empty. If the call stack is empty, the event loop takes the first callback function from the queue and pushes it onto the call stack for execution.
    
    This process ensures that JavaScript can handle asynchronous operations without blocking the main execution thread. Here's a simplified example:
    
    ```jsx
    console.log('Start');
    
    setTimeout(() => {
      console.log('Timeout callback');
    }, 1000);
    
    console.log('End');
    
    ```
    
    In this example, the code execution starts by logging 'Start'. The `setTimeout` function schedules the callback to be executed after 1000 milliseconds. Then, 'End' is logged. After the specified time (1000ms), the callback is placed in the callback queue. When the call stack is empty, the event loop takes the callback from the queue and logs 'Timeout callback'.
    
    It's important to note that the event loop allows JavaScript to handle asynchronous operations, but it also means that long-running synchronous operations can block the event loop and make your application unresponsive. To avoid this, it's best to use asynchronous techniques like Promises, async/await, and callback functions effectively.
    
8. Is JS synchronous
    
    JavaScript (JS) is primarily single-threaded and synchronous by nature. This means that it executes one operation at a time, in a sequence, and it follows a synchronous execution model. Each line of code is executed in the order it appears, and the next line of code won't execute until the previous one is complete.
    
    However, JavaScript also has mechanisms for handling asynchronous operations, which are crucial for tasks that might take some time to complete, like fetching data from a server or waiting for a user interaction. While the core of JavaScript is synchronous, its asynchronous capabilities allow it to perform non-blocking operations and maintain responsiveness in various contexts, like web browsers and Node.js environments.
    
    Here are the key points to understand about JavaScript's synchronous and asynchronous nature:
    
    1. **Synchronous Execution:** By default, JavaScript code runs synchronously. Each line of code is executed one after the other, in the order they appear in the code.
    2. **Asynchronous Operations:** JavaScript can perform asynchronous operations using mechanisms like timers (`setTimeout`, `setInterval`), Promises, and callbacks. These operations allow tasks to be scheduled to run in the future or to be executed in response to events.
    3. **Event Loop:** JavaScript's event loop is responsible for managing asynchronous operations. It continuously checks for completed asynchronous tasks in the callback queue and executes them when the call stack is empty, ensuring that asynchronous tasks do not block the main thread.
    4. **Blocking vs. Non-Blocking:** JavaScript's asynchronous operations are non-blocking, meaning that they don't halt the execution of other code while waiting for the asynchronous task to complete. This enables JavaScript to maintain responsiveness even when performing tasks that might take time.
    5. **Concurrency:** While JavaScript itself is single-threaded, modern web browsers and Node.js environments provide APIs and mechanisms (like Web Workers in browsers) to achieve concurrent processing and parallelism in certain scenarios.
    
    In summary, JavaScript is inherently synchronous, but its event loop and asynchronous mechanisms allow it to efficiently handle asynchronous tasks and maintain responsiveness, making it suitable for various types of applications, including those that require interacting with servers, user interfaces, and other time-consuming operations.
    
9. forEach syntax in js
    
    The `forEach` method is used to iterate over the elements of an array in JavaScript and execute a provided function for each element. It's a convenient way to perform an action on each item without manually managing the iteration index.
    
    Here's the basic syntax of the `forEach` method:
    
    ```jsx
    array.forEach(function(currentValue, index, array) {
      // Your code here
    });
    
    ```
    
    - `currentValue`: The current element being processed in the array.
    - `index` (optional): The index of the current element being processed.
    - `array` (optional): The array that `forEach` is being applied to.
    
    Here's an example of how to use `forEach`:
    
    ```jsx
    const numbers = [1, 2, 3, 4, 5];
    
    numbers.forEach(function(number) {
      console.log(number);
    });
    
    ```
    
    This code will log each number in the `numbers` array to the console.
    
    You can also use arrow functions for more concise syntax:
    
    ```jsx
    const numbers = [1, 2, 3, 4, 5];
    
    numbers.forEach(number => {
      console.log(number);
    });
    
    ```
    
    If you want to use the index or the whole array in your `forEach` callback, you can include them as additional parameters:
    
    ```jsx
    const numbers = [1, 2, 3, 4, 5];
    
    numbers.forEach(function(number, index, array) {
      console.log(`Number: ${number}, Index: ${index}, Array: ${array}`);
    });
    
    ```
    
    Remember that `forEach` is designed for iterating over elements in an array and performing side effects, such as logging or modifying the elements. If you need to transform or process the elements and create a new array, you might want to consider using `map`.
    
10. Why thunk and saga were introduced
    
    Redux Thunk and Redux Saga are two popular middleware libraries for managing side effects in Redux applications, particularly asynchronous operations like data fetching and handling complex asynchronous flows. They were introduced to address certain challenges and provide solutions for managing asynchronous behavior in Redux-based applications.
    
    1. **Redux Thunk:**
        
        Redux Thunk is a middleware that allows you to write action creators that return functions instead of plain action objects. These functions, known as "thunks," can perform asynchronous operations and dispatch multiple actions as needed. Thunks provide a straightforward way to handle asynchronous logic while keeping action creators simple.
        
        Thunks are useful for scenarios where you need to fetch data from APIs, perform async operations, or orchestrate a series of actions. By delaying the dispatch of actions, Thunk provides a clean separation of concerns between UI components and asynchronous logic.
        
        ```jsx
        const fetchData = () => {
          return async (dispatch) => {
            dispatch({ type: 'FETCH_REQUEST' });
            try {
              const response = await fetch('https://api.example.com/data');
              const data = await response.json();
              dispatch({ type: 'FETCH_SUCCESS', payload: data });
            } catch (error) {
              dispatch({ type: 'FETCH_FAILURE', payload: error });
            }
          };
        };
        
        ```
        
    2. **Redux Saga:**
        
        Redux Saga is a middleware library that focuses on managing complex asynchronous flows and side effects in a more declarative and testable manner. It uses generator functions to describe sequences of asynchronous actions and effects.
        
        Redux Saga is particularly useful when you have scenarios with intricate asynchronous interactions, such as making multiple API calls in parallel or handling complex user interactions. It provides more advanced capabilities like cancellation, debouncing, and easy-to-test sagas in isolation.
        
        ```jsx
        function* fetchDataSaga() {
          try {
            yield put({ type: 'FETCH_REQUEST' });
            const response = yield call(fetch, 'https://api.example.com/data');
            const data = yield response.json();
            yield put({ type: 'FETCH_SUCCESS', payload: data });
          } catch (error) {
            yield put({ type: 'FETCH_FAILURE', payload: error });
          }
        }
        
        ```
        
    
    The introduction of Redux Thunk and Redux Saga helped address the challenges of handling asynchronous operations in Redux applications. Thunk provides a simple way to handle basic asynchronous tasks, while Saga offers a more structured approach for handling complex asynchronous flows. Developers can choose the middleware that best fits their application's needs and level of complexity.
    
11. How to set row and col direction in flexbox
    
    In flexbox, the terms "row" and "column" direction refer to the main axis along which flex items are laid out. When you set the flex direction to "row," items are laid out horizontally along the main axis, and when you set it to "column," items are laid out vertically.
    
    Here's how you can set the row and column direction in flexbox using CSS:
    
    1. **Row Direction (`flex-direction: row;`):**
        
        In this layout, items are laid out horizontally from left to right along the main axis.
        
        ```css
        .container {
          display: flex;
          flex-direction: row;
        }
        
        ```
        
    2. **Column Direction (`flex-direction: column;`):**
        
        In this layout, items are laid out vertically from top to bottom along the main axis.
        
        ```css
        .container {
          display: flex;
          flex-direction: column;
        }
        
        ```
        
    
    Here's a simple example with HTML and CSS to demonstrate both row and column directions:
    
    HTML:
    
    ```html
    <div class="container row">
      <div class="item">Item 1</div>
      <div class="item">Item 2</div>
      <div class="item">Item 3</div>
    </div>
    
    <div class="container column">
      <div class="item">Item 1</div>
      <div class="item">Item 2</div>
      <div class="item">Item 3</div>
    </div>
    
    ```
    
    CSS:
    
    ```css
    .container {
      display: flex;
      margin-bottom: 20px;
    }
    
    .row {
      flex-direction: row;
    }
    
    .column {
      flex-direction: column;
    }
    
    .item {
      border: 1px solid black;
      padding: 10px;
      margin: 5px;
    }
    
    ```
    
    In the above example, the first container uses the "row" direction, and the second container uses the "column" direction. You can see how the items are laid out horizontally or vertically based on the chosen flex direction.
    
    Remember that the flex direction property is applied to the flex container (the parent element), and it affects the layout of its child flex items.
    
12. Difference between article section (HTML)
    
    In HTML, both the `<article>` and `<section>` elements are used to structure content on a webpage. However, they serve slightly different purposes and have distinct semantic meanings.
    
    1. **`<article>` Element:**
    
    The `<article>` element represents a self-contained, complete composition that can be independently distributed or reused. It's often used for standalone pieces of content that could be considered a whole in themselves. This could include blog posts, news articles, forum posts, or any other content that makes sense on its own and could potentially be syndicated or shared separately from the rest of the page.
    
    Example usage of `<article>`:
    
    ```html
    <article>
      <h1>Article Title</h1>
      <p>Content of the article...</p>
      <p>More content...</p>
    </article>
    
    ```
    
    1. **`<section>` Element:**
    
    The `<section>` element is used to define a thematic grouping of content. It doesn't necessarily represent a complete, standalone piece of content like the `<article>`. Instead, it's used to group related content together for organizational purposes. A `<section>` could encompass a series of content that is related in terms of topic, subject matter, or function.
    
    Example usage of `<section>`:
    
    ```html
    <section>
      <h2>Section Title</h2>
      <p>Content related to this section...</p>
      <p>More content...</p>
    </section>
    
    ```
    
    In summary:
    
    - **`<article>`** represents a self-contained, complete composition that can stand alone and be distributed independently.
    - **`<section>`** represents a thematic grouping of content, helping to organize related content together.
    
    When deciding whether to use `<article>` or `<section>`, consider the nature of the content and its intended purpose within the context of your webpage. Use `<article>` for content that could be a standalone piece, and use `<section>` to group related content together. Properly applying these elements enhances the semantic structure of your webpage and can also have positive effects on accessibility and search engine optimization.
