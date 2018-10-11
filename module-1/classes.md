# Classes

## ES6 Syntax

### Constructor

```js
class MyClass() {
  constructor(param1, param2) {
    this.attributeA = param1;
    this.attributeB = param2;
    // ...
  }
  // ...
}
```

### Method

```js
class MyClass() {
  // ...
  method1(x, y) {
    // ...
  }
}
```

### Creating object (same as ES5)

```js
// Declaring a new object by calling the constructor
var myObject = new MyClass(42, "Berlin");

// Accessing properties
myObject.attributeA; // => 42
myObject.attributeB; // => "Berlin"

// Using a method
myObject.method1(6, 7);
```

### Inheritance

```js
class ParentClass {
  constructor(param1) {
    this.param1 = param1;
    // ...
  }
}

class ChildClass extends ParentClass {
  constructor(param1,param2) {
    super(param1);
    this.param2 = param2;
  }
}
```

### Example


```js
class Shape {
  constructor(id, x, y) { // constructor syntactic sugar
    this.id = id;
    this.setLocation(x, y);
  }
  
  setLocation(x, y) { // prototype function
      this.x = x;
      this.y = y;
  }
  
  getLocation() {
    return {
      x: this.x,
      y: this.y
    };
  }
  
  toString() {
    return 'Shape("' + this.id + '")';
  }
}

function Circle extends Shape {
  constructor(id, x, y, radius) {
    super(id, x, y); // call Shape's constructor via super
    this.radius = radius;
  }
  
  toString() { // override Shape's toString
    return 'Circle > ' + super.toString(); // call `super` instead of `this` to access parent
  }
}

// test the classes
var myCircle = new Circle('mycircleid', 100, 200, 50); // create new instance
console.log(myCircle.toString()); // Circle > Shape("mycircleid")
console.log(myCircle.getLocation()); // { x: 100, y: 200 }
```



## ES5 Syntax

### Constructor

```js
function MyClass(param1, param2){
  this.attributeA = param1;
  this.attributeB = param2;
  // ...
}
```

### Method

```js
MyClass.prototype.method1(x, y){
  // ...
}
```

### Creating object

```js
// Declaring a new object by calling the constructor
var myObject = new MyClass(42, "Berlin");

// Accessing properties
myObject.attributeA; // => 42
myObject.attributeB; // => "Berlin"

// Using a method
myObject.method1(6, 7);
```

### Inheritance

```js
function ParentClass (param1) {
  this.param1 = param1;
  // ...
}

function ChildClass(param1,param2) {
  ParentClass.call(this, param1);
  this.param2 = param2;
}
ChildClass.prototype = Object.create(ParentClass.prototype);
ChildClass.prototype.constructor = ChildClass;
```

### Example

```js
function Shape(id, x, y) {
  this.id = id;
  this.setLocation(x, y);
}

Shape.prototype.setLocation = function(x, y) {
  this.x = x;
  this.y = y;
};

Shape.prototype.getLocation = function() {
  return {
    x: this.x,
    y: this.y
  };
};

Shape.prototype.toString = function() {
  return 'Shape("' + this.id + '")';
};

function Circle(id, x, y, radius) {
  Shape.call(this, id, x, y);
  this.radius = radius;
}
Circle.prototype = Object.create(Shape.prototype);
Circle.prototype.constructor = Circle;

Circle.prototype.toString = function() {
  return 'Circle > ' + Shape.prototype.toString.call(this);
};

// test the classes
var myCircle = new Circle('mycircleid', 100, 200, 50); // create new instance
console.log(myCircle.toString()); // Circle > Shape("mycircleid")
console.log(myCircle.getLocation()); // { x: 100, y: 200 }
```
