# React.Js Interview Questions

## What is React ??

- React is a Open-source JavaScript Frontend library for building user interfaces.
- It is maintained by Facebook and a community of individual developers and companies.
- React can be used as a base in the development of single-page or mobile applications.
- React allows us to create reusable UI components.
- React is declarative, which means we can write components that describe the user interface and React will automatically manage and update the UI as the data changes.
- React uses a virtual DOM to improve performance.
- It follows One-way data binding or Unidirectional data flow.
- It supports server-side rendering which helps in SEO(Search Engine Optimization).

## What is JSX ??

- JSX stands for JavaScript XML.
- JSX (JavaScript XML) is a syntax extension for JavaScript that allows developers to write code that looks similar to HTML or XML within JavaScript.
- JSX is not a necessity to write React applications, but it makes the code more readable and easier to write.
- JSX is a preprocessor step that adds XML syntax to JavaScript.
- It is used with React to describe what the UI should look like.
- JSX produces React “elements”.
- JSX expressions must have one parent element.
- Example:

  ```jsx
  export default function App() {
    return <h1 className="greeting">{"Hello, this is a JSX Code!"}</h1>;
  }
  ```

  ```jsx
  import { createElement } from "react";

  export default function App() {
    return createElement(
        "h1",
        { className: "greeting" },
        "Hello, this is a JSX Code!"
    );
  }
  ```

## What is the difference between Element and Component ?

- An Element is a plain object describing what you want to appear on the screen in terms of the DOM nodes or other components.
- Elements can contain other Elements in their props.
- Creating a React element is cheap.
- Once an element is created, it cannot be mutated.
- Example:

  ```jsx
  const element = React.createElement("div", { id: "login-btn" }, "Login");
  ```

  and this element can be simiplified using JSX:

  ```jsx
  <div id="login-btn">Login</div>
  ```

  The above `React.createElement()` function returns an object as below:

  ```jsx
  {
    type: 'div',
    props: {
        children: 'Login',
        id: 'login-btn'
    }
  }
  ```

  Finally, this element renders to the DOM using ReactDOM.render().

## When to use a Class Component over a Function Component?

- It is always preffered to use Function components over Class components in React. Because you could use state, lifecycle methods and other features that were only available in class component present in function component too.

- Use Function Components:

  - If you don't need state or lifecycle methods, and your component is purely presentational.

  - For simplicity, readability, and modern code practices, especially with the use of React Hooks for state and side effects.

- Use Class Components:

  - If you need to manage state or use lifecycle methods.

  - In scenarios where backward compatibility or integration with older code is necessary.

Note: You can also use reusable react error boundary third-party component without writing any class. i.e, No need to use class components for Error boundaries.

## What are pure components?

- Pure components are the components that do not re-render if the state or props of the component has not changed.