# BL React Getting Started

## Seven Steps
1. Break the app into components
2. Build a static version of the app
3. Determine what should be stateful
4. Determine in which component each piece of state should live 
5. Hard-code initial states
6. Add inverse data flow
7. Add server communication

## JSX - JavaScript XML
Write HTML within JS
```JSX
const element = <h1>Hello, world!</h1>;

ReactDOM.render(
  element,
  document.getElementById('root')
);
```

* You can embed any JavaScript expression in JSX by wrapping it in curly braces.
* JSX is compiled and transformed into regular JavaScript
* May use quotes with attribute strings or curly braces to embed a JavaScript expression
```jsx
const element = <div tabIndex="0"></div>;
//OR
const element = <img src={user.avatarUrl}></img>;
```
* You should either use quotes (for string values) or curly braces (for expressions), but not both in the same attribute.

React DOM uses camel case and we don't want to overwrite standard HTML
* For example, class becomes className in JSX, and tabindex becomes tabIndex.

JSX tags may have children - wrapping it in parentheses to avoid the pitfalls of automatic semicolon insertion.

```jsx
const element = (
  <div>
    <h1>Hello!</h1>
    <h2>Good to see you here.</h2>
  </div>
);
```

Everything is converted to a string before being rendered

## Babel compiles JSX into React.createElement() calls.
These are the same
```jsx
const element = (
  <h1 className="greeting">
    Hello, world!
  </h1>
);
const element = React.createElement(
  'h1',
  {className: 'greeting'},
  'Hello, world!'
);
```

