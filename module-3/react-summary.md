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
);
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
const element = <h1>Hello, world!</h1>;
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
  return <h1>Hello {props.name}</h1>;
}

// Class Component definition (it's doing the same)
class Welcome2 extends React.Component {
  render() {
    return <h1>Hello {this.props.name}</h1>;
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
  );
}

ReactDOM.render(
  <App />,
  document.getElementById('root')
);
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

## Stte a d Lifecycle

