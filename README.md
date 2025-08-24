
# React Notes

## React Fundamentals and Core Concepts

### Why React ?

- Before the release of React, web development was largely dominated by **jQuery**.  
  jQuery is a popular JavaScript library that was widely used to manipulate the DOM and handle events, making it easier to build interactive user interfaces compared to using plain JavaScript.

```html
<div id="app"></div>
<script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
<script>
  $("#app").text("Hello World");
</script>
```

- However, in jQuery, the application state was tightly coupled with the DOM.  
  This meant that to change the state of an application, developers had to manually traverse the DOM, find the specific nodes, and update them.  
  This approach was imperative and mutated the original state, which made complex applications harder to maintain and scale.

- To address some of these issues, **Backbone.js** emerged.  
  It introduced an MVC (Model-View-Controller) pattern, where the state could be managed in models, and the UI was defined in views.  
  This brought some structure to JavaScript applications, but it still relied on mutable state and didn’t fully solve the challenges of state synchronization with the UI.

- Next, **AngularJS** entered the scene with more built-in features, such as:  
  - Two-way data binding  
  - Dependency injection  
  - Inbuilt state management  
  - A more declarative style of building UIs  

- This made building dynamic web apps easier, but Angular also had its own complexity and performance challenges.

- Then in **2013, React** was developed and released by Facebook.  
  Initially, many developers were skeptical of React due to its unconventional approach (like using JSX), but over time, it gained massive popularity due to several key innovations:

  - **Virtual DOM**: React uses a virtual representation of the DOM to efficiently update only the parts of the UI that change, improving performance.  
  - **Component-based architecture**: UIs are built using reusable components, making the codebase modular and maintainable.  
  - **Unidirectional data flow**: React enforces a predictable flow of data, making it easier to debug and understand application state.  
  - **Separation of concerns**: Instead of separating concerns by technologies (HTML, CSS, JS), React separates concerns by components, allowing state (data) and UI logic to live together in a cohesive unit.  

```jsx
import React from "react";
import ReactDOM from "react-dom";

function App() {
  return <h1>Hello React</h1>;
}

ReactDOM.render(<App />, document.getElementById("root"));
```

---

## React Is Declarative Library , But What Declarative Means ?

### Imperative Programming
- In imperative programming, we need to tell the computer how to do things step by step.  
- For example, in Vanilla JS or jQuery, we have to specify what we want, along with a detailed step-by-step approach.  

```html
<ul id="list"></ul>
<script>
  const items = ["Apple", "Banana", "Cherry"];
  items.forEach(item => {
    const li = document.createElement("li");
    li.textContent = item;
    document.getElementById("list").appendChild(li);
  });
</script>
```

### Declarative Programming
- In Declarative Programming, we don’t need to tell step-by-step approach — instead we specify **what we want**.  
- For example, in React, we don’t need to tell the step-by-step approach. Instead, we declare how the UI should look, and React handles the rest.  

```jsx
function App() {
  const items = ["Apple", "Banana", "Cherry"];
  return (
    <ul>
      {items.map(item => (
        <li key={item}>{item}</li>
      ))}
    </ul>
  );
}
```

---

## JSX In React

- In React, to create components, we need to declare elements.  
- Traditionally, HTML elements were used to show content directly. But in React, we use a different approach.

### InBuilt Approach

React provides a built-in method to create elements:  

```js
React.createElement(type, props, children)
```

- **type** → The type of HTML element (like `h1`, `p`, `a`, etc.)  
- **props** → These are like attributes in HTML (such as `className`, `id`, etc.)  
- **children** → This is the content that goes inside the element  

> This works, but it becomes hard to read and manage, especially when we create many elements or deeply nested elements.

---

### JSX

- To solve this problem, **JSX (JavaScript Syntax Extension)** was introduced.  
- JSX is the second way to create elements in a React component.  
- It looks like HTML, but it works inside JavaScript.  

Benefits:
- With JSX, you can write the UI (HTML) and the logic (JS) together in one place.  
- It makes your code easier to read, maintain, and debug.  

⚠️ Browsers do not understand JSX directly. Behind the scenes, **Babel (a transpiler)** converts JSX into `React.createElement()` calls.

```jsx
const element = <h1 className="greeting">Hello JSX</h1>;
```

---

### JSX Rules
- Should have **one root parent element** → Use a wrapper element or React Fragment.  
- Props should always use **camelCase**.  
- Should **close all tags**.  

```jsx
// Wrong ❌
return (
  <h1>Hello</h1>
  <p>World</p>
);

// Correct ✅
return (
  <div>
    <h1>Hello</h1>
    <p>World</p>
  </div>
);
```

```jsx
// Using Fragment ✅
return (
  <>
    <h1>Hello</h1>
    <p>World</p>
  </>
);
```

### JSX Best Practices
- Use **Fragments** to avoid unnecessary nodes.  
- Maintain **consistent indentation** for readability.  
- Avoid too many **inline styles** → prefer CSS or styled-components.  
- Ensure **unique and descriptive keys** when rendering lists.  

```jsx
const users = ["Alice", "Bob", "Charlie"];

return (
  <ul>
    {users.map((user, index) => (
      <li key={index}>{user}</li>
    ))}
  </ul>
);
```

### JSX Misconceptions
- JSX is **not HTML** → it is syntactic sugar for JavaScript function calls.  
- JSX is **not required** → you can use React without JSX.  
- JSX does **not compile to HTML** → it compiles to JavaScript (React elements).  

---

## Component Based Architecture

- React follows a **component-based architecture**, which is a design pattern.  
- It allows us to **break apps into small, reusable components**.  
- Each component is self-contained and encapsulated.  

Advantages:
- **Reusable**  
- **Modular**  
- **Scalable**  
- **Testable**  
- **Easier to deploy**  

```jsx
function Greeting({ name }) {
  return <h1>Hello, {name}!</h1>;
}

export default function App() {
  return (
    <div>
      <Greeting name="Alice" />
      <Greeting name="Bob" />
    </div>
  );
}
```


## React DOM

- DOM is the programming interface for web page documents, which is the backbone for web applications and plays a vital role in web development.  
- By using DOM we can create interactive web applications.  
- DOM stands for **Document Object Model**, which is a tree representation of our document (as an object) containing nodes such as text, attributes, and elements.  
- By using DOM, we can manipulate the elements and styles programmatically.  

---

## Why is DOM Important?

- With DOM, we can enhance the user experience by creating animations, real-time content updates, and validations.  
- We can create **dynamic web pages** that respond to server data.  

---

## Virtual DOM

- As web development grew and applications became larger and more complex, developers needed a more efficient way to update and render the UI.  
- Updating the **Real DOM** for every small change is inefficient.  
- React introduced the **Virtual DOM (VDOM)** to solve this problem, making developers’ lives easier.  

---

## What is Virtual DOM?

- VDOM is an **in-memory representation** of the actual DOM.  
- In the real DOM, even small state changes cause the **entire UI to re-render**, which is inefficient.  
- With VDOM, React uses algorithms to update only what has changed in the UI, improving performance.  

---

## How it Works

### 1. Initial Render
- When a component is rendered for the first time, a corresponding VDOM is created.  

### 2. State Changes
- Whenever the state changes, React updates the VDOM instead of the real DOM.  

### 3. Diffing and Reconciliation
- VDOM uses a **diffing algorithm** to compare the old VDOM with the new VDOM.  
- Only the parts that changed are updated in the real DOM.  

### 4. Batch Updates
- After differences are identified, React updates the **real DOM** in batches, improving performance.  

---

## Advantages of VDOM

1. **Performance Optimization**  
   - Real DOM re-renders everything on every update.  
   - VDOM only re-renders what has changed.  

2. **Developer Friendly**  
   - React’s declarative nature means developers don’t need to worry about how the UI updates.  
   - Just declare how the UI should look, and React handles the updates.  

3. **Easy State Management**  
   - State updates are automatically reflected in the UI without manual DOM manipulation.  

---

## Common Pitfalls

1. Over-relying on VDOM  
2. Excessive or unnecessary state updates  

---

## Best Practices for Optimizing VDOM Usage

### 1. Use Keys for Lists

Whenever rendering lists, always provide a unique `key` so React can efficiently track changes.  

```jsx
const items = ["Apple", "Banana", "Cherry"];

function App() {
  return (
    <ul>
      {items.map((item, index) => (
        <li key={index}>{item}</li>
      ))}
    </ul>
  );
}
```

---

### 2. Use Memoization

For expensive calculations or large components, use **`React.memo`** or **`useMemo`** to avoid unnecessary re-renders.  

```jsx
import React, { useMemo, useState } from "react";

function ExpensiveComponent({ num }) {
  const computedValue = useMemo(() => {
    console.log("Calculating...");
    return num * 2;
  }, [num]);

  return <p>Computed: {computedValue}</p>;
}

export default function App() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <button onClick={() => setCount(count + 1)}>Increment</button>
      <ExpensiveComponent num={count} />
    </div>
  );
}
```

---

### 3. Break Down Components

Breaking down large components into smaller reusable ones reduces re-renders and improves readability.  

```jsx
function Item({ name }) {
  return <li>{name}</li>;
}

function ItemList({ items }) {
  return (
    <ul>
      {items.map((item) => (
        <Item key={item} name={item} />
      ))}
    </ul>
  );
}

export default function App() {
  const fruits = ["Apple", "Banana", "Cherry"];
  return <ItemList items={fruits} />;
}
```

---

# React Components #

# Component Classes vs. Functional Components in React

React has revolutionized the way we think about user interfaces by introducing component-based architecture. As a developer, understanding the different types of components is crucial for building efficient and maintainable applications. This section delves into the nuances of **Component Classes** and **Functional Components**, providing insights into their pros, cons, and best use cases.

---

## What Are Component Classes?

Component Classes, often referred to simply as **class components**, are the traditional way of defining components in React. These components are ES6 classes that extend the base `React.Component` class.

### Defining a Class Component

Here’s a simple example:

```jsx
import React from 'react';

class Greeting extends React.Component {
    render() {
        return <h1>Hello, {this.props.name}!</h1>;
    }
}

export default Greeting;
```

In the example above, the `Greeting` class component accepts `props` and uses the `render` method to display a greeting message.

---

## The Lifecycle of Class Components

One significant advantage of class components is the built-in **lifecycle methods** that allow developers to perform actions at specific points in the component’s life.  

Some commonly used lifecycle methods include:

- **componentDidMount** → Invoked after the component is mounted.  
- **componentDidUpdate** → Invoked immediately after updating occurs.  
- **componentWillUnmount** → Invoked immediately before a component is unmounted and destroyed.  

Utilizing these lifecycle methods effectively can lead to improved performance and user experience.

---

## What Are Functional Components?

Functional components, also known as **stateless components** (historically), are simpler and often preferred for their ease of use. They are JavaScript functions that return React elements.  

⚡ With the introduction of **Hooks** (React 16.8), functional components gained the ability to **manage state** and **side effects**, making them as powerful as class components.

### Why were functional components called "stateless"?

- **Before Hooks** → Functional components could not hold state. They just accepted `props` and returned JSX, hence the term "stateless".  
- **After Hooks** → Functional components can now use `useState`, `useEffect`, and other Hooks to manage state and lifecycle, making the term “stateless” outdated.

---

### Defining a Functional Component

```jsx
import React from 'react';

const Greeting = ({ name }) => {
    return <h1>Hello, {name}!</h1>;
}

export default Greeting;
```

This `Greeting` functional component does the same thing as its class counterpart but is more concise and easier to read.

---

## Using Hooks in Functional Components

Hooks are one of the key features that have made functional components more **functional**. With Hooks, developers can use state and other React features without writing class components.

### Example: Using `useState` and `useEffect`

```jsx
import React, { useState, useEffect } from 'react';

const Counter = () => {
    const [count, setCount] = useState(0);

    useEffect(() => {
        document.title = `Count: ${count}`;
    }, [count]);

    return (
        <div>
            <p>Count: {count}</p>
            <button onClick={() => setCount(count + 1)}>Increment</button>
        </div>
    );
}

export default Counter;
```

In this example:
- `useState` is used to manage the count state.  
- `useEffect` updates the document title whenever the count changes.  

---

## Class Components vs. Functional Components: A Comparison

1. **Syntax and Readability**  
   - Functional components are more concise and easier to read.  
   - Class components are more verbose due to `class` syntax and lifecycle methods.  

2. **State Management**  
   - Before Hooks → Only class components could manage state.  
   - After Hooks → Functional components can also manage state effectively.  

3. **Lifecycle Methods vs. Hooks**  
   - Class components rely on lifecycle methods (`componentDidMount`, etc.).  
   - Functional components use Hooks (`useEffect`) for lifecycle events.  

4. **Performance**  
   - Functional components have a smaller footprint and generally better performance due to less overhead.  

5. **Testing**  
   - Functional components are easier to test because they are pure functions.  
   - Class components may involve complex state and lifecycle logic.  

---

## Best Practices and Use Cases

### When to Use Class Components
- If you need lifecycle methods that are not directly covered by Hooks.  
- When working with legacy codebases with existing class-based components.  

### When to Use Functional Components
- For **new projects**, since they are modern, concise, and easier to read.  
- If you want to take advantage of React’s **Hooks** for state management and side effects.  
- When reusability and simplicity are priorities.  

---

## ✅ Key Takeaways

- **Before Hooks** → Class components were stateful; functional components were stateless.  
- **After Hooks** → Functional components are now fully stateful and preferred in modern React.  
- Functional components + Hooks = Modern standard for React development.  


