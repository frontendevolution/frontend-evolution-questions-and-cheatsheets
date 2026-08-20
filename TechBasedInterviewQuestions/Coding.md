---
title: "Coding Practice Questions"
topic: "FE"
format: "Tech Based Interview Questions"
framework: "FE"
difficulty: "Beginner-Senior"
description: ""
companies: []
publishedAt: "2026-07-31"
---


- **sum(2)(3)(4)(5)....(n)**
    
    You can achieve this functionality by creating a chain of curried functions that accumulate the values as they are passed in. Here's an example implementation:
    
    ```jsx
    function sum(value) {
        function addNext(nextValue) {
            return sum(value + nextValue);
        }
    
        addNext.valueOf = function() {
            return value;
        };
    
        return addNext;
    }
    
    console.log(sum(2)(3)(4)(5).valueOf()); // Outputs: 14
    
    ```
    
    In this implementation:
    
    1. The `sum` function takes an initial `value` as an argument and returns the `addNext` function.
    2. The `addNext` function is returned and takes the next value (`nextValue`) to be added to the accumulated total. It returns another curried `sum` function.
    3. This pattern continues, creating a chain of curried functions, each accumulating the total value.
    
    The `valueOf` method is used to extract the final value from the curried chain.
    
    Keep in mind that this example demonstrates the concept, but it might not be the most efficient or readable way to achieve the desired result. It involves some JavaScript magic and might not be intuitive for other developers reading your code. In real-world scenarios, consider using more straightforward approaches to achieve similar functionality, such as using regular functions or a loop.
    
- **Explain in detail how to check if password entered is valid or not**
    
    Validating passwords involves checking whether a password meets certain criteria, such as length, complexity, and security. Here's a step-by-step guide on how to check if a password is valid using JavaScript:
    
    1. **Define Validation Criteria:**
    Before you start, define the criteria that a valid password should meet. Common criteria include:
        - Minimum and maximum length
        - At least one uppercase letter
        - At least one lowercase letter
        - At least one digit
        - Special characters (optional)
        
        Modify the criteria based on your specific requirements and security considerations.
        
    2. **Use Regular Expressions:**
    Regular expressions are useful for pattern matching in strings. You can create a regex pattern that checks if the password meets the defined criteria.
    3. **Regex Pattern for Password Validation:**
    Here's an example regex pattern that checks for a password containing at least one uppercase letter, one lowercase letter, one digit, and is between 8 and 20 characters long:
        
        ```jsx
        const passwordPattern = /^(?=.*[a-z])(?=.*[A-Z])(?=.*\d).{8,20}$/;
        
        ```
        
    4. **Perform Validation:**
    Use the `.test()` method of the regex pattern to check if the entered password matches the pattern:
        
        ```jsx
        function isValidPassword(password) {
            const passwordPattern = /^(?=.*[a-z])(?=.*[A-Z])(?=.*\d).{8,20}$/;
            return passwordPattern.test(password);
        }
        
        const userPassword = "Secure123";
        if (isValidPassword(userPassword)) {
            console.log("Password is valid.");
        } else {
            console.log("Password is not valid.");
        }
        
        ```
        
    5. **Password Strength:**
    Depending on your application's security requirements, you might want to implement password strength checks, such as measuring entropy or utilizing libraries that provide more advanced password validation rules.
    6. **Use HTML5 Input Type:**
    For basic password validation, HTML5 provides the `type="password"` attribute on the `<input>` element, which can help users visualize the entered password.
    
    ```html
    <input type="password" id="passwordInput" />
    <button onclick="validatePassword()">Check Password</button>
    
    <script>
    function isValidPassword(password) {
        const passwordPattern = /^(?=.*[a-z])(?=.*[A-Z])(?=.*\d).{8,20}$/;
        return passwordPattern.test(password);
    }
    
    function validatePassword() {
        const passwordInput = document.getElementById("passwordInput").value;
        if (isValidPassword(passwordInput)) {
            console.log("Password is valid.");
        } else {
            console.log("Password is not valid.");
        }
    }
    </script>
    
    ```
    
    Remember that password validation on the client side is just a first step. Server-side validation is crucial to ensure that passwords meet security requirements before storing them in a database or using them for authentication.
    
- **Explain in detail how to check if email entered is valid or not**
    
    Validating an email address is a common task in web development to ensure that the entered email follows a proper format. While no validation can guarantee that an email address is valid for sure, you can use regular expressions to perform a basic check on the format of the email. Here's a step-by-step guide on how to check if an email address is valid using JavaScript:
    
    1. **Use Regular Expressions:**
    Regular expressions (regex) are patterns that describe sets of characters. They are commonly used for text validation tasks. For email validation, you can use a regex pattern that matches the expected format of an email address.
    2. **Regex Pattern for Basic Email Validation:**
    Here's a basic regex pattern that can be used to check if an email address has a valid format:
        
        ```jsx
        const emailPattern = /^[a-zA-Z0-9._-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,4}$/;
        
        ```
        
    3. **Perform Validation:**
    You can use the `.test()` method of the regex pattern to check if the entered email matches the pattern:
        
        ```jsx
        function isValidEmail(email) {
            const emailPattern = /^[a-zA-Z0-9._-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,4}$/;
            return emailPattern.test(email);
        }
        
        const userEmail = "example@example.com";
        if (isValidEmail(userEmail)) {
            console.log("Email is valid.");
        } else {
            console.log("Email is not valid.");
        }
        
        ```
        
    4. **Enhanced Email Validation:**
    The provided regex is a basic example and may not catch all possible valid email addresses. Email validation can get quite complex due to the wide range of valid formats and internationalization. There are more comprehensive regex patterns available, or you might consider using libraries or built-in browser methods for more accurate validation.
    5. **Use HTML5 Input Type:**
    In HTML5, you can use the `type="email"` attribute on the `<input>` element to enable browser-based email validation. However, keep in mind that browser-based validation might not cover all edge cases.
    
    ```html
    <input type="email" id="emailInput" />
    <button onclick="validateEmail()">Check Email</button>
    
    <script>
    function isValidEmail(email) {
        const emailPattern = /^[a-zA-Z0-9._-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,4}$/;
        return emailPattern.test(email);
    }
    
    function validateEmail() {
        const emailInput = document.getElementById("emailInput").value;
        if (isValidEmail(emailInput)) {
            console.log("Email is valid.");
        } else {
            console.log("Email is not valid.");
        }
    }
    </script>
    
    ```
    
    Remember that email validation is just one part of ensuring data quality and security. It's important to consider server-side validation as well to prevent malicious or incorrect data from being submitted to your application.
    
- **How to have responsive media**
    
    Creating responsive media, such as images and videos, ensures that they adapt and display appropriately on various screen sizes and devices, providing a better user experience. Responsive media helps prevent content from appearing too small or too large on different devices. Here are some techniques to achieve responsive media:
    
    1. **Use CSS for Images:**
    Set the `max-width` property of images to ensure they don't exceed the width of their container. This prevents images from overflowing and maintains their aspect ratio.
        
        ```css
        img {
          max-width: 100%;
          height: auto;
        }
        
        ```
        
    2. **Use the `<picture>` Element:**
    The `<picture>` element allows you to provide multiple versions of an image and select the appropriate one based on screen size or other conditions. This is particularly useful when serving different image sizes for different devices.
        
        ```html
        <picture>
          <source media="(min-width: 1200px)" srcset="large-image.jpg">
          <source media="(min-width: 768px)" srcset="medium-image.jpg">
          <img src="small-image.jpg" alt="Responsive Image">
        </picture>
        
        ```
        
    3. **Responsive Videos:**
    For videos, use the HTML5 `<video>` element. Set the `max-width` property for the video container and ensure the video's aspect ratio is maintained. This prevents videos from overflowing their containers and maintains their proportions.
        
        ```css
        .video-container {
          max-width: 100%;
          position: relative;
          padding-bottom: 56.25%; /* 16:9 aspect ratio */
        }
        
        video {
          position: absolute;
          width: 100%;
          height: 100%;
        }
        
        ```
        
    4. **Media Queries:**
    Use CSS media queries to apply different styles based on the screen size or device characteristics. This allows you to customize the layout and appearance of media for various devices.
        
        ```css
        @media (max-width: 768px) {
          /* Styles for small screens */
        }
        
        @media (min-width: 769px) and (max-width: 1200px) {
          /* Styles for medium screens */
        }
        
        @media (min-width: 1201px) {
          /* Styles for large screens */
        }
        
        ```
        
    5. **Viewport Meta Tag:**
    Add the viewport meta tag in the `<head>` section of your HTML to ensure proper scaling and responsiveness on mobile devices.
        
        ```html
        <meta name="viewport" content="width=device-width, initial-scale=1">
        
        ```
        
    
    By applying these techniques, you can ensure that your media elements, such as images and videos, adapt seamlessly to various screen sizes and devices, providing a better viewing experience for users across different platforms.
    
- **How to centre a div in screen**
    
    To center a `<div>` element both vertically and horizontally on the screen, you can use CSS along with positioning properties. There are different methods you can use, depending on your specific requirements. Here are a couple of common approaches:
    
    1. **Flexbox Method:**
    
    Using Flexbox is a popular and straightforward way to center elements both vertically and horizontally.
    
    HTML:
    
    ```html
    <div class="centered-div">
      <!-- Your content here -->
    </div>
    
    ```
    
    CSS:
    
    ```css
    .centered-div {
      display: flex;
      justify-content: center; /* Horizontal centering */
      align-items: center; /* Vertical centering */
      height: 100vh; /* Full viewport height */
    }
    
    ```
    
    In this approach, the `display: flex` on the container (`centered-div`) creates a flex container, and `justify-content: center` and `align-items: center` center the content both horizontally and vertically.
    
    1. **Position and Transform Method:**
    
    Another approach is to use positioning and the `transform` property.
    
    HTML:
    
    ```html
    <div class="centered-div">
      <!-- Your content here -->
    </div>
    
    ```
    
    CSS:
    
    ```css
    .centered-div {
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
    }
    
    ```
    
    In this method, `position: absolute` takes the element out of the normal document flow. Then, `top: 50%` and `left: 50%` position the element at the center of the viewport. Finally, `transform: translate(-50%, -50%)` shifts the element's position by half of its width and height to accurately center it.
    
    Choose the method that best fits your layout and styling requirements. Both methods are effective in centering a `<div>` element on the screen.
    
- **How to set row and col direction in flexbox**
    
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
    
- **Explain in detail how to make timer component that auto decreases by 1 every 1 second**
    
    Certainly! Here's how you can create a timer component in React that auto-decreases by 1 every second using the `useState` and `useEffect` hooks:
    
    ```jsx
    import React, { useState, useEffect } from 'react';
    
    function TimerComponent() {
      const [seconds, setSeconds] = useState(60); // Initial time in seconds
    
      useEffect(() => {
        // Create an interval that runs every 1 second
        const intervalId = setInterval(() => {
          // Decrement the seconds
          setSeconds(prevSeconds => prevSeconds - 1);
        }, 1000);
    
        // Cleanup: Clear the interval when the component unmounts
        return () => {
          clearInterval(intervalId);
        };
      }, []); // Empty dependency array, effect only runs once after mount
    
      return (
        <div>
          <h1>Countdown Timer</h1>
          <p>{seconds} seconds</p>
        </div>
      );
    }
    
    export default TimerComponent;
    
    ```
    
    In this example, the `TimerComponent` starts with an initial value of 60 seconds. The `useEffect` hook is used to create an interval that decrements the `seconds` state by 1 every 1000 milliseconds (1 second). The interval runs continuously until the component is unmounted, at which point the cleanup function provided in `useEffect` clears the interval.
    
    The component renders the remaining `seconds` value in the UI, creating a simple countdown timer that auto-decreases by 1 every second.
    
    Remember to import and use the necessary React hooks (`useState` and `useEffect`) at the beginning of your file. You can customize the initial time and the rendering format as needed for your use case.
    
- **Obj=[{name:'a', active: true,children:[{name:'a1', active: true,children:[{name:'a11', active: true,children:[]},{name:'a12', active: false,children:[]}]},
{name:'a2', active: true,children:[]}
]},
{name:'b', active: true,children:[{name:'b1', active: false,children:[{name:'b11', active: true,children:[]}]}]}
]
Iterate over array of objects and return object with elements with active true only, only if parent key has active true without passing extra argument in function**
    
    To achieve this, you can create a function that recursively iterates over the array of objects and filters out elements with `active: true` only if their parent has `active: true`. Here's a JavaScript function that accomplishes this:
    
    ```jsx
    function filterActive(objArray, parentActive = true) {
      return objArray.reduce((acc, obj) => {
        if (obj.active === true && parentActive) {
          const children = obj.children.length ? filterActive(obj.children, obj.active) : [];
          acc.push({ ...obj, children });
        }
        return acc;
      }, []);
    }
    
    const filteredArray = filterActive(obj);
    console.log(filteredArray);
    
    ```
    
    Replace `obj` with your provided array of objects. The `filterActive` function uses recursion to filter out objects with `active: true` and their children accordingly.
    
- **Sort out the frequency of occurrence of each element in an array and print the output in array in javascript**
    
    To sort out the frequency of occurrence of each element in an array and print the output in an array in JavaScript, you can follow these steps:
    
    1. Create an object to store the frequency of each element in the array.
    2. Loop through the input array and count the occurrences of each element using the object.
    3. Create an array of unique elements from the input array.
    4. Sort the unique elements array based on their frequency count.
    5. Finally, construct the output array with each element and its corresponding frequency count.
    
    Here's a code example to achieve this:
    
    ```jsx
    function sortByFrequency(inputArray) {
      // Step 1: Create an object to store the frequency of each element
      const frequencyObj = {};
    
      // Step 2: Loop through the input array and count occurrences
      inputArray.forEach((element) => {
        frequencyObj[element] = (frequencyObj[element] || 0) + 1;
      });
    
      // Step 3: Create an array of unique elements from the input array
      const uniqueElements = Array.from(new Set(inputArray));
    
      // Step 4: Sort the unique elements array based on their frequency count
      uniqueElements.sort((a, b) => frequencyObj[b] - frequencyObj[a]);
    
      // Step 5: Construct the output array with each element and its frequency count
      const outputArray = uniqueElements.map((element) => ({
        element,
        frequency: frequencyObj[element],
      }));
    
      return outputArray;
    }
    
    // Test the function
    const inputArray = [1, 2, 1, 3, 4, 2, 3, 4, 4, 5];
    const resultArray = sortByFrequency(inputArray);
    console.log(resultArray);
    
    ```
    
    This code will output:
    
    ```
    [
      { element: 4, frequency: 3 },
      { element: 2, frequency: 2 },
      { element: 1, frequency: 2 },
      { element: 3, frequency: 2 },
      { element: 5, frequency: 1 }
    ]
    
    ```
    
    The output array contains each element in the input array along with its frequency count, sorted in descending order based on the frequency.
    
- **Check if string is palindrome**
    
    To check if a string is a palindrome in JavaScript, you can follow these steps:
    
    1. Remove non-alphanumeric characters and convert the string to lowercase for accurate palindrome comparison.
    2. Compare characters from the beginning and the end of the string, moving towards the center, to check if they match.
    
    Here's a code example to achieve this:
    
    ```jsx
    function isPalindrome(str) {
      // Step 1: Remove non-alphanumeric characters and convert to lowercase
      const cleanStr = str.replace(/[^a-zA-Z0-9]/g, '').toLowerCase();
    
      // Step 2: Compare characters to check if it's a palindrome
      for (let i = 0; i < Math.floor(cleanStr.length / 2); i++) {
        if (cleanStr[i] !== cleanStr[cleanStr.length - 1 - i]) {
          return false;
        }
      }
      return true;
    }
    
    // Test the function
    const testString1 = "racecar";
    console.log(isPalindrome(testString1)); // Output: true
    
    const testString2 = "hello";
    console.log(isPalindrome(testString2)); // Output: false
    
    ```
    
    In the above code, the `isPalindrome` function takes a string as input, removes non-alphanumeric characters, converts it to lowercase, and then compares characters from the beginning and end of the cleaned string. If any characters don't match, the function returns `false`, indicating that the string is not a palindrome. If all characters match, it returns `true`, indicating that the string is a palindrome.
    
- **Convert array to object**
    
    To convert an array to an object in JavaScript, you can use various methods depending on your specific requirements. Here are a few approaches you can take:
    
    1. **Using a For Loop:**
    You can iterate through the array and manually create key-value pairs in the object.
    
    ```jsx
    function arrayToObject(array) {
      const result = {};
      for (let i = 0; i < array.length; i++) {
        result[i] = array[i];
      }
      return result;
    }
    
    const myArray = ['a', 'b', 'c'];
    const myObject = arrayToObject(myArray);
    console.log(myObject);
    
    ```
    
    1. **Using the `reduce()` Method:**
    The `reduce()` method is another way to convert an array to an object.
    
    ```jsx
    function arrayToObject(array) {
      return array.reduce((acc, currentValue, index) => {
        acc[index] = currentValue;
        return acc;
      }, {});
    }
    
    const myArray = ['a', 'b', 'c'];
    const myObject = arrayToObject(myArray);
    console.log(myObject);
    
    ```
    
    1. **Using the `Object.fromEntries()` Method (Modern Approach):**
    This method creates an object from an array of key-value pairs.
    
    ```jsx
    function arrayToObject(array) {
      const entries = array.map((value, index) => [index, value]);
      return Object.fromEntries(entries);
    }
    
    const myArray = ['a', 'b', 'c'];
    const myObject = arrayToObject(myArray);
    console.log(myObject);
    
    ```
    
    Each of these approaches will convert your array into an object with numeric indices as keys and corresponding array values as values. If you have a specific requirement for using non-numeric keys, you can modify the approaches accordingly.
    
- **clone object**
    
    To clone an object in JavaScript, you can use various methods. However, it's important to note that objects can have nested structures, and different cloning methods handle nested objects differently. Here are a few common approaches to clone an object:
    
    1. **Using the Spread Operator (`{...}`):**
    The spread operator can be used to create a shallow copy of an object.
    
    ```jsx
    const originalObj = { a: 1, b: 2, c: 3 };
    const clonedObj = { ...originalObj };
    console.log(clonedObj);
    
    ```
    
    This creates a shallow copy, meaning that if the original object contains nested objects, they will still be referenced in the cloned object.
    
    1. **Using `Object.assign()`:**
    Similar to the spread operator, `Object.assign()` can also be used to create a shallow copy of an object.
    
    ```jsx
    const originalObj = { a: 1, b: 2, c: 3 };
    const clonedObj = Object.assign({}, originalObj);
    console.log(clonedObj);
    
    ```
    
    1. **Using the `JSON.parse()` and `JSON.stringify()` Method:**
    This method creates a deep copy of the object, but it has limitations. It won't work if the object contains functions, symbols, or circular references.
    
    ```jsx
    const originalObj = { a: 1, b: { x: 2, y: 3 }, c: 4 };
    const clonedObj = JSON.parse(JSON.stringify(originalObj));
    console.log(clonedObj);
    
    ```
    
    1. **Using a Third-Party Library (e.g., Lodash):**
    Lodash provides a `cloneDeep()` function that creates a deep copy of an object, handling nested structures and circular references.
    
    ```jsx
    const _ = require('lodash');
    const originalObj = { a: 1, b: { x: 2, y: 3 }, c: 4 };
    const clonedObj = _.cloneDeep(originalObj);
    console.log(clonedObj);
    
    ```
    
    1. **Using `Object.create()`:**
    This method creates a new object with the specified prototype object and properties. It's a way to create an empty object with the same prototype as the original object.
    
    ```jsx
    const originalObj = { a: 1, b: 2, c: 3 };
    const clonedObj = Object.create(Object.getPrototypeOf(originalObj), Object.getOwnPropertyDescriptors(originalObj));
    console.log(clonedObj);
    
    ```
    
    Keep in mind that while these methods will create clones of the object, they may have different behaviors when it comes to handling nested objects, prototypes, and other advanced features. Choose the method that best suits your specific use case.
    
- **Retrieve only numbers which are repeated in an array in js**
    
    To retrieve only numbers that are repeated in a JavaScript array, you can use the following code:
    
    ```jsx
    function findRepeatedNumbers(arr) {
      const numCount = {};
      const repeatedNumbers = [];
    
      // Count occurrences of each number
      arr.forEach(num => {
        numCount[num] = (numCount[num] || 0) + 1;
      });
    
      // Identify repeated numbers
      for (const num in numCount) {
        if (numCount[num] > 1) {
          repeatedNumbers.push(parseInt(num));
        }
      }
    
      return repeatedNumbers;
    }
    
    const numbers = [1, 2, 3, 2, 4, 3, 5, 6, 4];
    const repeatedNumbers = findRepeatedNumbers(numbers);
    console.log('Repeated numbers:', repeatedNumbers);  // Output: [2, 3, 4]
    
    ```
    
    The `findRepeatedNumbers` function takes an array as input and returns an array containing the numbers that are repeated in the original array. In this example, `[2, 3, 4]` are the numbers that are repeated in the given array.
    
- **Write code to Change c# variable names like this_variable_name to Java variable names like thisVariableName and vice versa in javascript**
    
    To convert variable names between the snake_case style used in C# (e.g., `this_variable_name`) and the camelCase style used in Java (e.g., `thisVariableName`) in JavaScript, you can create two functions for each conversion.
    
    1. Converting snake_case (C#) to camelCase (Java):
    
    ```jsx
    function snakeToCamel(input) {
      return input.replace(/_(.)/g, (_, char) => char.toUpperCase());
    }
    
    const cSharpVariableName = 'this_variable_name';
    const javaVariableName = snakeToCamel(cSharpVariableName);
    console.log('Java variable name:', javaVariableName);  // Output: thisVariableName
    
    ```
    
    1. Converting camelCase (Java) to snake_case (C#):
    
    ```jsx
    function camelToSnake(input) {
      return input.replace(/[A-Z]/g, char => `_${char.toLowerCase()}`);
    }
    
    const javaVariableName = 'thisVariableName';
    const cSharpVariableName = camelToSnake(javaVariableName);
    console.log('C# variable name:', cSharpVariableName);  // Output: this_variable_name
    
    ```
    
    These functions use regular expressions to perform the respective conversions. The `snakeToCamel` function converts snake_case (C#) to camelCase (Java), and the `camelToSnake` function converts camelCase (Java) to snake_case (C#).
