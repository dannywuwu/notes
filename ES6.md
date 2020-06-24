# Destructuring

ex. React: passing in props `first` and `last`

```js
const component = props => {
  const {first, last} = props;
  return (
    // instead of props.first, props.last
    <h1>Hello {first} {last}</h1>
  );
}
```

- Changing variable names:

```js
const {first: a} = props;
console.log(a);
```

## Arrays

```js
let names = ['danny', 'Danny', 'wu'];
let [first, middle, last] = ['danny', 'Danny', 'wu']

console.log(first + middle); // dannyDanny

middle = '';
console.log(middle); //
```

# Arrow Functions

- Function shorthand using => syntax
- Lexical (Static) `this` 

# Template Literals

```js
let a = 'first';
let b = 'last';
let c = `${a}   ${b}`
console.log(c); // first   last
```

# Object Literals

```js
const address = {city: city, state: state};
const address = {city, state};
```

- If keys are the same as the values, no need to set

# For of/For in

- For of is for iterables
- For in is for objects

```js
for(const char of string){
  console.log(char);
}
```

- log each char by char

### Remember: Designed to iterate over variables, not mutate them (ex. changing `const` to `let` does not allow for mutation)

# Spread `...`

```js
let a = [1,2,3,4,5];
let b = [...a];
```

- Unwraps values of `a` into `b`

## Rest  

```js
function add(nums){
  console.log(nums);
  // {0: 2, 1: 4, 2: 6} 
  // NOT an array
}

function add(...nums){
  console.log(nums);
  // [2, 4, 6]
}

add(2, 4, 6);
```

- When you are not sure how many values are to be inputted

# Default Parameters

```js
function(a = 'default'){
  console.log(a); //default
}
```

# Let/Const

- Block scoping, no hoisting

# Import/Export

```js
// file 1
export const data = [1, 2, 3];

// file 2
import { data } from './file1'
console.log(data); // [1, 2, 3]
```

# Classes

```js
// animal.js
export class Animal {
  constructor(type){
    this.type = type;
  }
}

// main.js
import { Animal } from './animal.js'
let cat = new Animal('feline');
```

- Classic
- Best when combined with import/export

###  `static` functions

- Do not need to create an instance of the class to use it
- Import the class in, call with `Class.function()`

# Async

```js
// traditional approach
fetch(url)
    .then()
    .catch()
```

- `fetch` gets data and returns a promise of type `response`
- `.then` handles the promise once it is delivered
- `.catch` fires if there is an error

## Await

```js
async apiCall(){
  // wait until fetch completes
  const response = await fetch(url);
  // wait for the response and turn it into json
  const json = await response.json();
}
```