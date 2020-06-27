# Context & Hooks

- A nice way to work with shared data
- Redux uses Context and provides a way to handle state mutation, while Context is about access to state

# Context API

- Share state within component tree
- Gives central place to store state and share between components
- Components grab the data when needed

# Add Context + Provider

```js
import React, { createContext, Component } from 'react'

export const ThemeContext = createContext();

export class ThemeContextProvider extends Component {
    render() 
        return (
           <ThemeContext.Provider value={{...this.state}}>
            { this.props.children }
           </ThemeContext.Provider>
        )
    }
}

```

- `value` provides its data to whatever the Provider wraps
- `this.props.children` refers to the components that the provider wraps

# Accessing Context

- 2 ways

## Context Type

- Used in class components

```js
static contextType = ThemeContext;
render(){
  ...
}
```

- The context type of the component we want to use is the `ThemeContext`
- We now have access to all the data passed in: `this.context`

## Context Consumer

- Used in functional components

```js
render() {
    return (
        <ThemeContext.Consumer>{(context) => {
            return (
            // html
            )
        </ThemeContext.Consumer>
    )
}
```

- Can access context with the passed in `context` parameter
- **Can consume multiple contexts**

# Multiple Contexts

- Nest them together and they work

## Consuming Multiple Contexts

- Must use context consumers (`contextType` will not work as we will have 2 static properties with the same name)
- Can mix and match: 1 `contextType` +context consumers, only context consumers

```js
export class Navbar extends Component {
    static contextType = ThemeContext;
    render() {
        return (
            <AuthContext.Consumer>{(authContext) => (
                <ThemeContext.Consumer>{(themeContext) => {
                    
                    )
                }}
                </ThemeContext.Consumer>
            )}
            </AuthContext.Consumer>
        )
    }
}
```

- Notice how `AuthContext` only returns JSX using `( )` instead of `{ }`

# React Hooks

- Special functions
- Do cool stuff inside functional components
    - ex. Use state

## `useState()`

- Use state within functional component

```js
const [fruit, setFruit] = useState('orange');

// equivalent to
var fruitStateVariable = useState('orange'); // Returns a pair
var fruit = fruitStateVariable[0]; // First item in a pair
var setFruit = fruitStateVariable[1]; // Second item in a pair
```
- `orange` is the initial value of `fruit`
- `setFruit` is basically the `setState` function for class components
- `useState` returns a pair, an array of 2 items
- First item is the current value, and the second is a function that lets us update it

## `useEffect()`

- Run code when a component renders/re-renders
- By default, runs after all data changes

```js
// only run hook when fruit data changes
useEffect(() => {
  ...
}, [fruit])
```

- Can pass in an array of data that we want to watch for changes

# Hooks with Context

## `useContext()`

- Consume context in functional component

```js
const { light, dark } = useContext(ThemeContext)
```

## Create context with functional components

- Combine `useState` and `createContext`