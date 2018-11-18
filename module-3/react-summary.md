# React Summary

- [Resources](#resources)
- [How to use React?](#how-to-use-react)
- [Hello React](#hello-react)
- [JSX](#jsx)
- [React Components and Props](#react-components-and-props)
- [React State](#react-state)
- [React Lifecycle](#react-lifecycle)
- [React and Events](#react-and-events)
- [React and Conditional Rendering](#react-and-conditional-rendering)
- [React Lists and Keys](#react-lists-and-keys)
- [React Forms](#react-forms)



## Resources
- [React Official Documentation](https://reactjs.org/): They have a good [tutorial](https://reactjs.org/docs/hello-world.html), [advanced guides](https://reactjs.org/docs/jsx-in-depth.html) and [API Reference (list of all methods)](https://reactjs.org/docs/react-api.html)
- [React Router Offical Documentation](https://reacttraining.com/react-router/web/guides/)

## How to use React?

### With Codepen 
To use React, you can either play on Codepen with this [Hello World React example on Codepen](https://codepen.io/pen?&editors=0010).

### With CodeSanbox

If you want something very quick to use, very close to what you can have with VS Code, you can go on CodeSanbox.io: https://codesandbox.io/s/new

### With `create-react-app` 
Or you can create a React application with your terminal:

```
$ npm install -g create-react-app
$ create-react-app my-app
$ cd my-app
$ npm start
```

## Hello React

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

## JSX

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


## React Components and Props

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

## React State

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



## React and Conditional Rendering

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

## React and Events

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


## React Lists and Keys

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

When we use forms in React, we can use the following methodology.

First, for each items on the form (`<input />`, `<textarea />` and `<select></select>`), we set a property `value`(generally with a state) and a property `onChange`. Examples:
- .......................................


When we use forms in React, we use 2 main event listener.

The first event is **`onChange`**, used with .

**Basic Example with 1 input**

```javascript
class NameForm extends React.Component {
  constructor(props) {
    super(props);
    this.state = {value: ''};

    this.handleChange = this.handleChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
  }

  handleChange(event) {
    this.setState({value: event.target.value});
  }

  handleSubmit(event) {
    alert('A name was submitted: ' + this.state.value);
    event.preventDefault();
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <label>
          Name:
          <input type="text" value={this.state.value} onChange={this.handleChange} />
        </label>
        <input type="submit" value="Submit" />
      </form>
    );
  }
}
```

## React Router

### Installation
```
npm install --save react-router-dom
```

### Import

```javascript
import { BrowserRouter, Route, Link } from 'react-router-dom'
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
</table>


### `match`

A component displayed with `<Route>` has access to `match` (as `this.props.match` or as `({ match }) => ()`) and it is an object containing the following properties:

Property | Type | Description
-- | -- | --
`params`| bool | Key/value pairs parsed from the URL corresponding to the dynamic segments of the path
`isExact`| bool | `true` if the entire URL was matched (no trailing characters)
`path`| string | The path pattern used to match. Useful for building nested `<Route>`s
`url`| string | The matched portion of the URL. Useful for building nested `<Link>`s


## Using Axios with React

### Installation 
```
npm install --save axios
```

```javascript
import axios from 'axios'
```

### Example of GET request
```javascript 
class PersonList extends React.Component {
  constructor(props) {
    super(props)
    this.state = {
      persons: []
    }
  }

  componentDidMount() {
    axios.get(`https://jsonplaceholder.typicode.com/users`)
      .then(res => {
        const persons = res.data;
        this.setState({ persons });
      })
  }

  render() {
    return (
      <ul>
        { this.state.persons.map(person => <li>{person.name}</li>) }
      </ul>
    )
  }
}
```

### Example of POST request

```javascript
class PersonList extends React.Component {
  constructor(props) {
    super(props)
    this.state = {
      name: ''
    }
  }

  handleChange(event) {
    this.setState({ name: event.target.value });
  }

  handleSubmit(event) => {
    event.preventDefault();
    const user = {
      name: this.state.name
    };
    axios.post(`https://jsonplaceholder.typicode.com/users`, { user })
      .then(res => {
        console.log(res);
        console.log(res.data);
      })
  }

  render() {
    return (
      <div>
        <form onSubmit={this.handleSubmit.bind(this)}>
          <label>
            Person Name:
            <input type="text" name="name" onChange={this.handleChange.bind(this)} />
          </label>
          <button type="submit">Add</button>
        </form>
      </div>
    )
  }
}
```

### Base instance

```javascript
// src/api.js
import axios from 'axios';

export default axios.create({
  baseURL: `http://jsonplaceholder.typicode.com/`
});
```

```javascript
// src/index.js
import API from './api';

// ...
API.delete(`users/${this.state.id}`)
  .then(res => {
    console.log(res);
    console.log(res.data);
  })
// ...
```


## Coming soon
- Reactstrap (React + Bootstrap)
- Mapbox and React
- React and SCSS
- Maybe Formik


