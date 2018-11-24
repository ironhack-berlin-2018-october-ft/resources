# React Summary

- [Resources](#resources)
- [How to use React?](#how-to-use-react)
- [VS Code extensions for React](#vs-code-extensions-for-react)
- [Import/Export](#import-export)
- [Hello React](#hello-react)
- [JSX](#jsx)
- [React Components and Props](#react-components-and-props)
- [React State](#react-state)
- [React Lifecycle](#react-lifecycle)
- [React and Events](#react-and-events)
- [React and Conditional Rendering](#react-and-conditional-rendering)
- [React Lists and Keys](#react-lists-and-keys)
- [React Forms](#react-forms)
- [React Router](#react-router)
- [Using Axios with React](#using-axios-with-react)
- [Code Examples](#code-examples)
- [Coming soon](#coming-soon)


## Resources
- [React Official Documentation](https://reactjs.org/): They have a good [tutorial](https://reactjs.org/docs/hello-world.html), [advanced guides](https://reactjs.org/docs/jsx-in-depth.html) and [API Reference (list of all methods)](https://reactjs.org/docs/react-api.html)
- [React Router Offical Documentation](https://reacttraining.com/react-router/web/guides/)
- **[MERN Boilerplate](https://github.com/mc100s/mern-boilerplate)**

## How to use React?

### With Codepen 
To use React, you can either play on Codepen with this [Hello World React example on Codepen](https://reactjs.org/redirect-to-codepen/hello-world).

### With CodeSanbox

If you want something very quick to use, very close to what you can have with VS Code, you can go on CodeSanbox.io: https://codesandbox.io/s/new

### With `create-react-app` 
Or you can create a React application with your terminal:

```sh
# Only the first time 
$ npm install -g create-react-app

# To create a new React app
$ create-react-app my-app
$ cd my-app

# To start the React app
$ npm start # or yarn start
```

Then you have the following architecture:
- **`node_modules/`**
- **`public/`**: All the files here are accessible by the user
  - `index.html`: The HTML page displayed
- **`src/`**: All the React code
  - `App.css`
  - `App.js`
  - `App.test.js`
  - `index.css`
  - `index.js`: The main file
  - `logo.svg`
  - `serviceWorker.js`
- `.gitignore`
- `package.json`

## VS Code extensions for React

To have many useful shortcuts, you can install [ES7 React/Redux/GraphQL/React-Native snippets](https://marketplace.visualstudio.com/items?itemName=dsznajder.es7-react-js-snippets).

```js
// Shortcut: imp→	
import moduleName from 'module'

// Shortcut: imn→	
import 'module'

// Shortcut: imd→	
import { destructuredModule } from 'module'

// Shortcut: exp→ (→ is TAB)
export default moduleName

// Shortcut: exd→
export { destructuredModule } from 'module'

// Shortcut: rcc→ (React Class Component)
import React, { Component } from 'react'

export default class Filename extends Component {
  render() {
    return (
      <div>
        $1
      </div>
    )
  }
}

// Shortcut: rfc→ (React Function Component)
import React from 'react'

export default function Filename() {
  return (
    <div>
      $1
    </div>
  )
}
```

## Import/Export

```js
// variables.js

// There is maximum 1 export default
export default 10

export const a = 1
export let b = 2
export function c () {
  return 3
}
```


```
// playground.js

import x, { a, b, c } from "./variables.js";

console.log(x)   // => 10
console.log(a)   // => 1
console.log(b)   // => 2
console.log(c()) // => 3


import { a as apple, b as banana, c as carrot } from "./variables.js";

console.log(apple)    // => 1
console.log(banana)   // => 2
console.log(carrot()) // => 3
```

## [Hello React](https://reactjs.org/docs/hello-world.html)

The minimum code you need for React

```html
<!-- index.html -->
<html>
<head>
  <title>React App</title>
</head>
<body>
  <!-- The React content will be injected in this div -->
  <div id="root"></div>

  <!-- If you use create-react-app, you don't need to include any JS, it's done autmoatically -->
  <script src="index.js"></script>  
</body>
</html>
```

```js
// index.js
ReactDOM.render(
  <h1>Hello, world!</h1>,
  document.getElementById('root')
)
```

Page rendered (Chrome inspector):
```html
<html>
<head>
  <title>React App</title>
</head>
<body>
  <div id="root"><h1>Hello, world!</h1></div>
</body>
</html>
```

## [JSX](https://reactjs.org/docs/introducing-jsx.html)

JSX is a syntax extension to JavaScript. 

```js
const element = <h1>Hello, world!</h1>
```

A JSX will be always wrap in 1 tag, opened and closed.

```js
// Syntax error, 2 children
const wrongElement = (
  <section>first section</section>
  <section>second section</section>
)

// No syntax error, everything is wrapped by "<div>"
const rightElement1 = (
  <div>
    <section>first section</section>
    <section>second section</section>
  </div>
)

// No syntax error, everything is wrapped by "<React.Fragment>", that is invisible in the DOM
const rightElement2 = (
  <React.Fragment>
    <section>first section</section>
    <section>second section</section>
  </React.Fragment>
)

// Syntax error, the tag is never closed
const wrongImage = <img src="...">

// No syntax error, the tag is self closing
const rightImage = <img src="..." />
```

To embedding JavaScript expressions in JSX, you need to use `{}`

```js
// Simple example with expression
const x = 6
const y = 7
const element1 = <div>Product: {x} * {y} = {x*y}</div>
// renders ====> <div>Product: 6 * 7 = 42</div>

// Simple example with expression
const element2 = <div>Random number: {Math.floor(100 * Math.random())}</div>
// renders ====> <div>Random number: 87</div>

// Simple example with a JavaScript expression in an attribute 
// You mustn't wrap {} by quotes
const picture = "https://media.giphy.com/media/cFdHXXm5GhJsc/giphy.gif"
const element3 = <img src={picture} />
// DON'T DO:     <img src="{picture}" />
// renders ====> <img src="https://media.giphy.com/media/cFdHXXm5GhJsc/giphy.gif" />

const name = 'Smith'
const gender = 'female'
const element4a = <div>Hi {gender === 'male' ? 'Mr' : 'Mrs'} {name}!</div>
const element4b = <div>Hi Mr{gender === 'female' && 's'} {name}!</div>
// both render => <div>Hi Mrs Smith!</div>

const numbers = [1,2,4,8,16]
const element5 = <div>Numbers: {numbers}</div>
// renders ====> <div>Numbers: 124816</div>

const element6 = <ul>{numbers.map((number,i) => <li key={i}>{number}</li>)}</ul>
// renders ====> <ul>
//                 <li>1</li>
//                 <li>2</li>
//                 <li>4</li>
//                 <li>8</li>
//                 <li>16</li>
//               </ul>
```


## [React Components and Props](https://reactjs.org/docs/components-and-props.html)

A detailed component API reference is available [here](https://reactjs.org/docs/react-component.html).

2 differents syntaxes to write a component:
- **Function Component**: Can only take props and renders its return value.
- **Class Component**: Can use props and state and renders the return value of the `render` method.

```js
// Function Component definition
function Welcome1(props) {
  return <h1>Hello {props.name}</h1>
}

// Class Component definition (it's doing the same)
class Welcome2 extends React.Component {
  render() {
    return <h1>Hello {this.props.name}</h1>
  }
}

// Another Function Component definition
function App() {
  return (
    <div>
      {/* Component usage: it's the same for function and class components */}
      <Welcome1 name="Alice" />
      <Welcome2 name="Bob" />
    </div>
  )
}

ReactDOM.render(
  <App />,
  document.getElementById('root')
)
```

```html
<!-- Content rendered (Chrome inspector) -->
<div id="root">
  <div> <!-- Rendered from <App /> -->
    <h1>Hello Alice</h1> <!-- Rendered from <Welcome1 name="Alice" /> -->
    <h1>Hello Bob</h1>   <!-- Rendered from <Welcome1 name="Bob" /> -->
  </div>
</div>
```

There is one props special: `props.children`, explained in the following example:

```js
function MyComponent(props) {
  return <div>{props.children}</div>
}

// In some other components
// ...

{/* It works */}
<MyComponent children="My value" />

{/* Recommanded syntax */}
<MyComponent>My value</MyComponent>
```

A more complex example is available [here](https://codepen.io/maxencebouret/pen/yQzWoj). 

## [React State](https://reactjs.org/docs/state-and-lifecycle.html)

A class component can have a state. Every time the state is changed, it re-renders the component.

**To initialise a state value**: in the constructor `this.state = { myKey1: value1, myKey2: value2 }`

**To get a state value**: `this.state.myKey`

**To set a state value**: `this.setState({ myKey: newValue })` 
(and never `this.state.myKey = newValue` !!!)


Let's say you want to have a state with 2 keys:
- `random`: A number, between 1 and 100
- `history`: An array of numbers that remembers the list of all previous random values

This code display the states values and create a new random value when we click on the button.

```js
class App extends React.Component {
  constructor(props){
    super(props)
    // Initialisation of the state, always in the constructor
    this.state = {
      random: null,
      history: []
    }
  }
  handleClick() {
    let r = 1+Math.floor(100*Math.random()) // random value between 1 and 100
    // Set state values
    this.setState({
      random: r,
      history: [...this.state.history , r]
    })
  }
  render() {
    return (
      <div>
        <button onClick={() => this.handleClick()}>New random value</button> <br/>
        
        {/* Get state values */}
        random: {this.state.random} <br />
        history: {this.state.history.map((x,i) => <li key={i}>{x}</li>)} <br />
      </div>
    )
  }
}

ReactDOM.render(
  <App />,
  document.getElementById('root')
)
```

Another example of a component with a state (`<Bomb initalN={100} />`) available [here](https://codepen.io/maxencebouret/pen/GwOKNo)

## React Lifecycle

[![image](https://user-images.githubusercontent.com/5306791/48663701-41838d80-ea94-11e8-8807-0271701fe28f.png)](http://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/)



### Mounting

These methods are called in the following order when an instance of a component is being created and inserted into the DOM
- [`constructor()`](https://reactjs.org/docs/react-component.html#constructor): Must start with `super(props)`; Perfect to initialize the state and bind methods.
- [`render()`](https://reactjs.org/docs/react-component.html#render)
- [`componentDidMount()`](https://reactjs.org/docs/react-component.html#componentdidmount): Perfect place to call APIs and set up any subscriptions. 

### Updating

An update can be caused by changes to props or state. These methods are called in the following order when a component is being re-rendered

- [`shouldComponentUpdate(nextProps, nextState)`](https://reactjs.org/docs/react-component.html#shouldcomponentupdate) (only if you want to optimise your React application)
- [`render()`](https://reactjs.org/docs/react-component.html#render)
- [`componentDidUpdate(prevProps, prevState)`](https://reactjs.org/docs/react-component.html#componentdidupdate)

### Unmounting

This method is called when a component is being removed from the DOM:

- [`componentWillUnmount()`](https://reactjs.org/docs/react-component.html#componentwillunmount)

### Error Handling

These methods are called when there is an error during rendering, in a lifecycle method, or in the constructor of any child component.

- [`componentDidCatch()`](https://reactjs.org/docs/react-component.html#componentdidcatch)



### Example

Copy/paste this example, open it in Chrome with an opened console and see what happens when you type a name.

```js
// index.js
class DisplayInfo extends React.Component{
  constructor(props){
    console.log("- DisplayInfo::constructor")
    super(props)
  }
  render() {
    console.log("- DisplayInfo::render")
    return (
      <div>
        Hello {this.props.name}, your name as {this.props.name.length} characters!
      </div>
    )
  }
  componentDidMount() {
    console.log("- DisplayInfo::componentDidMount")
  }
  componentDidUpdate(prevProps, prevState) {
    console.log("- DisplayInfo::componentDidUpdate", prevProps, prevState)
  }
  componentWillUnmount() {
    console.log("- DisplayInfo::componentWillUnmount")
  }
}

class App extends React.Component {
  constructor(props){
    console.log("App::constructor")
    super(props)
    this.state = {
      name: "" 
    }
  }
  handleChange(event) {
    this.setState({
      name: event.target.value // the value of the input
    })
  }
  render() {
    console.log("App::render")
    return (
      <div>
      {/* When the input is changed, handleChange is triggered and set state.name to the input value */}
        <input type="text" value={this.state.name} onChange={(event)=>this.handleChange(event)} placeholder="Type a name" />
      
        {this.state.name !== "" && <DisplayInfo name={this.state.name} />}
      </div>
    )
  }
  componentDidMount() {
    console.log("App::componentDidMount")
  }
  componentDidUpdate(prevProps, prevState) {
    console.log("App::componentDidUpdate", prevProps, prevState)
  }
  componentWillUnmount() {
    console.log("App::componentWillUnmount")
  }
}

ReactDOM.render(
  <App />,
  document.getElementById('root')
)
```


## [React and Events](https://reactjs.org/docs/handling-events.html)

Handling events with React elements is very similar to handling events on DOM elements. There are some syntactic differences:

- React events are named using camelCase
- With JSX you pass a function as the event handler

**Examples**

```js
function alertTheAnswer() {
  alert(42)
}

{/* These 3 buttons are the same and display 42 on click */}

<button onClick={() => alert(42)}>
  What is the answer to life, the universe and everything? 
</button>

<button onClick={() => { alert(42) }}>
  What is the answer to life, the universe and everything? 
</button>

<button onClick={alertTheAnswer}>
  What is the answer to life, the universe and everything? 
</button>
```


### [List of events](https://reactjs.org/docs/events.html)

Event Types | Event Names | Event Properties
-- | -- | --
Clipboard Events | `onCopy` `onCut` `onPaste` | `clipboardData`
Composition Events | `onCompositionEnd` `onCompositionStart` `onCompositionUpdate` | `data` 
Keyboard Events | `onKeyDown` `onKeyPress` `onKeyUp` | `altKey` `charCode` `ctrlKey` `getModifierState(key)` `key` `keyCode` `locale` `location` `metaKey` `repeat` `shiftKey` `which` 
Focus Events | `onFocus` `onBlur` | `relatedTarget` 
Form Events | `onChange` `onInput` `onInvalid` `onSubmit` | 
Mouse Events | `onClick` `onContextMenu` `onDoubleClick` `onDrag` `onDragEnd` `onDragEnter` `onDragExit` `onDragLeave` `onDragOver` `onDragStart` `onDrop` `onMouseDown` `onMouseEnter` `onMouseLeave` `onMouseMove` `onMouseOut` `onMouseOver` `onMouseUp` | `altKey` `button` `buttons` `clientX` `clientY` `ctrlKey` `getModifierState(key)` `metaKey` `pageX` `pageY` `relatedTarget` `screenX` `screenY` `shiftKey`
Selection Events | `onSelect` | 
Touch Events | `onTouchCancel` `onTouchEnd` `onTouchMove` `onTouchStart` | `altKey` `changedTouches` `ctrlKey` `getModifierState(key)` `metaKey` `shiftKey` `targetTouches` `touches` 
UI Events | `onScroll` | `detail` `view` 
Wheel Events | `onWheel` | `deltaMode` `deltaX` `deltaY` `deltaZ` 
Media Events | `onAbort` `onCanPlay` `onCanPlayThrough` `onDurationChange` `onEmptied` `onEncrypted` `onEnded` `onError` `onLoadedData` `onLoadedMetadata` `onLoadStart` `onPause` `onPlay` `onPlaying` `onProgress` `onRateChange` `onSeeked` `onSeeking` `onStalled` `onSuspend` `onTimeUpdate` `onVolumeChange` `onWaiting` | 
Image Events | `onLoad` `onError` | 
Animation Events | `onAnimationStart` `onAnimationEnd` `onAnimationIteration` | `animationName` `pseudoElement` `elapsedTime` 
Transition Events | `onTransitionEnd` | `propertyName` `pseudoElement` `elapsedTime` 
Other Events | `onToggle` | 


### Binding your method

If you want to give a method to your event, you will probably need to bind your method.

In the example below, that is component to display a button with the number of likes, you will find below 4 ways to bind a method `handleClick`.

```js
// Method 1: arrow function in "onClick"
class LikeButton extends React.Component {
  constructor(props){
    super(props)
    this.state = {
      nbOfLikes: 0
    }
  }
  handleClick() {
    this.setState({
      nbOfLikes: this.state.nbOfLikes+1
    })
  }
  render() {
    return (
      // The arrow function set the "this" definition
      <button onClick={() => this.handleClick()}>
        {this.state.nbOfLikes} likes
      </button>
    )
  }
}

// Method 2: bind in "onClick"
class LikeButton extends React.Component {
  constructor(props){
    super(props)
    this.state = {
      nbOfLikes: 0
    }
  }
  handleClick() {
    this.setState({
      nbOfLikes: this.state.nbOfLikes+1
    })
  }
  render() {
    return (
      // "bind(this)" set the definition of this 
      <button onClick={this.handleClick.bind(this)}>
        {this.state.nbOfLikes} likes
      </button>
    )
  }
}

// Method 3: bind in constructor
class LikeButton extends React.Component {
  constructor(props){
    super(props)
    this.state = {
      nbOfLikes: 0
    }
    // "bind" sets the definition of this
    this.handleClick = this.handleClick.bind(this)
  }
  handleClick() {
    this.setState({
      nbOfLikes: this.state.nbOfLikes+1
    })
  }
  render() {
    return (
      <button onClick={this.handleClick}>
        {this.state.nbOfLikes} likes
      </button>
    )
  }
}

// Method 4: arrow function for the method
class LikeButton extends React.Component {
  constructor(props){
    super(props)
    this.state = {
      nbOfLikes: 0
    }
  }
  // Arrow function for a method autobind this (experimental feature)
  handleClick = () => {
    this.setState({
      nbOfLikes: this.state.nbOfLikes+1
    })
  }
  render() {
    return (
      <button onClick={this.handleClick}>
        {this.state.nbOfLikes} likes
      </button>
    )
  }
}
```




## [React and Conditional Rendering](https://reactjs.org/docs/conditional-rendering.html)

```js
// Component that display a login or logout button based on this.props.isLoggedIn
class MyComponent extends React.Component {
  showButton() {
    if (this.props.isLoggedIn)
      return <LogoutButton />
    else 
      return <LoginButton />
  }
  render() {
    let button
    if (this.props.isLoggedIn)
      button = <LogoutButton />
    else 
      button = <LoginButton />
    return (
      <div>
        {/********** Method 1: Variable **********/}
        {button}
        {/********** Method 2: Function **********/}
        {this.showButton()}
        {/********** Method 3: Ternary **********/}
        {this.props.isLoggedIn ? <LogoutButton /> : <LoginButton />}
        {/********** Method 4: Inline If with Logical && Operator **********/}
        {this.props.isLoggedIn && <LogoutButton />}        
        {!this.props.isLoggedIn && <LoginButton />}        
      </div>
    )
  }
}
```


## [React Lists and Keys](https://reactjs.org/docs/lists-and-keys.html)

```js
const students = ['Alice', 'Bob', 'Charly', 'David']

// Component that display a list of students
class MyComponent extends React.Component {
  showList() {
    let list = []
    for (let i = 0; i < students.length; i++) {
      list.push(<li key={i}>{students[i]}</li>)
    }
    return list
  }
  render() {
    let list = []
    for (let i = 0; i < students.length; i++) {
      list.push(<li key={i}>{students[i]}</li>)
    }
    return (
      <ul>
        {/********** Method 1: Variable **********/}
        {list}
        {/********** Method 2: Function **********/}
        {this.showList()}
        {/********** Method 3: Map **********/}
        {students.map((student,i) => <li key={i}>{student}</li>)}
      </ul>
    )
  }
}
```



## [React Forms](https://reactjs.org/docs/forms.html)

When we use forms in React, we generally follow this methodology.

First, for each items on the form (`<input />`, `<textarea />` and `<select></select>`), we set a property `value`(generally with a state) and a property `onChange`. 

**Example**:

```js
// Component method
handleChange = (event) => {
  this.setState({[event.target.name]: event.target.value});
}
```

```js
// Some code in the render

{/* This input display "this.state.firstname" and update this value on change  */}
<input type="text" name="firstname" value={this.state.firstname} onChange={this.handleChange} /> 

{/* This textarea display "this.state.occupation" and update this value on change  */}
<textarea name="occupation" value={this.state.occupation} onChange={this.handleChange} /> 

{/* This select display "this.state.debt" and update this value on change  */}
<select name="debt" value={this.state.debt} onChange={this.handleChange}>
  <option value={true}>Yes</option>
  <option value={false}>No</option>
</select>
```

Then, we need to listen at the form submission, with `onSubmit`.


**Example**:
```js
handleSubmit = (event) => {
  event.preventDefault() // To avoid going to the action page of the form

  // The code to be executed when the user submit the form (click on a button)
}
```

```js
// Some code in the render

<form onSubmit={this.handleSubmit}>
  {/* ... */}
</form>
```

**Full example of a component that display a list of characters and let the user add some.** Be careful, it's a shared API ;)

```js
// Don't import in Codepen, add a CDN in the settings instead
import axios from 'axios'

class App extends React.Component {
  constructor(props){
    super(props)
    this.state = {
      characters: [],
      name: '', // Default value for the form
      occupation: '', // Default value for the form
      debt: false, // Default value for the form
      weapon: '' // Default value for the form
    }
  }
  handleChange = (event) => {
    this.setState({
      [event.target.name]: event.target.value // the value of the input
    })
  }
  handleSubmit = (event) => {
    event.preventDefault();
    const character = {
      name: this.state.name,
      occupation: this.state.occupation,
      debt: this.state.debt,
      weapon: this.state.weapon,
    };
    axios.post('https://ih-crud-api.herokuapp.com/characters', character)
      .then(res => {
        console.log(res);
        console.log(res.data);
      })
  }
  handleClick = () => {
    this.setState({ characters: [] })
    axios.get('https://ih-crud-api.herokuapp.com/characters')
      .then(response => {
        this.setState({
          characters: response.data
        })
      })
  }
  render() {
    return (
      <div>
        <h2>Add a character</h2>
        <form onSubmit={this.handleSubmit}>
          Name: 
          <input type="text" name="name" value={this.state.name} onChange={this.handleChange} /> 
          <br />
          
          Occupation: 
          <textarea name="occupation" value={this.state.occupation} onChange={this.handleChange} /> 
          <br />
          
          Debt: 
          <select name="debt" value={this.state.debt} onChange={this.handleChange}>
            <option value={true}>Yes</option>
            <option value={false}>No</option>
          </select>
          <br />
          
          Weapon: 
          <input type="text" name="weapon" value={this.state.weapon} onChange={this.handleChange} /> 
          <br />
          
          <button type="submit">Add</button>
        </form>
        
        <h2>Display all characters</h2>
        <button onClick={this.handleClick}>Display the characters from the API</button> 
        
        <table>
          <thead>
            <tr>
              <th>Name</th>
              <th>Occupation</th>
              <th>Debt</th>
              <th>Weapon</th>
            </tr>
          </thead>
          <tbody>
            {this.state.characters.map(c => (
              <tr>
                <td>{c.name}</td>
                <td>{c.occupation}</td>
                <td>{c.debt ? 'Yes' : 'No'}</td>
                <td>{c.weapon}</td>
              </tr>
            ))}
          </tbody>
        </table>
      </div>
    )
  }
}

ReactDOM.render(
  <App />,
  document.getElementById('root')
)
```

## [React Router](https://reacttraining.com/react-router/web/guides/)

### Installation
```
$ npm install react-router-dom
```

### Import

```javascript
import { BrowserRouter, Route, Switch, Link, NavLink } from 'react-router-dom'
```

### React Router Components

<table>
  <tr>
    <th> Component </th>
    <th> Description </th>
    <th width="30%"> Main Props </td>
  </tr>
  <tr>
    <td><code>&lt;BrowserRouter&gt;</code></td>
    <td>Router Component that should wrap your application</td>
    <td>
    </td>
  </tr>
  <tr>
    <td><code>&lt;Route&gt;</code></td>
    <td>When the url matches its props <code>path</code>, it renders its content</td>
    <td>
      <ul>
        <li><code>path</code>: string</li>
        <li><code>component</code>: Component</li>
        <li><code>render</code>: func</li>
        <li><code>exact</code>: bool</li>
      </ul>
    </td>
  </tr>
  <tr>
    <td><code>&lt;Switch&gt;</code></td>
    <td>Group <code>&lt;Route&gt;</code> together and display maximum 1</td>
    <td>
    </td>
  </tr>
  <tr>
    <td><code>&lt;Link&gt;</code></td>
    <td>Replace the <code>&lt;a&gt;</code> tag of HTML in React Router</td>
    <td>
      <ul>
        <li><code>to</code>: string</li>
        <li><code>to</code>: object</li>
      </ul>
    </td>
  </tr>
  <tr>
    <td><code>&lt;NavLink&gt;</code></td>
    <td>A special version of the <code>&lt;Link&gt;</code> that will add styling attributes to the rendered element when it matches the current URL</td>
    <td>
      <ul>
        <li><code>activeClassName</code>: string</li>
        <li><code>activeStyle</code>: object</li>
        <li><code>exact</code>: bool</li>
      </ul>
    </td>
  </tr>
  <tr>
    <td><code>&lt;Redirect&gt;</code></td>
    <td>Will navigate to a new location</td>
    <td>
      <ul>
        <li><code>to</code>: string</li>
      </ul>
    </td>
  </tr>
</table>


### `match`

A component displayed with `<Route>` has access to `match` (as `this.props.match` or as `({ match }) => ()`) and it is an object containing the following properties:

Property | Type | Description
-- | -- | --
**`params`**| object | Key/value pairs parsed from the URL corresponding to the dynamic segments of the path
`isExact`| bool | `true` if the entire URL was matched (no trailing characters)
`path`| string | The path pattern used to match. Useful for building nested `<Route>`s
`url`| string | The matched portion of the URL. Useful for building nested `<Link>`s


### The Minimum Website with `react-router-dom`

First, we have to enable the routing in the React application with `<BrowserRouter>`
```js
// src/index.js

// Many imports...
// We import "BrowserRouter" and name it "Router"
import { BrowserRouter as Router } from 'react-router-dom';

// We need to wrap <App /> by <Router> to use routing inside it
ReactDOM.render((
  <Router>
    <App />
  </Router>
), document.getElementById('root'));
```

Second, we have to set some routes, with `<Route />` (and `<Switch>`), generally in `App.js` (and sometimes in extra files).
```js
// src/components/App.js
import React, { Component } from 'react';
import Home from './components/Home';
import About from './components/About';
import MyNavbar from './components/Navbar';
import { Switch, Route } from 'react-router-dom';

class App extends Component {
  render() {
    return (
      <div className="App">
        <MyNavbar />

        {/* With <Switch>, maximum 1 route is executed */}
        {/* The Home component will be displayed if the URL is exactly "/" */}
        {/* The About component will be displayed if the URL starts with "/about" */}
        {/* "404" will be rendered in any case (if the previous routes failed) */}
        <Switch>
          <Route exact path='/' component={Home}/>
          <Route path='/about' component={About}/>
          <Route render={() => <h1>404</h1>}/>
        </Switch>
      </div>
    );
  }
}

export default App;
```

Third, everytime we want to go to another page/URL, we never use `<a>` but `<Link>` or `<NavLink>`

```js
// src/components/Navbar.js
import React from 'react';
import { NavLink } from 'react-router-dom';

export default () => {
  return (
    <nav>
      <ul>
        {/* Add the class "bold" if the URL match the path (if nothing is precised, the default would be "active") */}
        <li><NavLink exact to="/" activeClassName="bold">Home</NavLink></li>
        <li><NavLink to="/about" activeClassName="bold">About</NavLink></li>
      </ul>
    </nav>
  )
}
```

```css
/* src/index.css */
.bold {
  font-weight: bold;
}
```

### How to create a route with some variable in the URL

Let's say we want to be able to extract the end of the following URL:
- http://localhost:3000/country/France
- http://localhost:3000/country/Germany

First, we have to create a `<Route>` with some pattern. Example:

```js
// Any component file, for example: src/components/App.js
<Route path="/country/:countryName" component={CountryDetail}/>
```

Then, we can create the component. Example: 

```js
// src/components/CountryDetail.js
import React, { Component } from 'react'

export default class CountryDetail extends Component {
  render() {
    return (
      <div>
        {/* We can access the value with: this.props.match.params.countryName */}
        Country: {this.props.match.params.countryName}
      </div>
    )
  }
}
```

Finally, we can have some link to this route. Example:
```js
// Any component file

// In render
let countries = ['France','Germany','Spain','Netherlands']
return (
  <div>
    {countries.map(c => <Link key={c} to={c}>{c}</Link>)}
  </div>
)
```


## Using Axios with React

### Installation 
```
$ npm install axios
```

```javascript
import axios from 'axios'
```

### Example of GET request
```javascript 
// Display all users from the API
class PersonList extends React.Component {
  constructor(props) {
    super(props)
    this.state = {
      persons: null // init to null
    }
  }

  render() {
    // If state.persons is null, it means we don't have the data from the API yet
    if (!this.state.persons) {
      return <div>Loading...</div>
    }
    return (
      <ul>
        { this.state.persons.map(person => <li>{person.name}</li>) }
      </ul>
    )
  }

  componentDidMount() {
    axios.get(`https://jsonplaceholder.typicode.com/users`)
      .then(res => {
        const persons = res.data;
        this.setState({ persons });
      })
  }
}
```

### Example of POST request

```javascript
// Add a person thanks to the API
class AddPerson extends React.Component {
  constructor(props) {
    super(props)
    this.state = {
      name: ''
    }
  }

  handleChange(event) {
    this.setState({ [event.target.name]: event.target.value });
  }

  handleSubmit(event) => {
    event.preventDefault();
    const user = {
      name: this.state.name
    };
    axios.post(`https://jsonplaceholder.typicode.com/users`, { user })
      .then(res => {
        console.log(res.data)
        // Redirect to the Home page
        this.props.history.push('/')
      })
  }

  render() {
    return (
      <div>
        <form onSubmit={this.handleSubmit.bind(this)}>
          Person Name:
          <input type="text" name="name" onChange={this.handleChange.bind(this)} />
          <button type="submit">Add</button>
        </form>
      </div>
    )
  }
}
```

### Base instance

```javascript
// src/api.js (in the client folder)
import axios from 'axios';

export default axios.create({
  baseURL: `http://jsonplaceholder.typicode.com/`
  withCredentials: true
})

const errHandler = err => {
  console.error(err)
  if (err.response && err.response.data) {
    console.error("API response", err.response.data)
  }
  throw err
}

export default {
  service: service,

  // Promise to return all users
  getUsers() {
    return service
      .get('/users')
      .then(res => res.data)
      .catch(errHandler)
  },

  // Promise to return 1 user
  getUser(id) {
    return service
      .get('/users/'+id)
      .then(res => res.data)
      .catch(errHandler)
  },

  // Promise to create a user
  addUser(user) {
    return service
      .post('/users', user)
      .then(res => res.data)
      .catch(errHandler)
  },
}
```

```javascript
// src/index.js
import api from './api';

// ...
api.getUser(1)
  .then(user => {
    console.log(user);
  })
// ...
```

Some hints when you use an API in a React website:
- If you want to display some data from an API, generally 

## Code Examples
- [React Data Binding (with components A, B, C, D)](https://codesandbox.io/s/p7y3jk8pq0)
- [Lab corrections and examples](https://github.com/ironhack-berlin-2018-october-ft)
  - [Bulma Components](https://github.com/ironhack-berlin-2018-october-ft/lab-bulma-components)
  - [Iron Nutrition](https://github.com/ironhack-berlin-2018-october-ft/lab-react-ironnutrition)
  - [Wiki Countries](https://github.com/ironhack-berlin-2018-october-ft/lab-wiki-countries)
  - [IronBeers](https://github.com/ironhack-berlin-2018-october-ft/lab-react-ironbeers)

## Coming soon
- Inline styling
- Reactstrap (React + Bootstrap)
- Mapbox and React
- React and SCSS
- Maybe Formik


