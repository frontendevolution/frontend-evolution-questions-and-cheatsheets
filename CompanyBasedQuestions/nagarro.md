---
title: "FE Questions asked in Nagarro"
topic: "generic"
format: "interview-questions"
framework: "Interview Questions"
difficulty: "medium"
description: "10 interview questions asked in Nagarro"
companies: []
publishedAt: "2026-07-31"
---



1. What are css preprocessors?
    
    CSS preprocessors are scripting languages that extend the capabilities of CSS (Cascading Style Sheets), which is the standard language used for styling web pages. Preprocessors provide additional features and functionality that make it easier and more efficient to write and manage CSS code.
    
    Here are some common CSS preprocessors:
    
    1. **Sass (Syntactically Awesome Stylesheets):**
    Sass is one of the most popular CSS preprocessors. It introduces features like variables, nesting, mixins, and functions, allowing for more modular and maintainable CSS code. Sass files use the `.scss` extension.
    2. **Less:**
    Less is another widely used CSS preprocessor that extends CSS with features like variables, nesting, and functions. Less files use the `.less` extension.
    3. **Stylus:**
    Stylus is a preprocessor that offers a more minimal and flexible syntax compared to Sass and Less. It supports features like variables, nesting, and mathematical operations. Stylus files typically use the `.styl` extension.
    4. **PostCSS:**
    PostCSS is a tool rather than a preprocessor, but it's often used in combination with preprocessors. It allows for the transformation and manipulation of CSS using plugins. PostCSS can be configured to process CSS in a way similar to preprocessors.
    
    Benefits of using CSS preprocessors include:
    
    - **Modularity:** Preprocessors allow for code modularity through features like nesting, mixins, and functions, making the CSS code more organized and easier to maintain.
    - **Reusability:** Preprocessors enable the reuse of code snippets (mixins) and values (variables), reducing redundancy and improving efficiency in development.
    - **Easier Maintenance:** Preprocessors help in writing cleaner, more maintainable code by providing a structured approach to CSS organization.
    - **Mathematical Operations:** Some preprocessors allow for mathematical operations within the stylesheet, enabling dynamic calculations for properties like widths, margins, and padding.
    - **Cross-browser Compatibility:** Preprocessors can help manage vendor prefixes and other browser-specific properties, ensuring better cross-browser compatibility.
    
    In summary, CSS preprocessors enhance the capabilities of CSS by providing features like variables, nesting, mixins, functions, and more, to facilitate efficient and maintainable stylesheets for web development.
    
2. Create custom prototype chain
    
    In JavaScript, the prototype chain is a fundamental concept that allows objects to inherit properties and methods from other objects. To create a custom prototype chain, we'll demonstrate how to define multiple constructors and link their prototypes to achieve inheritance.
    
    Let's create a simple example where we have two constructors: `Animal` and `Dog`, with `Dog` inheriting from `Animal`.
    
    ```jsx
    // Constructor for Animal
    function Animal(name) {
      this.name = name;
    }
    
    // Adding a method to Animal prototype
    Animal.prototype.sayName = function() {
      console.log('My name is ' + this.name);
    };
    
    // Constructor for Dog, inheriting from Animal
    function Dog(name, breed) {
      Animal.call(this, name); // Call the Animal constructor to set the name
      this.breed = breed;
    }
    
    // Linking Dog's prototype to Animal's prototype for inheritance
    Dog.prototype = Object.create(Animal.prototype);
    Dog.prototype.constructor = Dog; // Fixing the constructor property
    
    // Adding a method to Dog prototype
    Dog.prototype.bark = function() {
      console.log('Woof!');
    };
    
    // Creating instances of Animal and Dog
    const animal = new Animal('Generic Animal');
    const dog = new Dog('Buddy', 'Labrador');
    
    // Using the methods from the prototype chain
    animal.sayName(); // Output: My name is Generic Animal
    dog.sayName();    // Output: My name is Buddy
    dog.bark();       // Output: Woof!
    
    ```
    
    In this example, we define two constructors: `Animal` and `Dog`. The `Animal` constructor sets the `name` property and defines a method `sayName()`. The `Dog` constructor calls the `Animal` constructor to set the name and adds a `breed` property. We link `Dog.prototype` to `Animal.prototype` to establish the prototype chain for inheritance.
    
    Now, instances of `Dog` inherit properties and methods from both `Animal` and `Dog`, thanks to the prototype chain.
    
3. Inheritance without ES6
    
    In JavaScript, you can achieve inheritance without ES6 (ECMAScript 2015) classes by using constructor functions and prototypes. Here's an example of how you can create a simple inheritance hierarchy using this approach:
    
    ```jsx
    // Parent constructor function
    function Animal(name) {
      this.name = name;
    }
    
    // Adding a method to the Animal prototype
    Animal.prototype.sayName = function() {
      console.log('My name is ' + this.name);
    };
    
    // Child constructor function inheriting from Animal
    function Dog(name, breed) {
      Animal.call(this, name); // Call the Animal constructor to set the name
      this.breed = breed;
    }
    
    // Set Dog's prototype to a new instance of Animal
    Dog.prototype = Object.create(Animal.prototype);
    Dog.prototype.constructor = Dog; // Fixing the constructor property
    
    // Adding a method to the Dog prototype
    Dog.prototype.bark = function() {
      console.log('Woof!');
    };
    
    // Creating instances of Animal and Dog
    const animal = new Animal('Generic Animal');
    const dog = new Dog('Buddy', 'Labrador');
    
    // Using the methods from the prototype chain
    animal.sayName(); // Output: My name is Generic Animal
    dog.sayName();    // Output: My name is Buddy
    dog.bark();       // Output: Woof!
    
    ```
    
    In this example, we use constructor functions `Animal` and `Dog` to create objects. We set up the prototype chain by creating a new object with `Object.create` and linking `Dog.prototype` to a new instance of `Animal.prototype`.
    
    The `Animal` constructor sets the `name` property and defines a method `sayName()`, while the `Dog` constructor calls the `Animal` constructor to set the name and adds a `breed` property. Both constructors use the prototype chain for inheritance, allowing instances of `Dog` to access properties and methods defined in both `Animal` and `Dog`.
    
4. Pass data from child to parent without callbacks in react
    
    In React, passing data from a child component to a parent component without using callbacks is typically achieved through a technique called "lifting state up" or using a state management solution like Context API or a global state management library like Redux. Here's how you can achieve this using "lifting state up":
    
    1. **Lifting State Up Approach:**
        
        The idea behind "lifting state up" is to manage the shared state in the parent component, and pass down that state and a function to update that state as props to the child component.
        
        Parent Component (`Parent.js`):
        
        ```jsx
        import React, { useState } from 'react';
        import Child from './Child';
        
        function Parent() {
          const [dataFromChild, setDataFromChild] = useState(null);
        
          const handleDataFromChild = (data) => {
            setDataFromChild(data);
          };
        
          return (
            <div>
              <Child onDataReceived={handleDataFromChild} />
              {dataFromChild && <p>Data from child: {dataFromChild}</p>}
            </div>
          );
        }
        
        export default Parent;
        
        ```
        
        Child Component (`Child.js`):
        
        ```jsx
        import React, { useState } from 'react';
        
        function Child({ onDataReceived }) {
          const [data, setData] = useState('Some data from child');
        
          const sendDataToParent = () => {
            onDataReceived(data);
          };
        
          return (
            <div>
              <button onClick={sendDataToParent}>Send Data to Parent</button>
            </div>
          );
        }
        
        export default Child;
        
        ```
        
        In this example, when the button in the child component is clicked, it triggers `sendDataToParent` which calls the `onDataReceived` function passed down from the parent, effectively passing the data from child to parent.
        
    2. **Context API or Global State Management:**
        
        You can also use Context API or a global state management library like Redux to manage shared state across components without directly passing props.
        
    
    Please note that lifting state up and using callbacks is a common pattern in React to pass data from child to parent, and it's considered a good practice in most cases. If you need to avoid using callbacks altogether, consider exploring other state management solutions like Context API or Redux.
    
5. What is mocking in test in react
    
    Mocking in tests, particularly in the context of React, involves simulating certain parts of the application or system to isolate the code being tested from external dependencies, ensuring that the tests focus on the specific logic or behavior being examined.
    
    In React testing, you might encounter scenarios where you want to isolate components, functions, or API calls to maintain control and predictability during testing. Here are common uses of mocking in React testing:
    
    1. **Component Mocking:**
    Mocking components allows you to simulate the rendering and behavior of child components so that you can test a parent component in isolation. This is often achieved using testing libraries like Jest and tools like `jest.mock`.
    2. **Function Mocking:**
    Mocking functions allows you to simulate the behavior of functions that are being called within the component being tested. This is useful for isolating the logic of a specific function and focusing on its behavior in different scenarios.
    3. **API or Data Mocking:**
    In situations where your components make API calls or fetch data from external sources, mocking is used to simulate these interactions. This ensures that your tests are not dependent on the actual API responses, making the tests faster and more reliable.
    4. **Module Mocking:**
    Module mocking involves replacing entire modules or libraries with mock implementations. This is useful when you want to control the behavior of third-party libraries or modules within your code.
    
    Mocking helps in creating controlled environments for testing and makes tests more predictable, reliable, and faster. By providing mock implementations for external dependencies or components, you can focus on testing the specific behavior or logic of the component being tested.
    
    Here's a simple example of mocking a function using Jest:
    
    ```jsx
    // Example function to be mocked
    function fetchData() {
      return 'Real data';
    }
    
    // Component that uses the fetchData function
    function MyComponent() {
      const data = fetchData();
      return <div>{data}</div>;
    }
    
    // Mocking the fetchData function for the test
    jest.mock('./path/to/fetchData', () => {
      return jest.fn(() => 'Mocked data');
    });
    
    // Test for MyComponent
    test('MyComponent renders with mocked data', () => {
      const { getByText } = render(<MyComponent />);
      expect(getByText('Mocked data')).toBeInTheDocument();
    });
    
    ```
    
    In this example, we mock the `fetchData` function to return 'Mocked data' instead of the actual implementation, allowing us to isolate and test the `MyComponent` with a predictable behavior.
    
6. How do you test that you get exception on particular input in react component?
    
    To test that a specific input in a React component triggers an exception (error, warning, etc.), you can use the testing framework and assertion libraries like Jest and React Testing Library. Here's a step-by-step approach to testing for exceptions in a React component:
    
    1. **Setup Testing Environment:**
    Make sure you have Jest and a testing utility like React Testing Library installed in your project.
    2. **Write the Test:**
    Create a test case that checks for an exception when a particular input is passed to a component.
    3. **Trigger the Exception:**
    In your test, render the component and provide the input that should trigger the exception.
    4. **Expect the Exception:**
    Use assertions to check if an exception occurred or if a specific error message was thrown.
    
    Here's a simple example to demonstrate testing for an exception in a React component:
    
    ```jsx
    // Example component to test
    function MyComponent() {
      function handleInput(input) {
        if (input === 'errorInput') {
          throw new Error('An error occurred');
        }
        return 'Input is okay';
      }
    
      return (
        <div>
          <button onClick={() => handleInput('errorInput')}>Trigger Error</button>
        </div>
      );
    }
    
    // Example test
    test('Exception is thrown for specific input', () => {
      // Render the component
      const { getByText } = render(<MyComponent />);
    
      // Trigger the function that should throw an exception
      const triggerButton = getByText('Trigger Error');
      fireEvent.click(triggerButton);
    
      // Assert that an error was thrown
      expect(() => { getByText('Input is okay'); }).toThrow(Error);
    });
    
    ```
    
    In this example, we're testing that when the button with the text 'Trigger Error' is clicked, an error is thrown. We use `expect(...).toThrow(Error)` to verify that the component throws an error as expected for a specific input.
    
    Adjust the test according to your specific use case, where you want to ensure an exception is thrown for a particular input in your React component.
    
7. Webpack configuration - inputs and outputs
    
    Webpack is a popular module bundler in the JavaScript ecosystem used to bundle and manage dependencies in a web application. Configuring inputs and outputs in Webpack involves specifying the entry points (inputs) and defining the output bundles (outputs) for your application.
    
    Let's go through a basic example of setting up the input and output configurations in a Webpack configuration file (typically named `webpack.config.js`):
    
    1. **Setting up the Webpack Configuration:**
    
    Create a `webpack.config.js` file in the root of your project and require the necessary modules.
    
    ```jsx
    const path = require('path');
    
    module.exports = {
      entry: './src/index.js',  // Entry point (input)
      output: {
        filename: 'bundle.js',   // Output bundle filename
        path: path.resolve(__dirname, 'dist')  // Output directory
      }
    };
    
    ```
    
    In this example:
    
    - `entry` specifies the entry point of your application, typically a JavaScript file where the bundling process starts.
    - `output` defines the output configuration:
        - `filename` specifies the name of the bundled file.
        - `path` defines the output directory where the bundled file will be generated.
    1. **Configuring Input (Entry Point):**
    
    In the `entry` configuration, you define the entry point of your application. This is usually the main JavaScript file that imports and includes other modules.
    
    ```jsx
    module.exports = {
      entry: './src/index.js',  // Entry point (input)
      // ...
    };
    
    ```
    
    In this example, the entry point is `./src/index.js`.
    
    1. **Configuring Output:**
    
    In the `output` configuration, you define how the bundled file is named and where it will be saved.
    
    ```jsx
    module.exports = {
      // ...
      output: {
        filename: 'bundle.js',   // Output bundle filename
        path: path.resolve(__dirname, 'dist')  // Output directory
      }
    };
    
    ```
    
    In this example, the bundled file will be named `bundle.js` and will be saved in the `dist` directory.
    
    1. **Usage:**
    
    To bundle your application using this configuration, run the `webpack` command in your project directory:
    
    ```bash
    webpack --config webpack.config.js
    
    ```
    
    This will use the specified `webpack.config.js` file to bundle your application based on the defined inputs and outputs.
    
    Adjust the entry and output configurations based on your project structure and requirements.
    
8. What is caching
    
    Caching is a technique used in computing to store frequently accessed data in a temporary storage area called a "cache." The purpose of caching is to improve the speed and efficiency of data retrieval and processing by reducing the time it takes to access frequently used or expensive-to-compute data.
    
    Here are the key aspects of caching:
    
    1. **Faster Data Retrieval:**
    Caching allows for quicker access to data by storing a copy of frequently accessed data in a cache. Retrieving data from a cache is typically faster than fetching it from the original source, such as a database or a remote server.
    2. **Reduction in Resource Usage:**
    Caching helps reduce the load on primary data sources or systems by serving data from the cache when possible. This can lead to improved overall system performance and responsiveness.
    3. **Optimized Performance:**
    By caching frequently used data or the results of expensive computations, applications can deliver a more responsive and efficient user experience. This is especially critical for web applications, where latency can significantly impact user satisfaction.
    4. **Cache Invalidation:**
    Caches need to be managed carefully to ensure the data remains consistent and up-to-date. Cache invalidation is the process of updating or removing cached data when the original data changes to maintain accuracy.
    5. **Cache Policies:**
    Various cache policies determine how data is stored, accessed, and evicted from the cache. Common cache policies include Least Recently Used (LRU), First In, First Out (FIFO), and Time to Live (TTL).
    6. **Caching Layers:**
    Applications often have multiple levels of caching, such as in-memory caches, browser caches, CDN (Content Delivery Network) caches, and database query result caches. Each caching layer serves a different purpose and helps optimize data access at various levels of the application stack.
    7. **Cache Keys:**
    Cache keys are used to identify and retrieve data from the cache. Developers use cache keys to uniquely identify data based on parameters, requests, or other relevant attributes.
    
    Caching is widely used in various software systems, including web servers, databases, browsers, content delivery networks, and more. It's an essential technique for achieving faster response times, improving system performance, and enhancing the overall user experience in applications and websites.
    
9. Explain in detail In request lifecycle how and where caching is used
    
    The request lifecycle in web development refers to the stages a request goes through from initiation by the client (e.g., a web browser) to the response being received and displayed. Caching is a critical aspect of this lifecycle that helps optimize performance and reduce server load by storing and serving frequently accessed resources.
    
    Here's a detailed explanation of how and where caching is used within the request lifecycle:
    
    1. **Client-Side Caching:**
        - **Browser Cache:** When a client (e.g., a web browser) makes a request to a web server for a resource (e.g., HTML, CSS, JavaScript, images), the server may include caching directives in the HTTP response headers.
        - **Cache-Control Header:** The `Cache-Control` header provides directives to the browser, specifying how the resource should be cached. For example, the `max-age` directive indicates the maximum time (in seconds) the resource can be cached before it's considered stale.
        - **Expires Header:** The `Expires` header specifies a date/time when the resource becomes invalid and should be re-fetched from the server.
        - **If-Modified-Since and ETag Headers:** These headers enable conditional requests, allowing the server to respond with a `304 Not Modified` status if the resource hasn't changed since the client's last request.
    2. **Server-Side Caching:**
        - **Caching at the Application Level:** Within the server, the application may cache certain responses or data to avoid recalculating or regenerating them for subsequent requests. This is often done using in-memory caches like Redis or Memcached.
        - **Database Query Caching:** Queries to the database can be cached to reduce the load on the database server and improve response times for frequently accessed data.
        - **Full Page Caching:** Entire HTML pages or fragments can be cached to serve identical responses to multiple clients, improving server performance and reducing the need for generating dynamic content for each request.
    3. **CDN (Content Delivery Network) Caching:**
        - **CDN Edge Caches:** CDNs cache static and dynamic content at their edge servers located geographically closer to users. This minimizes the distance between the server and the client, improving content delivery speed.
        - **Cache Invalidation:** CDNs have mechanisms to invalidate or update cached content based on rules or time-to-live settings, ensuring that the cached content remains fresh and up-to-date.
    4. **Proxy Server Caching:**
        - **Proxy Servers:** Intermediate proxy servers between the client and the origin server can cache responses to serve them directly to subsequent requests, reducing the load on the origin server and improving response times for clients.
    
    In summary, caching is used at multiple levels within the request lifecycle, including client-side, server-side, CDN, and proxy server caching. It optimizes performance by reducing the load on servers, minimizing latency, and improving the overall user experience by serving cached content whenever appropriate. Effective cache management, including cache expiration and cache invalidation strategies, ensures that the cached content remains accurate and up-to-date.
    
10. pass data from child to parent without callbacks in react with context and how parent uses it
    
    Passing data from a child component to a parent component in React without using callbacks can be achieved using React Context. Context provides a way to pass data through the component tree without having to pass props manually at every level.
    
    Here's a step-by-step approach to using React Context to pass data from a child to a parent:
    
    1. **Create a Context:**
    Create a context using `React.createContext`.
    
    ```jsx
    import React from 'react';
    
    const MyContext = React.createContext();
    
    export default MyContext;
    
    ```
    
    1. **Wrap Parent Component with Context Provider:**
    Wrap the parent component with the `Provider` from the context, and set the data you want to share as the value.
    
    ```jsx
    import React from 'react';
    import MyContext from './MyContext';
    
    const ParentComponent = () => {
      const sharedData = 'Data from Parent';
    
      return (
        <MyContext.Provider value={sharedData}>
          <ChildComponent />
        </MyContext.Provider>
      );
    };
    
    export default ParentComponent;
    
    ```
    
    1. **Access Context in Child Component:**
    In the child component, use `useContext` hook to access the context and retrieve the shared data.
    
    ```jsx
    import React, { useContext } from 'react';
    import MyContext from './MyContext';
    
    const ChildComponent = () => {
      const sharedData = useContext(MyContext);
    
      return <div>{sharedData}</div>;
    };
    
    export default ChildComponent;
    
    ```
    
    Now, the `ChildComponent` has access to the data shared via the context without needing to pass it through props directly.
    
    1. **Parent Consuming the Data:**
    The parent component (`ParentComponent`) doesn't need to do anything specific to consume the data. The data passed through the context will be available to any child component wrapped in the `Provider`.
    
    By utilizing React Context in this manner, you can efficiently share data between components, including passing data from child to parent without relying on callbacks.
