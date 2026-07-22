Here’s a **deeper dive** into all topics with expanded explanations and insights to help you fully understand and articulate answers during your interview.

---

## **1. Core Concepts**

### **JavaScript & TypeScript**

1. **What are closures, and why are they important?**
    
    **A:**
    
    - A closure is a function that retains access to its lexical scope, even when the function is executed outside that scope.
    - **Example:**
        
        ```jsx
        function outerFunction() {
          let count = 0;
          return function innerFunction() {
            count++;
            console.log(count);
          };
        }
        const counter = outerFunction();
        counter(); // Output: 1
        counter(); // Output: 2
        
        ```
        
    - **Importance:** Closures are useful for data encapsulation, creating private variables, and building factories or event handlers.
2. **How does TypeScript improve code reliability?**
    
    **A:**
    
    - Ensures **type safety** by catching errors during compile time instead of runtime.
    - Provides **type inference** for cleaner code.
    - Offers **structural typing**, allowing compatibility checks between types with the same shape.
    - **Example:** TypeScript catches this error:
        
        ```tsx
        function greet(name: string) {
          console.log("Hello, " + name.toUpperCase());
        }
        greet(42); // Error: Argument of type 'number' is not assignable to 'string'
        
        ```
        
3. **What is the difference between shallow and deep copying in JavaScript?**
    
    **A:**
    
    - **Shallow copy:** Copies only the first level of an object. Changes to nested objects affect the copy.
        
        ```jsx
        const obj = { a: 1, b: { c: 2 } };
        const shallowCopy = { ...obj };
        shallowCopy.b.c = 42;
        console.log(obj.b.c); // Output: 42
        
        ```
        
    - **Deep copy:** Creates a new copy of all nested objects.
        
        ```jsx
        const obj = { a: 1, b: { c: 2 } };
        const deepCopy = JSON.parse(JSON.stringify(obj));
        deepCopy.b.c = 42;
        console.log(obj.b.c); // Output: 2
        
        ```
        

---

### **React**

1. **What is the difference between controlled and uncontrolled components?**
    
    **A:**
    
    - **Controlled components:** Managed by React state. You use `useState` or similar hooks to control input values.
        
        ```jsx
        function ControlledComponent() {
          const [value, setValue] = React.useState("");
          return <input value={value} onChange={(e) => setValue(e.target.value)} />;
        }
        
        ```
        
    - **Uncontrolled components:** Managed by the DOM using `ref`.
        
        ```jsx
        function UncontrolledComponent() {
          const inputRef = React.useRef(null);
          const handleSubmit = () => console.log(inputRef.current.value);
          return <input ref={inputRef} />;
        }
        
        ```
        
2. **Explain the Context API and its use cases.**
    
    **A:**
    
    - The Context API provides a way to share values like theme or authentication across components without explicitly passing props.
    - **Example:**
        
        ```jsx
        const ThemeContext = React.createContext("light");
        function App() {
          return (
            <ThemeContext.Provider value="dark">
              <Toolbar />
            </ThemeContext.Provider>
          );
        }
        function Toolbar() {
          const theme = React.useContext(ThemeContext);
          return <div>{`Theme: ${theme}`}</div>;
        }
        
        ```
        
3. **How do React hooks replace class components?**
    
    **A:**
    
    - Hooks like `useState` and `useEffect` enable state management and lifecycle methods in functional components.
    - **Benefits:** Simplifies code, avoids boilerplate, and supports better composition.

---

### **Redux**

1. **What are common issues in Redux, and how do you solve them?**
    
    **A:**
    
    - **Issue:** Too many reducers.**Solution:** Combine reducers or modularize the store.
    - **Issue:** State mutation.**Solution:** Use `Immer` or tools like Redux Toolkit to ensure immutability.
    - **Issue:** Verbosity in action creation.**Solution:** Use action creators and middleware.
2. **How does Redux Toolkit simplify Redux?**
    
    **A:**
    
    - Provides utilities for managing slices, actions, and reducers.
    - Includes middleware like `redux-thunk` by default.
    - Simplifies boilerplate code with functions like `createSlice`.

---

## **2. Frameworks & Libraries**

### **Next.js**

1. **How do you implement authentication in Next.js?**
    
    **A:**
    
    - **Approach 1:** Use server-side authentication with middleware or API routes.
    - **Approach 2:** Use a library like `next-auth`.
        
        ```jsx
        import { useSession, signIn, signOut } from "next-auth/react";
        export default function Component() {
          const { data: session } = useSession();
          return session ? (
            <div>
              <p>Signed in as {session.user.email}</p>
              <button onClick={() => signOut()}>Sign out</button>
            </div>
          ) : (
            <button onClick={() => signIn()}>Sign in</button>
          );
        }
        
        ```
        
2. **What is Incremental Static Regeneration (ISR)?**
    
    **A:**
    
    - ISR allows static pages to be updated by re-rendering on the server after a set interval.
    - **Example:**
        
        ```jsx
        export async function getStaticProps() {
          const data = await fetchData();
          return {
            props: { data },
            revalidate: 10, // Regenerate every 10 seconds
          };
        }
        
        ```
        

---

### **CSS Frameworks**

1. **What are the differences between MUI, Bootstrap, and Tailwind?**
    
    **A:**
    
    - **MUI:** Component library for React with pre-built, customizable components (e.g., buttons, dialogs).
    - **Bootstrap:** Classic CSS framework for grids, responsive design, and UI components.
    - **Tailwind:** Utility-first CSS framework for custom designs using class-based styling.
2. **How do you theme an application using Tailwind?**
    
    **A:**
    
    - Modify the `tailwind.config.js` file to add custom colors, spacing, and typography.
        
        ```jsx
        module.exports = {
          theme: {
            extend: {
              colors: {
                customBlue: "#1E40AF",
              },
            },
          },
        };
        
        ```
        

---

## **3. Behavioral Questions**

1. **How do you handle conflicts in a team?**
    
    **A:**
    
    - Listen actively to all perspectives.
    - Use data or prototypes to validate ideas.
    - Suggest a compromise or escalate if necessary.
2. **Can you describe a challenging project and how you managed it?**
    
    **A:** Use the STAR framework:
    
    - **Situation:** Briefly describe the challenge.
    - **Task:** Explain your role.
    - **Action:** Describe the steps you took.
    - **Result:** Highlight the positive outcome.

---

### **JavaScript & TypeScript**

1. **Event Emitter**
Implement a simple event emitter class.

```tsx
class EventEmitter {
  private events: Record<string, Function[]> = {};

  on(event: string, listener: Function) {
    if (!this.events[event]) {
      this.events[event] = [];
    }
    this.events[event].push(listener);
  }

  emit(event: string, ...args: any[]) {
    if (this.events[event]) {
      this.events[event].forEach(listener => listener(...args));
    }
  }

  off(event: string, listener: Function) {
    if (this.events[event]) {
      this.events[event] = this.events[event].filter(l => l !== listener);
    }
  }
}

// Usage
const emitter = new EventEmitter();
const log = (msg: string) => console.log(msg);
emitter.on("event", log);
emitter.emit("event", "Hello, World!"); // Output: Hello, World!
emitter.off("event", log);

```

1. **Throttle Function**
Write a throttle function that limits the frequency of a callback execution.

```tsx
function throttle<T extends (...args: any[]) => void>(func: T, limit: number): (...args: Parameters<T>) => void {
  let lastCall = 0;
  return function (...args: Parameters<T>) {
    const now = Date.now();
    if (now - lastCall >= limit) {
      lastCall = now;
      func(...args);
    }
  };
}

// Usage
const throttledLog = throttle((msg: string) => console.log(msg), 2000);
throttledLog("Hello"); // Logs immediately
throttledLog("World"); // Ignored if within 2 seconds

```

---

### **React**

1. **Custom Hook: Fetch Data**
Create a custom hook to fetch data with error handling and loading states.

```tsx
import { useState, useEffect } from "react";

function useFetch<T>(url: string) {
  const [data, setData] = useState<T | null>(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState<string | null>(null);

  useEffect(() => {
    fetch(url)
      .then(response => {
        if (!response.ok) throw new Error("Network response was not ok");
        return response.json();
      })
      .then(setData)
      .catch(err => setError(err.message))
      .finally(() => setLoading(false));
  }, [url]);

  return { data, loading, error };
}

// Usage
export default function App() {
  const { data, loading, error } = useFetch<{ id: number; title: string }[]>("https://jsonplaceholder.typicode.com/posts");

  if (loading) return <p>Loading...</p>;
  if (error) return <p>Error: {error}</p>;

  return (
    <ul>
      {data?.map(post => (
        <li key={post.id}>{post.title}</li>
      ))}
    </ul>
  );
}

```

1. **Higher-Order Component (HOC)**
Create an HOC that logs props of a wrapped component.

```tsx
import React from "react";

function withLogger<P>(WrappedComponent: React.ComponentType<P>) {
  return (props: P) => {
    console.log("Props:", props);
    return <WrappedComponent {...props} />;
  };
}

// Usage
function HelloWorld({ message }: { message: string }) {
  return <h1>{message}</h1>;
}

const HelloWorldWithLogger = withLogger(HelloWorld);
export default function App() {
  return <HelloWorldWithLogger message="Hello, World!" />;
}

```

---

### **Redux**

1. **Async Redux with Redux Toolkit**
Set up Redux Toolkit to manage a counter that can increment, decrement, and fetch a random number from an API.

```tsx
import { configureStore, createSlice, createAsyncThunk } from "@reduxjs/toolkit";
import { Provider, useDispatch, useSelector } from "react-redux";

// Async thunk to fetch random number
const fetchRandom = createAsyncThunk("counter/fetchRandom", async () => {
  const res = await fetch("https://randomuser.me/api/");
  const data = await res.json();
  return data.info.seed.length; // Example random data
});

// Slice
const counterSlice = createSlice({
  name: "counter",
  initialState: { value: 0 },
  reducers: {
    increment: state => { state.value += 1; },
    decrement: state => { state.value -= 1; }
  },
  extraReducers: builder => {
    builder.addCase(fetchRandom.fulfilled, (state, action) => {
      state.value = action.payload;
    });
  }
});

// Store
const store = configureStore({ reducer: counterSlice.reducer });
const { increment, decrement } = counterSlice.actions;

// App Component
function Counter() {
  const dispatch = useDispatch();
  const value = useSelector((state: any) => state.value);

  return (
    <div>
      <h1>{value}</h1>
      <button onClick={() => dispatch(increment())}>Increment</button>
      <button onClick={() => dispatch(decrement())}>Decrement</button>
      <button onClick={() => dispatch(fetchRandom())}>Fetch Random</button>
    </div>
  );
}

export default function App() {
  return (
    <Provider store={store}>
      <Counter />
    </Provider>
  );
}

```

---

### **CSS Frameworks**

1. **Accordion Component with Tailwind CSS**
Create an accordion component using Tailwind.

```tsx
import { useState } from "react";

function Accordion({ title, children }: { title: string; children: React.ReactNode }) {
  const [isOpen, setIsOpen] = useState(false);
  return (
    <div className="border-b">
      <button
        className="w-full text-left p-4 bg-gray-100 hover:bg-gray-200"
        onClick={() => setIsOpen(!isOpen)}
      >
        {title}
      </button>
      {isOpen && <div className="p-4">{children}</div>}
    </div>
  );
}

// Usage
export default function App() {
  return (
    <div className="max-w-md mx-auto">
      <Accordion title="Section 1">Content for section 1</Accordion>
      <Accordion title="Section 2">Content for section 2</Accordion>
    </div>
  );
}

```

1. **Responsive Grid with Tailwind CSS**
Create a responsive image gallery.

```tsx
export default function Gallery() {
  return (
    <div className="grid grid-cols-2 sm:grid-cols-3 lg:grid-cols-4 gap-4 p-4">
      {[...Array(12).keys()].map(i => (
        <div key={i} className="bg-gray-200 h-32 flex items-center justify-center">
          {i + 1}
        </div>
      ))}
    </div>
  );
}

```

---

### **Next.js Advanced**

1. **Middleware for Authentication**
Create middleware to restrict access to certain pages.

```tsx
import { NextResponse } from "next/server";

export function middleware(req: Request) {
  const token = req.cookies.get("token");
  if (!token) {
    return NextResponse.redirect(new URL("/login", req.url));
  }
  return NextResponse.next();
}

// Usage: Apply this middleware to pages that require authentication.

```

1. **Image Optimization**
Use Next.js `Image` component to optimize images dynamically.

```tsx
import Image from "next/image";

export default function App() {
  return (
    <div>
      <Image
        src="/example.jpg"
        alt="Optimized Example"
        width={800}
        height={600}
        placeholder="blur"
      />
    </div>
  );
}

```

---

### **JavaScript & TypeScript**

### **Array and String Manipulations**

1. **Anagram Check**
Write a function to determine if two strings are anagrams of each other.

```tsx
function isAnagram(s1: string, s2: string): boolean {
  return s1.split("").sort().join("") === s2.split("").sort().join("");
}

```

1. **Merge Intervals**
Merge overlapping intervals from an array of intervals.

```tsx
function mergeIntervals(intervals: [number, number][]): [number, number][] {
  intervals.sort((a, b) => a[0] - b[0]);
  const merged: [number, number][] = [];
  for (let i = 0; i < intervals.length; i++) {
    if (!merged.length || merged[merged.length - 1][1] < intervals[i][0]) {
      merged.push(intervals[i]);
    } else {
      merged[merged.length - 1][1] = Math.max(merged[merged.length - 1][1], intervals[i][1]);
    }
  }
  return merged;
}

```

### **Algorithmic Problems**

1. **Binary Search**
Implement binary search for a sorted array.

```tsx
function binarySearch(arr: number[], target: number): number {
  let left = 0, right = arr.length - 1;
  while (left <= right) {
    const mid = Math.floor((left + right) / 2);
    if (arr[mid] === target) return mid;
    else if (arr[mid] < target) left = mid + 1;
    else right = mid - 1;
  }
  return -1;
}

```

1. **Fibonacci Sequence**
Write a function to generate the first `n` Fibonacci numbers using recursion and memoization.

```tsx
function fibonacci(n: number, memo: Record<number, number> = {}): number {
  if (n <= 1) return n;
  if (memo[n]) return memo[n];
  memo[n] = fibonacci(n - 1, memo) + fibonacci(n - 2, memo);
  return memo[n];
}

```

---

### **React**

### **Components and State Management**

1. **Theme Switcher**
Build a theme switcher (light/dark mode) using React Context.

```tsx
import React, { createContext, useContext, useState } from "react";

const ThemeContext = createContext({ theme: "light", toggleTheme: () => {} });

export function ThemeProvider({ children }: { children: React.ReactNode }) {
  const [theme, setTheme] = useState("light");
  const toggleTheme = () => setTheme(theme === "light" ? "dark" : "light");
  return (
    <ThemeContext.Provider value={{ theme, toggleTheme }}>
      <div className={theme}>{children}</div>
    </ThemeContext.Provider>
  );
}

export function useTheme() {
  return useContext(ThemeContext);
}

// Usage
export default function App() {
  const { theme, toggleTheme } = useTheme();
  return (
    <div>
      <p>Current theme: {theme}</p>
      <button onClick={toggleTheme}>Toggle Theme</button>
    </div>
  );
}

```

1. **Drag-and-Drop List**
Create a drag-and-drop sortable list using React state.

---

### **Next.js**

### **Server-Side Rendering (SSR)**

1. **Fetch Data Server-Side**
Create a page that fetches user details using `getServerSideProps`.

```tsx
export async function getServerSideProps() {
  const res = await fetch("https://jsonplaceholder.typicode.com/users");
  const users = await res.json();
  return { props: { users } };
}

export default function UsersPage({ users }: { users: any[] }) {
  return (
    <ul>
      {users.map(user => (
        <li key={user.id}>{user.name}</li>
      ))}
    </ul>
  );
}

```

### **Dynamic Routes**

1. **Product Pages with Dynamic Paths**
Create product pages with unique routes like `/product/[id]` fetching product data.

---

### **Redux**

### **State Management**

1. **Counter with Middleware**
Add middleware to log every action dispatched in a Redux counter app.

```tsx
const loggerMiddleware = (store: any) => (next: any) => (action: any) => {
  console.log("Dispatching:", action);
  const result = next(action);
  console.log("Next state:", store.getState());
  return result;
};

```

1. **Async API Calls**
Fetch data and store it in Redux using Redux Toolkit.

---

### **CSS Frameworks**

### **Tailwind CSS Challenges**

1. **Responsive Card Grid**
Design a responsive grid layout for cards using Tailwind CSS.

```html
<div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6">
  <div class="bg-white shadow rounded p-4">Card 1</div>
  <div class="bg-white shadow rounded p-4">Card 2</div>
  <div class="bg-white shadow rounded p-4">Card 3</div>
</div>

```

1. **Sticky Navbar**
Create a sticky navbar using Tailwind classes.

### **Bootstrap Challenges**

1. **Accordion Component**
Use Bootstrap to create a collapsible accordion for FAQs.

---

### **Advanced Topics**

### **Performance Optimization**

1. **Lazy Loading Images**
    
    Implement lazy loading in a React app using the `IntersectionObserver` API.
    
2. **Code Splitting with React**
    
    Split large components into smaller chunks using React’s `lazy` and `Suspense`.
    

### **Testing**

1. **Write Unit Tests**
Write tests for your components using Jest and React Testing Library.

---

### **JavaScript**

1. **Explain the difference between `var`, `let`, and `const`.**
    - `var` is function-scoped, meaning it is scoped to the nearest function block. Variables declared with `var` can be redeclared and updated.
    - `let` is block-scoped, meaning it is scoped to the nearest enclosing block (e.g., within loops or conditionals). It can be updated but not redeclared in the same block.
    - `const` is also block-scoped, but it cannot be reassigned after its initial assignment. However, if the variable holds an object, the object's properties can still be modified.
2. **How does the JavaScript event loop work? Can you explain using an example?**
    - The event loop is the mechanism that JavaScript uses to handle asynchronous code. It continuously checks the **call stack** and moves tasks from the **message queue** to the stack when it's clear.
    - Example: When a `setTimeout` is called, it goes to the Web APIs. Once the timer finishes, it moves to the callback queue. The event loop waits for the call stack to be empty before executing the callback function.
3. **What is the difference between `==` and `===`?**
    - `==` performs type coercion before comparison, meaning it converts the operands to the same type before comparing. For example, `1 == "1"` will return `true`.
    - `===` performs strict comparison, meaning it checks both the value and the type. For example, `1 === "1"` will return `false`.
4. **How would you debounce a function in JavaScript? Can you implement it?**
    - Debouncing ensures that a function is only called once after a certain delay, even if it is invoked multiple times.
    - Example:
        
        ```jsx
        function debounce(func, delay) {
          let timeout;
          return function (...args) {
            clearTimeout(timeout);
            timeout = setTimeout(() => func(...args), delay);
          };
        }
        const debouncedFn = debounce(() => console.log('Executed!'), 300);
        debouncedFn();
        
        ```
        
5. **Explain the concept of closures with an example.**
    - A closure is a function that retains access to its lexical scope even when the function is executed outside that scope.
    - Example:
        
        ```jsx
        function outer() {
          const name = "John";
          return function inner() {
            console.log(name);
          };
        }
        const innerFn = outer();
        innerFn(); // Output: "John"
        
        ```
        
6. **What are Promises? How are they different from callbacks?**
    - A **Promise** is an object representing the eventual completion or failure of an asynchronous operation. Promises provide `.then()` and `.catch()` methods for handling results or errors.
    - Unlike callbacks, Promises avoid callback hell (nested functions) and allow chaining.
    - Example:
        
        ```jsx
        let promise = new Promise((resolve, reject) => {
          let success = true;
          if (success) resolve("Success!");
          else reject("Failure");
        });
        promise.then(result => console.log(result)).catch(error => console.log(error));
        
        ```
        
7. **What is the difference between `map()`, `filter()`, and `reduce()`?**
    - `map()` creates a new array by applying a function to each element.
    - `filter()` creates a new array with elements that pass a test.
    - `reduce()` applies a function to accumulate a single result from all elements.
    - Example:
        
        ```jsx
        let arr = [1, 2, 3, 4];
        let mapped = arr.map(x => x * 2); // [2, 4, 6, 8]
        let filtered = arr.filter(x => x > 2); // [3, 4]
        let reduced = arr.reduce((acc, x) => acc + x, 0); // 10
        
        ```
        
8. **How would you deep clone an object in JavaScript?**
    - A deep clone creates a new object, recursively copying all properties of the original object.
    - Example:
        
        ```jsx
        function deepClone(obj) {
          return JSON.parse(JSON.stringify(obj));
        }
        const original = { a: 1, b: { c: 2 } };
        const cloned = deepClone(original);
        
        ```
        

---

### **TypeScript**

1. **What are TypeScript generics? Can you provide an example of their usage?**
    - Generics allow you to create reusable components that work with any data type, providing type safety.
    - Example:
        
        ```tsx
        function identity<T>(arg: T): T {
          return arg;
        }
        const num = identity(5); // num is of type number
        const str = identity("Hello"); // str is of type string
        
        ```
        
2. **How does TypeScript improve JavaScript code?**
    - TypeScript adds type annotations, which provide compile-time error checking, improving code quality and readability. It also supports modern JavaScript features and tools like interfaces, enums, and decorators.
3. **Explain the difference between `interface` and `type` in TypeScript.**
    - `interface` defines the structure of an object, whereas `type` is more flexible and can define primitive types, unions, intersections, etc.
    - Example:
        
        ```tsx
        interface Person {
          name: string;
          age: number;
        }
        type Animal = { species: string };
        
        ```
        
4. **What is the `unknown` type in TypeScript? How is it different from `any`?**
    - `unknown` is safer than `any` because it forces you to perform type checking before using the value. `any` allows any operation without checking types.
    - Example:
        
        ```tsx
        let value: unknown = 42;
        if (typeof value === "number") {
          console.log(value + 1); // This is safe
        }
        
        ```
        
5. **How would you use TypeScript to enforce function overloads?**
    - Function overloads allow a function to behave differently based on its arguments.
    - Example:
        
        ```tsx
        function greet(person: string): string;
        function greet(person: string, age: number): string;
        function greet(person: string, age?: number): string {
          return age ? `Hello ${person}, Age: ${age}` : `Hello ${person}`;
        }
        
        ```
        

---

### **React**

1. **What are React hooks? Explain `useState`, `useEffect`, and `useMemo` with examples.**
    - **`useState`**: A hook that manages state in functional components.
        
        ```tsx
        const [count, setCount] = useState(0);
        
        ```
        
    - **`useEffect`**: A hook that allows you to perform side effects (like fetching data or subscribing to events) in functional components.
        
        ```tsx
        useEffect(() => {
          console.log('Component mounted');
        }, []);
        
        ```
        
    - **`useMemo`**: A hook that memoizes the result of a function to optimize performance.
        
        ```tsx
        const memoizedValue = useMemo(() => computeExpensiveValue(a, b), [a, b]);
        
        ```
        
2. **How would you optimize a React application for performance?**
    - Use **React.memo** to prevent unnecessary re-renders.
    - Use **useCallback** and **useMemo** to memoize functions and values.
    - Implement **code splitting** and **lazy loading**.
    - Use **useEffect** and **useReducer** instead of `useState` in complex state management.
    - Avoid unnecessary rerenders using **shouldComponentUpdate** (for class components) or **React.memo**.
3. **What is the difference between controlled and uncontrolled components in React?**
    - A **controlled component**'s state is controlled by React (via `useState` or `this.setState`).
    - An **uncontrolled component** manages its own state, typically accessed via `refs`.
    - Example of controlled component:
        
        ```tsx
        const [value, setValue] = useState("");
        return <input value={value} onChange={e => setValue(e.target.value)} />;
        
        ```
        
4. **Explain the concept of a higher-order component (HOC).**
    - An HOC is a function that takes a component and returns a new component with additional props or behavior.
    - Example:
        
        ```tsx
        function withLogger(WrappedComponent) {
          return function(props) {
            console.log(props);
            return <WrappedComponent {...props} />;
          };
        }
        
        ```
        
5. **What is the purpose of `useReducer`, and how is it different from `useState`?**
    - `useReducer` is used for managing complex state logic in a more structured way, particularly when state changes depend on previous state values.
    - It's often used instead of `useState` for more complex state management scenarios (like when the state is an object or array).
6. **How does React handle reconciliation?**
    - React uses a **diffing algorithm** (reconciliation) to efficiently update the DOM. It compares the previous and current virtual DOM to determine the minimal number of changes required to update the actual DOM.
7. **Can you explain the React Context API with an example?**
    - The React Context API allows you to share values like themes or user authentication data across components without having to pass props down manually at each level.
    - Example:
        
        ```tsx
        const ThemeContext = createContext("light");
        
        function App() {
          return (
            <ThemeContext.Provider value="dark">
              <Child />
            </ThemeContext.Provider>
          );
        }
        
        function Child() {
          const theme = useContext(ThemeContext);
          return <div>{theme}</div>;
        }
        
        ```
        

---

### **Next.js**

1. **What is the difference between `getStaticProps`, `getServerSideProps`, and `getStaticPaths`?**
    - **`getStaticProps`** fetches data at build time (for static pages).
    - **`getServerSideProps`** fetches data on each request (for dynamic pages).
    - **`getStaticPaths`** is used alongside `getStaticProps` to generate dynamic routes based on data.
2. **How would you implement dynamic routing in Next.js?**
    - You can create dynamic routes by adding square brackets in filenames (e.g., `[id].tsx`).
3. **Explain the use of middleware in Next.js with an example.**
    - Middleware in Next.js allows you to run code before requests are completed (e.g., authentication).
    - Example:
        
        ```jsx
        export function middleware(req) {
          if (!req.cookies.token) {
            return NextResponse.redirect('/login');
          }
          return NextResponse.next();
        }
        
        ```
        
4. **How does Next.js handle API routes?**
    - API routes in Next.js are functions located in the `pages/api` directory that handle HTTP requests.
5. **What are the benefits of using Next.js over plain React?**
    - **SSR/SSG**: Server-side rendering and static site generation out of the box.
    - **File-based routing**: Simplified routing without the need for React Router.
    - **Optimized performance**: Automatic code splitting and image optimization.

---

### **Redux**

1. **What is Redux, and why would you use it?**
    - Redux is a state management library that provides a centralized store for managing application state. It helps in handling large, complex states by maintaining a predictable state container.
2. **Explain the concept of actions, reducers, and the store in Redux.**
    - **Actions** are payloads of information that send data from the app to the Redux store.
    - **Reducers** specify how the app state changes in response to actions.
    - **Store** holds the entire state of the application.
3. **What are middleware in Redux? Provide an example.**
    - Middleware extends Redux’s capabilities (e.g., for async actions). An example is `redux-thunk`, which allows action creators to return functions that can dispatch other actions.
4. **How does Redux Toolkit simplify state management?**
    - Redux Toolkit provides utilities like `createSlice

`and`createAsyncThunk` to simplify Redux store configuration and reduce boilerplate code.

1. **How would you handle asynchronous actions in Redux?**
    - You would use **middleware** like **redux-thunk** or **redux-saga** to handle asynchronous actions. For example:
        
        ```jsx
        const fetchData = () => async dispatch => {
          const response = await fetch('/api/data');
          const data = await response.json();
          dispatch({ type: 'FETCH_DATA_SUCCESS', payload: data });
        };
        
        ```
        

---

### **CSS Frameworks (Bootstrap, Tailwind CSS)**

1. **How does Tailwind CSS differ from traditional CSS?**
    - Tailwind CSS is a utility-first CSS framework, where you build components using single-purpose utility classes. Traditional CSS relies on writing custom classes for each component.
2. **What are utility-first CSS classes? Give an example using Tailwind.**
    - Utility-first classes are low-level utility classes that can be combined to style elements without writing custom CSS.
    - Example:
        
        ```html
        <div class="bg-blue-500 text-white p-4">Hello World</div>
        
        ```
        
3. **How would you create a responsive grid layout using Bootstrap?**
    - You can use the grid system (`row` and `col`) to create responsive layouts. Columns adjust according to screen size by adding breakpoints (`col-sm-`, `col-md-`, etc.).
4. **Explain the difference between `container`, `container-fluid`, and `row` in Bootstrap.**
    - `container` provides a responsive fixed-width container.
    - `container-fluid` provides a full-width container, stretching across the entire width.
    - `row` is used to group columns and apply proper spacing.
5. **How can you customize Tailwind CSS for a specific project?**
    - You can customize Tailwind CSS by editing the `tailwind.config.js` file, where you can add custom colors, fonts, and breakpoints.

---

### **Behavioral Questions**

1. **Can you describe a challenging project you worked on and how you overcame the challenges?**
    - Talk about a project where you had to solve a difficult technical problem (e.g., performance issues, debugging, scaling an app). Explain the challenges and the steps you took to resolve them.
2. **How do you stay updated with the latest trends in web development?**
    - Follow blogs, attend webinars, participate in coding challenges, and contribute to open-source projects. Regularly read documentation and research new tools and frameworks.
3. **Have you ever had a disagreement with a teammate? How did you resolve it?**
    - Explain a situation where you had a difference of opinion. Highlight how you communicated openly, respected their viewpoint, and came to a collaborative solution.
4. **Can you share an example of a time you improved the performance of an application?**
    - Describe optimizing a slow-loading page, reducing API calls, or implementing lazy loading to enhance performance.
5. **What motivates you to keep improving your skills?**
    - Express your passion for continuous learning, problem-solving, and staying ahead of new technologies in the ever-evolving field of web development.

---

### 1. **Build a React Component for a Todo List with Add, Delete, and Edit Functionalities**

```tsx
import React, { useState } from "react";

type Todo = {
  id: number;
  text: string;
};

const TodoList: React.FC = () => {
  const [todos, setTodos] = useState<Todo[]>([]);
  const [input, setInput] = useState("");
  const [editingId, setEditingId] = useState<number | null>(null);
  const [editInput, setEditInput] = useState("");

  const addTodo = () => {
    if (input.trim()) {
      setTodos([...todos, { id: Date.now(), text: input }]);
      setInput("");
    }
  };

  const deleteTodo = (id: number) => {
    setTodos(todos.filter((todo) => todo.id !== id));
  };

  const startEditing = (id: number, currentText: string) => {
    setEditingId(id);
    setEditInput(currentText);
  };

  const saveEdit = () => {
    setTodos(todos.map(todo =>
      todo.id === editingId ? { ...todo, text: editInput } : todo
    ));
    setEditingId(null);
    setEditInput("");
  };

  return (
    <div>
      <h2>Todo List</h2>
      <input
        type="text"
        value={input}
        onChange={(e) => setInput(e.target.value)}
        placeholder="Add a todo"
      />
      <button onClick={addTodo}>Add</button>
      <ul>
        {todos.map((todo) => (
          <li key={todo.id}>
            {editingId === todo.id ? (
              <>
                <input
                  type="text"
                  value={editInput}
                  onChange={(e) => setEditInput(e.target.value)}
                />
                <button onClick={saveEdit}>Save</button>
              </>
            ) : (
              <>
                {todo.text}
                <button onClick={() => deleteTodo(todo.id)}>Delete</button>
                <button onClick={() => startEditing(todo.id, todo.text)}>Edit</button>
              </>
            )}
          </li>
        ))}
      </ul>
    </div>
  );
};

export default TodoList;

```

---

### 2. **Implement a Custom Hook for Fetching Data in React**

```tsx
import { useState, useEffect } from "react";

const useFetch = <T,>(url: string): { data: T | null; error: string | null; loading: boolean } => {
  const [data, setData] = useState<T | null>(null);
  const [error, setError] = useState<string | null>(null);
  const [loading, setLoading] = useState<boolean>(true);

  useEffect(() => {
    const fetchData = async () => {
      try {
        const response = await fetch(url);
        if (!response.ok) throw new Error("Failed to fetch");
        const result = await response.json();
        setData(result);
      } catch (err: any) {
        setError(err.message);
      } finally {
        setLoading(false);
      }
    };
    fetchData();
  }, [url]);

  return { data, error, loading };
};

export default useFetch;

```

Usage:

```tsx
import React from "react";
import useFetch from "./useFetch";

const App: React.FC = () => {
  const { data, error, loading } = useFetch<any[]>("https://jsonplaceholder.typicode.com/posts");

  if (loading) return <p>Loading...</p>;
  if (error) return <p>Error: {error}</p>;

  return (
    <div>
      {data?.map((post) => (
        <p key={post.id}>{post.title}</p>
      ))}
    </div>
  );
};

```

---

### 3. **Write a Function in JavaScript to Flatten a Nested Array**

```jsx
function flattenArray(arr) {
  return arr.reduce(
    (acc, val) => Array.isArray(val) ? acc.concat(flattenArray(val)) : acc.concat(val),
    []
  );
}

const nestedArray = [1, [2, [3, 4], 5], 6];
console.log(flattenArray(nestedArray)); // Output: [1, 2, 3, 4, 5, 6]

```

---

### 4. **Create a Responsive Navbar Using Tailwind CSS**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <script src="https://cdn.tailwindcss.com"></script>
</head>
<body>
  <nav class="bg-blue-500 p-4">
    <div class="container mx-auto flex justify-between items-center">
      <div class="text-white text-lg font-bold">Brand</div>
      <button id="menuButton" class="lg:hidden text-white">Menu</button>
      <ul id="menu" class="hidden lg:flex space-x-4 text-white">
        <li><a href="#" class="hover:underline">Home</a></li>
        <li><a href="#" class="hover:underline">About</a></li>
        <li><a href="#" class="hover:underline">Contact</a></li>
      </ul>
    </div>
  </nav>
  <script>
    const menuButton = document.getElementById("menuButton");
    const menu = document.getElementById("menu");
    menuButton.addEventListener("click", () => {
      menu.classList.toggle("hidden");
    });
  </script>
</body>
</html>

```

---

### 5. **Implement a Counter Application with Redux**

### Redux Setup:

**actions.js**

```jsx
export const increment = () => ({ type: "INCREMENT" });
export const decrement = () => ({ type: "DECREMENT" });

```

**reducer.js**

```jsx
const initialState = { count: 0 };

export const counterReducer = (state = initialState, action) => {
  switch (action.type) {
    case "INCREMENT":
      return { count: state.count + 1 };
    case "DECREMENT":
      return { count: state.count - 1 };
    default:
      return state;
  }
};

```

**store.js**

```jsx
import { createStore } from "redux";
import { counterReducer } from "./reducer";

export const store = createStore(counterReducer);

```

### React Component:

```tsx
import React from "react";
import { useSelector, useDispatch } from "react-redux";
import { increment, decrement } from "./actions";

const CounterApp: React.FC = () => {
  const count = useSelector((state: { count: number }) => state.count);
  const dispatch = useDispatch();

  return (
    <div>
      <h1>Counter: {count}</h1>
      <button onClick={() => dispatch(increment())}>Increment</button>
      <button onClick={() => dispatch(decrement())}>Decrement</button>
    </div>
  );
};

export default CounterApp;

```

Wrap your app with the `Provider`:

```tsx
import React from "react";
import ReactDOM from "react-dom";
import { Provider } from "react-redux";
import { store } from "./store";
import CounterApp from "./CounterApp";

ReactDOM.render(
  <Provider store={store}>
    <CounterApp />
  </Provider>,
  document.getElementById("root")
);

```

---
