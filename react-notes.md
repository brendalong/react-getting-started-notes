# Getting Started With React
https://github.com/fullstackreact/30-days-of-react

## One

* React is a JavaScript library for building user interfaces, the view layer for web applications.
* Full of components - a self-contained module that renders output
   * A button could be a component
   * Components are **composable** - put one inside another
   * Components relate to interface elements and then can relate to higher level elements
   * Example: Form
   * React components have strict data management
* How does it work - React does not operates directly on the browser's DOM immediately. React uses a virtual DOM (memory). Changes are made in memory and then determines what needs changes to actual document. This is faster.
* We write a virtual component that React will turn into the DOM.

## TWO - JSX/ES6 - Hello World
* ES6 version of JavaScript with nice syntactical and functional additions (finalized in 2015 and most new browsers support)
* To work in all, transpose ES6 to JS
* All React components have a `render` function specifying the HTML output
* JSX, is a React extension that allows us to write JavaScript that looks like HTML.
* Attribute **className** (same as class)
* Review JSX and JS comparison (which one is easier)

## THREE - Component
* Include React library
* Use of Babel - transpiler from ES6 to ES5
* `ReactDOM.render(<what>, <where>)`
* Component
  * All React components require at least a `render()` function. This returns a virtual DOM representation of browser DOM elements.

```
class App extends React.Component {
    render() {
      return <h1>Hello from our app</h1>
    }
 }
```
* Need to tell it **where and what**

```
var mount = document.querySelector('#app');
ReactDOM.render(<App />, mount);
```

## FOUR - Complex Components (good visuals)
* Take a look at css structure: https://gist.github.com/auser/2bc34b9abf07f34f602dccd6ca855df1
* Break down large into smaller chunks (components). Skill developed with experience.
  * App(wrapper/parent), Title Bar(child), and Conent(child)
  * Example: start by adding main content into the render of the app.
  * Create components for the children and add to the App (simple hard-coded example)
* Comments in React (remember objects) `{/* This is a comment in React */}`
 



