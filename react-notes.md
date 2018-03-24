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
* ES6 is a new version of JavaScript that adds some nice syntactical and functional additions (finalized in 2015 and most new browsers support)
* To work in all, transpose ES6 to JS
* All React components have a `render` function specifying the HTML output
* JSX, is a React extension that allows us to write JavaScript that looks like HTML.

