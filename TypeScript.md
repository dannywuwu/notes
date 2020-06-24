### `tsc file.ts -w`

-  Watches and compiles `file.ts` into `file.js`

# Types

- Typing does not have to be explicit; TS infers variable type based on assigned value

```ts
let name = 'danny' // string
let age = 1 // number
let epic = true // boolean
```

```ts
const double = (num: number) => {
  return num * 2;
}
```

- Specify type of parameters
- Type checks on compile

##  Mixing Types

```ts
let nums = [1, 2, 3];
nums.push('four'); // error

let mixed = ['five', 6, true]
// this array can now contain strings, numbers, and booleans
```

### Objects

- Property types are unchangeable
- Cannot add additional properties onto objects upon instantiation

```ts
let gosu = {
  name: 'gang',
  dumpling: 100
}

gosu = {
  name: 'yong',
  //dumpling: 100
}
```

- Cannot add/omit properties on reassignment
- Must have same structure

# Explicit Types

```ts
let name: string;
let age: number;
let epic: boolean;

// Initialize arrays with an empty []
let ninjas: string[] = [];
ninjas.push('danny');
```

### Union Types

```ts
// Array of strings/numbers
let mixed: (string|number)[] = [];

let union: string|number;
```

### Objects

```ts
let me: object;

let me2: {
  name: string,
  age: number
}

me2 = { name: 'danny', age: 2 }
```

# Dynamic Type `any`

```ts
let age: any = 100;
age = 'cool';
age = false;
```

- All valid

# tsconfig

### `tsc --init`

```ts
// tsconfig.json

"outDir":
"rootDir":
...
},
"include": ["src"] // only compile from src folder
```

- TS scripts are in rootDir, compile to outDir

# Functions

```ts
let f: Function;

const add = (a: number, b: number, c?: number | string) => {
  console.log(a + b);
}

// returns a number
const add = (..., c: number = 10): number => {
  return c; // default 10
}

// no error, c is optional
add(5, 10);
```

### `?:`

- Optional argument
- Can also use default parameter with `=`, then no need for `?:`

# Type Alias

```ts
type StringOrNum = string | number;
type username = { name: string, id: StringOrNum }

const hi = (user: username) => {
  ...
}
```

# Function Signatures

```ts
() => void // no args, return void

let hi: (a: string, b: string) => void;

hi = (name: string, greeting: string) => {
  ...
}
```

- Be careful of if/else - if you do not cover all cases the return value may have the same type as the function signature

# The DOM

- TypeScript is so cool because recognizes HTML element types 
- When selecting a node, the node may not exist (object is possibly null)
- We should wrap selectors with if statements or if we are certain they exist, append a `!` before the semicolon

```ts
const link = document.querySelector('a')!;

console.log(anchor.href); // no error
```

## Casting

- When passing in elements with IDs/classes, TS recognizes them as type `Element`
- We can cast these elements

```ts
const form = document.querySelector('.new-form') as HTMLFormElement;
```
- Can take off `!` as the type will never be null, it will always be the type of the cast

# Classes

- Same as Vanilla JS
- All properties are by default public, can be accessed from anywhere

```ts
class Person {
  public name: string;
  private age: number;
  readonly cool: boolean;
}
```

- `readonly` is public but immutable

###  Constructor shorthand

```ts
constructor(
  public name: string,
  private age: number,
  readonly cool: boolean,
){}
```
- Automatically assigns values to parameters with access modifiers
- No need for `this.name = ...`

# Interfaces

- Enforce class/object structure
- Type checking classes

```ts
interface IsPerson {
  name: string;
  age: number;
  speak(a: string): void;
  sleep(a: number): boolean;
}

const me: IsPerson = {
  name: 'danny', 
  ... implement fields
}
```

## Interfaces with Classes

```ts
interface HasShoes(){
  shoes(): number;
}

class Person implements HasShoes {
  shoes() {
    return 3;
  }
}
```

- Class `Person` must follow the structure of the `HasShoes` interface 
    - Must include the `shoes()` function
- Now we know that `Person` instances have 3 shoes, we can now create variables of type `HasShoes` to house Person instances 

```ts
let personOne: HasShoes;
let personTwo: HasShoes;

personOne = new Person();
personTwo = new Duck();
```

- It is obvious that `Person` and `Duck` instances have shoes so this makes sense

```ts
let coolKids: HasShoes[] = [];
```

- An array of cool kids who have shoes

# Generics

- Create reusable code which can be used with different types

```ts
// <T> must be an object with the name property
const objID = <T extends {name: string>(obj: T) => {
  let id = 68;
  // return new object with id propert
  return {...obj, id};
}

```

- Generics capture the properties on the objects we pass in
- In this example, if we did not use a generic we do not know what properties are on the returned object 

```ts
interface document<T> {
  id: number;
  name: string;
  data: T;
}

// T is a string
const paper: document<string> = {
  id: 70,
  type: 'letter',
  data: 'bounceu bounceu'
}
```

# Enums

```ts
enum DocumentType { BOOK, LETTER, MANGA }

interface document<T> {
  id: number;
  type: DocumentType;
  data: T;
}

const paper: document<string> = {
  id: 70,
  type: DocumentType.LETTER,
  data: 'bounceu bounceu'
}

console.log(paper.type); // 1
```

- Each `enum` keyword is associated with its index

# Tuples

- Types are fixed once you define a tuple

```ts
let tup: [string, number, boolean] = ['cool', 1, true];
```

- Useful for constructors where parameters must be of a certain type (spreading in values from a tuple)