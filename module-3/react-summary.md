# React Summary

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
  <section>1st section</section>
  <section>2st section</section>
)

// No syntax error, everything is wrapped by "<div>"
const rightElement1 = (
  <div>
    <section>1st section</section>
    <section>2st section</section>
  </div>
)

// No syntax error, everything is wrapped by "<React.Fragment>", that is invisible in the DOM
const rightElement2 = (
  <React.Fragment>
    <section>1st section</section>
    <section>2st section</section>
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

const element = <div></div>
const element = <div></div>
const element = <div></div>
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

## State

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

## Lifecycle

[![image](https://user-images.githubusercontent.com/5306791/48663701-41838d80-ea94-11e8-8807-0271701fe28f.png)](http://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/)



### Mounting

These methods are called in the following order when an instance of a component is being created and inserted into the DOM
- [`constructor()`](https://reactjs.org/docs/react-component.html#constructor)
- [`render()`](https://reactjs.org/docs/react-component.html#render)
- [`componentDidMount()`](https://reactjs.org/docs/react-component.html#componentdidmount)

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