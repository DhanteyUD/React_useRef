# React-useRef
 
 - [x] The `useRef` Hook allows you to persist values between renders. 
 - [x] It can be used to store a mutable value that does not cause a re-render when updated. 
 - [x] It can be used to access a DOM element directly.
 
 ## Does Not Cause Re-renders
 
 If you try to count how many times your application renders using the `useState` Hook, you would be caught in an infinite loop since this Hook itself causes a re-render.
 
 To avoid this, you can use the `useRef` Hook.
 
 ### Example:
 
 Use `useRef` to track application renders.
 
```js 
import { useState, useEffect, useRef } from "react";
import ReactDOM from "react-dom/client";

function App() {
  const [inputValue, setInputValue] = useState("");
  const count = useRef(0);

  useEffect(() => {
    count.current = count.current + 1;
  });

  return (
    <>
      <input
        type="text"
        value={inputValue}
        onChange={(e) => setInputValue(e.target.value)}
      />
      <h1>Render Count: {count.current}</h1>
    </>
  );
}

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<App />);
```

`useRef()` only returns one item. It returns an Object called `current`.

When we initialize `useRef` we set the initial value: `useRef(0)`.

## Accessing DOM Elements

In general, you want to let React handle all DOM manipulation.

But there are some instances where `useRef` can be used without causing issues.

In React, we can add a `ref` attribute to an element to access it directly in the DOM.

### Example:

Use `useRef` to focus the input:

```js
import { useRef } from "react";
import ReactDOM from "react-dom/client";

function App() {
  const inputElement = useRef();

  const focusInput = () => {
    inputElement.current.focus();
  };

  return (
    <>
      <input type="text" ref={inputElement} />
      <button onClick={focusInput}>Focus Input</button>
    </>
  );
}

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<App />);
```
## Tracking State Changes

The `useRef` Hook can also be used to keep track of previous state values.

This is because we are able to persist `useRef` values between renders.

### Example:

Use `useRef` to keep track of previous state values:

```js
import { useState, useEffect, useRef } from "react";
import ReactDOM from "react-dom/client";

function App() {
  const [inputValue, setInputValue] = useState("");
  const previousInputValue = useRef("");

  useEffect(() => {
    previousInputValue.current = inputValue;
  }, [inputValue]);

  return (
    <>
      <input
        type="text"
        value={inputValue}
        onChange={(e) => setInputValue(e.target.value)}
      />
      <h2>Current Value: {inputValue}</h2>
      <h2>Previous Value: {previousInputValue.current}</h2>
    </>
  );
}

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<App />);
```
This time we use a combination of `useState`, `useEffect`, and `useRef` to keep track of the previous state.

In the `useEffect`, we are updating the `useRef` current value each time the `inputValue` is updated by entering text into the input field.
