# Getting Started With React
https://github.com/fullstackreact/30-days-of-react

**Take a look at: array split, join, filter and map.**

Determine `state` - Ask three questions about each piece of data:
https://reactjs.org/docs/state-and-lifecycle.html
1. Is it passed in from a parent via props? If so, it probably isn’t state.
2. Does it remain unchanged over time? If so, it probably isn’t state.
3. Can you compute it based on any other state or props in your component? If so, it isn’t state.

**props are read-only**

Also be mindful that who owns state becomes **the source of truth**.

* Temperature converter from ReactJS.org: https://reactjs.org/docs/lifting-state-up.html

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
  * Create components for the children and add to the App (simple hard-coded example) child/parent relationship
* Comments in React (remember objects) `{/* This is a comment in React */}`
 

## FIVE - Data Diven Component
* Send data to components with **props**
* Reference the title within the component - <Header> component
  
```
<span className="title">
   {this.props.title}
</span>
```

* Set Header to different values when called

```
<Header title="Timeline" />
<Header title="Profile" />
<Header title="Settings" />
<Header title="Chat" />
```

* Can pass all kinds of things: objects, functions, numbers, etc.
* Define what props the content needs and create an object
* Example: setup object

```
{
  timestamp: new Date().getTime(),
  text: "Ate lunch",
  user: {
    id: 1,
    name: 'Shelly',
    avatar: "images/shelly.jpg"
  },
  comments: [
    { from: 'Ari', text: 'Me too!' }
  ]
}
```

* Use props
  
```jsx
class Content extends React.Component {
  render() {
    const {activity} = this.props; // ES6 destructuring

    return (
    <div>
      <div className="avatar">
         <img
           alt={activity.text}
           src={activity.user.avatar} />
         {activity.user.name}
       </div>
      <span className="time">
         {activity.timestamp}
      </span>
      <p>{activity.text}</p>
      <div className="commentCount">
         {activity.comments.length}
      </div>
    </div>
    )
  }
}
```

### Javascript within JSX - it's all JS

```jsx
//`activities` is an array of objects
render() {
    const {activities} = this.props;

    return (
      <div>
        {/* Use the array method `map` */}
        {/* Timeline item */}
        {activities.map((activity) => {
          return (
            <div className="item">
              <div className="avatar">
                <img
                  alt={activity.text}
                  src={activity.user.avatar} />
                {activity.user.name}
              </div>

              <span className="time">
                {activity.timestamp}
              </span>
              <p>{activity.text}</p>
              <div className="commentCount">
                {activity.comments.length}
              </div>
            </div>
          );
        })}

      </div>
    )
  }
}
```

### The React way would be to create components for the containing and displaying of content

```jsx
{/* Timeline item */}
{activities.map((activity) => (
  <ActivityItem
    activity={activity} />
))}
```
* use props to pass the data to the component
  

## SIX - Stateful Components - Clock Example
* Do not modify `this.props`, instead use state. Example of header title with props. If header updates prop then app no longer knows what the title is.
* Use props as much as possible, however there are times when component needs to update it's own state.
* Example: active flag on child component or timer. 
* Whenever the state changes (via the this.setState() function), the component will **rerender**.
* Clock example: will need to track the current time in the state of the component.
* Set intial state in the constructor() with this.state.
* First line of constructor needs to call `super(props)`
* Call `setState()` on the `this` value of the component as it's a part of the React.Component class we are subclassing.
* `this.setState()` can pass a function as a second argument. Guarantees function is called after `setState()`

```jsx
this.setState({loading: true}, this.updateData);

//OR

this.setState({
  currentTime: currentTime
}, this.setTimer);
```

* Only keep values in state that you are using in the render(). For example, new Date() delivers many more properties that hours, minutes, seconds - but those are the only ones to keep. Extra values/calculations cause unnecessary rendering and wasteful CPU cycles.


## SEVEN - Lifecycle Hooks - Updating timeline app with api call.
* Components loading is not instant. Takes a moment. Need hooks.
* `componentWillMount()` - called just before the component is due to be mounted on the page.
* `componentDidMount()` - called just after the component has been mounted.
* Mounting - converting the virtual components into actual DOM elements that are placed in the DOM by React.
* `componentWillUpdate()` - a hook to handle preparing our component for a change (don't call `this.setState()` to handle change as it will cause an infinite loop).
* `componentDidUpdate()`
* `componentWillReceiveProps()` - when the component is about to receive new props and update our state based on new props.
* `componentWillUnmount()` - called right before component is unmounted. Allows us to clean up (example of clock and setTimeout()).


## EIGHT - Packaging and PropTypes
* prop-types object export gives ability to define type of prop (string, number, bool, func, symbol, object, array, and anything with PropTypes.node)
* Import prop-types and then define

```
import PropTypes from 'prop-types'

class Header extends React.Component {
  // ...
}

Header.propTypes = {
  title: PropTypes.string
}
```
* Ability to communicate from child to parent using function.
* Define what an array can hold - `PropTypes.arrayOf([])`
* Define collection type
* Define object type
* Define React types - passing elements from a parent to child
* `isRequired` append to any proptype descriptions. Helpful when component relies on prop
```
MyComponent.propTypes = {
  title: PropTypes.name.isRequired,
}
```
* Can also have custom types
* Finally set `defaultProps`

## NINE - Styles
* **Remember** `class` becomes `className` in React
* Straight up link to CSS doc
```
render() {
  return <span className="menu navigation-menu">Menu</span>
}

// OR 

render() {
  let className = 'menu';
  if (this.props.isActive) {
    className += ' menu-active';
  }
  return <span className={className}>Menu</span>
}
```

* Option: Use of CSS Modules: https://glenmaddern.com/articles/css-modules

**From React Docs** CSS classes are generally more efficient than inline styles.

### Inline styles - add to component - use of JS Object
```
const style = { color: 'blue' }
<div style={style}>
  This text will have the color blue
</div>

// OR

render() {
  const divStyle = { color: 'blue' }
  return (
    <div style={divStyle}>
      This text will have the color blue
  </div>
  );
}
```
* React requires us to **camel-case** the style name: backgroundColor vs background-color

### Styling libraries
* Radium https://formidable.com/open-source/radium/ - inline style library
  * Scoped styles without selectors
  * Avoids specificity conflicts
  * Source order independence
  * Dead code elimination
  * Highly expressive
* ReactStrap https://reactstrap.github.io/


## TEN - Interactivity - Toggle search input - Great one for reading through.

https://www.fullstackreact.com/30-days-of-react/day-10/


* Regular JS uses event listeners.
* React handles events using `props`

For example: `addEventListener('mousemove', someFunction(){});` becomes

```
<div onMouseMove={(evt) => console.log(evt)}>
  Move the mouse over this text
</div>
```
* click, touch, drag, scroll, selection events, and many more: https://reactjs.org/docs/events.html
* Event object is reused and all properties will be nullified after the event callback has been invoked. (Cannot access asynchronous, can use `event.persist()` if needed to change this behavior)
* `onClick` - used a lot, become familiar!
* The idea is that clicks update the state of something, which causes a re-render: `this.setState()`

### Constructor function
* In JS, constructor runs when object is created and returns a reference to the Object function that created the instance's prototype.
* Runs when new object is created and method allows to setup instance variables right when it is created.
* With ES6 class syntax, call `super()` before any other method which calls the parent class's constructor.

### Show Search Box Example Flow
* `this.state = {searchVisible: false}`
* create function `showSearch()` that toggles searchVisible with `!this.state.searchVisible`
* `onClick` calls showSearch which toggles the state of searchVisible
* Remember, when state changes, re-render occurs
* The class on the input always starts with `searchInput`. Depending on the **state** could add `active` which will then show.

### Input Events - Search Form
* Mostly use `onSubmit()` and `onChange()` - get familiar!
* Create SearchForm component and add to the Header component inside `render()` and part of `return()`
* SearchForm is stateful since we hold on to the value of search input `this.state = {searchText: ''}`
* Pass searchVisible as prop from Header component
* Submit - call `event.preventDefault()`. Default behavior causes page to reload.
* Good practice to define as `defaultProps{}`
* Actual submitForm passed up to Header component and to another called Panel - looks like:
```
<Panel>
  <Header>
    <SearchForm></SearchForm>
  </Header>
</Panel>
```
* Common way of doing things - pass it along. The search passes to the header but since the panel displays the results, pass the search to the panel.
* filter function - filters out the values that return falsy values and keep truthy ones.


## ELEVEN - pure components or stateless
* Checkout React.Children for helpers related to mapping over children and unique key vals.
* Stateless can replace any component that has only a `render()` function.
```
// this is simple component
const HelloWorld = () => (<div>Hello world</div>);

//little bit more
const Notification = (props) => {
  const {level, message} = props;
  const classNames = ['alert', 'alert-' + level]
  return (
    <div className={classNames}>
      {message}
    </div>
  )
};
```
* Check out `React.Children` object


## TWELVE - create-react-app
Official generator app to get up and running.
* `npm install --global create-react-app`
* use nvm for version management 
* Get started: within designated directory, `create-react-app myApp && cd myApp`
* `npm start` compiles and starts server
* Review the folder structure created.
* Take a look at the package.json
  * scripts: start, build, test, eject. (Only eject on a branch - once done, it cannot be undone.)
* Built-in webserver (webpack) - changes will be updated in browser.
* Take a look at App.js - simple component with render() function.
* index.html - div for placement of React app. Styles can be included here. Mounting of the app takes place in index.js
* Create `components` directory.
  * Components (classes) names begin with capital letter (Header.js, Content.js, etc.)
  * Use `import MyComponent` similar to Browserify
  * Use `export default MyComponent` similar to Browserify. Single export exclude `{}`
```
import React from 'react';

class MyComponent extends React.Component {

}
export default MyComponent;
```
* `npm run build` creates a minified optimize version of app
  
  
## THIRTEEN - Repeating Elements
Within template tags, any JS can be used
```jsx
const a = [1, 10, 100, 1000, 10000];

const App = (props) => {
  return (
    <ul>
      {a.map(i => {
        return <li>{i}</li>
      })}
    </ul>
  )
}
```
### Array Methods
* map - accepts a function to be run on each element of the array

### Virtual DOM comes into play
* `<li>` needs more details so React knows what to update. 
* Provide unique keys with the `key` prop.

```jsx
const App = (props) => {
  return (
    <ul>
      {a.map(i => {
        return <li key={i}>{i}</li>
      })}
    </ul>
  )
}
```

* **Checkout** `React.cloneElement()`. Has the same API as the React.createElement() function where the arguments are:
  * The ReactElement we want to clone
  * Any props we want to add to the instance
  * Any children we want it to have.
* **Checkout** `React.Children` object - has utilities/methods for dealing with children.
* Updated example with React.Children. Adding the key is a utility.

```jsx
const App = (props) => {
  return (
    <ul>
      {React.Children.map(a, i => <li>{i}</li>)}
    </ul>
  )
}
```

## FOURTEEN - Remote Data

### Use of fetch
* This example is using fetch with npm install **check on** Not sure if needed.
* https://fetch.spec.whatwg.org/
* install fetch library `npm install --save whatwg-fetch`

## FIFTEEN - Promises

Promise States
* pending
* fulfilled (resolved)
* rejected (error)

```
var promise = new Promise(function(resolve, reject) {
  // call resolve if the method succeeds
  resolve(true);
})
promise.then(bool => console.log('Bool is true'))
```

## SIXTEEN - Display Remote Data
* Use of fetch - can use ajax or XMHTTPRequest
* returns a promise
* convert to format `.then(resp => resp.json())`

# Let's move along to other notes, now...
## SEVENTEEN - Routing
## EIGHTEEN > Flux and Redux for state/data management

## TWENTY-TWO > - Testing (Jasmine)
## TWENTY-SEVEN > Deployment




