# BL React Getting Started

## Seven Steps
1. Break the app into components
2. Build a static version of the app
3. Determine what should be stateful
4. Determine in which component each piece of state should live 
5. Hard-code initial states
6. Add inverse data flow
7. Add server communication

### Example component (with element and render())
```jsx
function tick() {
  const element = (
    <div>
      <h1>Hello, world!</h1>
      <h2>It is {new Date().toLocaleTimeString()}.</h2>
    </div>
  );
  ReactDOM.render(
    element,
    document.getElementById('root')
  );
}

setInterval(tick, 1000);
```

You can convert a functional component (like Clock) to a class in five steps:
1. Create an ES6 class, with the same name, that extends React.Component.
1. Add a single empty method to it called render().
1. Move the body of the function into the render() method.
1. Replace props with this.props in the render() body.
1. Delete the remaining empty function declaration.

### Example as class with state
```jsx
function FormattedDate(props) {
  return <h2>It is {props.date.toLocaleTimeString()}.</h2>;
}

class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }

  componentDidMount() {
    this.timerID = setInterval(
      () => this.tick(),
      1000
    );
  }

  componentWillUnmount() {
    clearInterval(this.timerID);
  }

  tick() {
    this.setState({
      date: new Date()
    });
  }

  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <FormattedDate date={this.state.date} />
      </div>
    );
  }
}

ReactDOM.render(
  <Clock />,
  document.getElementById('root')
);

```

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
**Recommend naming props from the component’s own point of view rather than the context in which it is being used.**
