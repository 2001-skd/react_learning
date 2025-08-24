
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
