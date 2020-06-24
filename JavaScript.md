# Basics

### Unary Plus
```js
console.log(+"+20"); // 20
```

## Comparisons

`==` and `===`
- `==` just compares value
- `===` compares value and type

```js
null == undefined //true
null === undefined //false
```
### Non-truthy (!!)
- 0
- ""
- false
- null
- undefined
- NaN

## Hoisting

- Function declarations 
- Var

### `let` and `var`

- `var` is function scope
- `let` is block{} scope

## Functions

Declaration: 
```js
function ok(){
  console.log("ok");  
}
```
- available in entire scope 
- semicolons at the end of function declarations are not necessary; semicolons separate statements however declarations are not statements as they are evaluated before the code is executed (hoisting)
Expression 
```js
let epic = function ok(){
  console.log("ok");  
};
epic(); //ok
```
### Anonymous functions
```js
let cool = function(var){
  console.log(var);  
}
cool("amazing"); //amazing
```

### Shorthand Notation

### Arrow Notation
```js
//let func = (arg1, arg2, ...argN) => expression

let sum = (a, b) => a + b;
let sum = function(a, b) {
  return a + b;
};

const isEven = num = > ( //implicit return 
  num % 2 == 0
)

const hi = () => alert("hi"); //1 line implicit return 

const makeCard = () => ({suit: 'hearts', val: 5}); 
// implicitly return object literal
// {} implies function body and ({}) is a return value

```

## The DOM (Document Object Model)

- A tree (parents, siblings) representing a webpage
- HTML is parsed by a browser to the DOM

### JS manipulation: convert CSS kebab-case into JS camelCase

## Bubbling

- When an event occurs on an element, it runs on itself -> parent -> up to its ancestors

```html
<form onclick="alert('form')">FORM
  <div onclick="alert('div')">DIV
    <p onclick="alert('p')">P</p>
  </div>
</form>
```
- A click on `<p>` runs `onclick` on `<p>` -> `<div>` -> `<form>` -> ...  ->`document`
- *Almost* all events bubble

### `event.target`

- The element that causes the event is the *target* element (accessed through `event.target`)
- note difference between `event.target` and `this`

### Event propagation

1. Capturing - event goes down to element
2. Target - event reached target element
3. Bubbling - event bubbles up from element

- Can stop bubbling using `event.stopPropagation()`/`event.stopImmediatePropagation()`
- No real need to prevent bubbling

# Array stuff
- Map, Reduce, Filter, Sort

### Sort

- Remember to make the function return 1 or -1, that is how sorting works

### Spread

- "Spreads" array elements; all elements in the array are treated as separate elements being passed through
- Useful for copying arrays/objects as they are reference types
    - note: spread only goes 1 level deep, not good for deep copy of nested arrays
```js
nums = [1,2,3,4,5]
Math.min(nums); // NaN
Math.min(...nums) // 1 

console.log(..."epic") // e p i c 
```
# Objects
- String (key), Value pairs
```js
let user = new Object(); // Object Constructor
let user = {}; // Object literal 

let user = {
  name: "Nick",
  age: 19,
  "Likes Lisa": true  // multiword property 
};

alert(user['Likes Lisa']); // remember keys are strings, case-sensitive

delete user;
```
- A `const` object's properties can change
```js
const user = {
  name = 'a';  
}
user.name = 'b'
```
## `in` 
- check if property with key exists
```js
alert('Likes Lisa' in user); // true
```
### `for in`
```js
for(let i in user){
  alert(i); // name, age, Likes Lisa
  alert(user[i]); // Nick, 19, true
}
```
- Keys are listed in creation order, however integers are ordered 
- `for in` is for objects, `for of` is for other iterables

## Constructors 

- Note `new` keyword

```js
function Book(title, author, read){
  this.title = title;
  this.author = author;
  this.read = read;
}
book1 = new Book('redwall', 'brian jacques', true);
```

## Prototype

- All objects have a non-enumerable (hidden) prototype property (parent) that is another object or `null`
- `Object.getPrototypeOf/Object.setPrototypeOf`

### Prototype Chain

- If we look for a property in a child and it's missing, JS takes it from the prototype (prototype chain)
```js
let animal = {
  eats: true
  
};

let rabbit = {
  jumps: true 
};

//rabbit.prototype = Object.create(animal.prototype);
Object.setPrototypeOf(rabbit, animal); // obj, prototype
console.log(rabbit.eats); // true
```
#### `for..in`
- Iterates through inherited properties
```js
for(let key in rabbit){
  console.log(key);
  //jumps
  //eats
}
```
### Prototypes and `this`

- `this` is not affected by prototypes, is always the object before the 

### `this`

- `.call()` and `.apply` binds the correct `this` value by passing in a scope

## Private and Public Scope - Module Pattern

- Emulated through Closures (function wrappers; new function = new scope)
- Encapsulation using scope, methods are only available through the `Module` namespace
```js
var Module = (function () {
  var myModule = {};
  var _privateMethod = function () {

  };
  myModule.publicMethod = function () {

  };
  return myModule; // returns the Object with public methods
})();

// usage
Module.publicMethod();
```
## Closures

- An inner function has access to the outer function scope
```js
function outer(a){
  return function inner(b){
    console.log('a is ' + a);
    console.log('b is ' +b);
  }
}
const newFunction = outer('outside');
newFunction(); 
//a is outside;
//b is undefined 
newFunction('inside'); 
// a is outside
// b is inside
```

## IIFE

- Invoke a function expression immediately
- Used for encapsulation
```js
(function () {
    var a = 'hey';
    console.log(a); // hey
})();

console.log(a); // undefined
```

## Classes

- `constructor()` is automatically called by `new`

# Asynchronous JS

```js
loadScript('/my/script.js'); // contains function fx()
fx(); // undefined
```
- `loadScript` is executed asynchronously, any code after is executed while it is loading
- While `loadScript` is loading, `fx` runs (undefined!)

## Callbacks

```js
loadScript('/my/script.js', () => {
  // the callback runs after the script is loaded
  fx(); // works
  ...
});
```
- Second argument runs when the action is completed
- Nesting looks bad
    - Make every action a standalone function (okay fix)

## Promises

```js
let p = new Promise(function(resolve, reject) {
  // do async tasks...
  if(/* good */) {
    resolve('yay');
  } else {
    reject('bad');
  }
});

p.then(function(result){
  // something with result
}).catch(function() {
  // uh oh
}).finally(function() {
  // executes regardless
})
```
Another example:
```js
Promise.all([
  loadImage(image1),
  loadImage(image2),
  loadImage(image3)
]).then((images) => {
  // do image stuff
}).catch((error) => {
  // handle error
})
```