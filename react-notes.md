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
this.setState({
  currentTime: currentTime
}, this.setTimer);
```

* Only keep values in state that you are using in the render(). For example, new Date() delivers many more properties that hours, minutes, seconds - but those are the only ones to keep. Extra values/calculations cause unnecessary rendering and wasteful CPU cycles.


## Seven - Lifecycle Hooks - Updating timeline app with api call.
* Components loading is not instant. Takes a moment. Need hooks.
* `componentWillMount()` - called just before the component is due to be mounted on the page.
* `componentDidMount()` - called just after the component has been mounted.
* Mounting - converting the virtual components into actual DOM elements that are placed in the DOM by React.
* `componentWillUpdate()` - a hook to handle preparing our component for a change (don't call `this.setState()` to handle change as it will cause an infinite loop).
* `componentDidUpdate()`
* `componentWillReceiveProps()` - when the component is about to receive new props and update our state based on new props.
* `componentWillUnmount()` - called right before component is unmounted. Allows us to clean up (example of clock and setTimeout()).


## Eight - Packaging and PropTypes
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
