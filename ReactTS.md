### `create-react-app [appname] --typescript`

### `React.FC` - Functional component

##  Props

```typescript
export const Component: React.FC<{ text: string }> = () => {
}
```

- Destructure props

```typescript
interface Props {
  text: string
}

Component: React.FC<Props> = () => {
}
```

- Or use an interface

## Hooks

- Types inferred

```typescript
interface TextNode {
  text: string
}
const [count, setCount] = useState<TextNode> ({text: 'hey'});
```

- Can also explicitly set types by passing in an interface

# [React TS cheatsheet](https://github.com/typescript-cheatsheets/react-typescript-cheatsheet#reacttypescript-cheatsheets)

- The following examples are notes from the cheatsheet

# Functional Components

2 different implementations:

```typescript
type AppProps = { message: string }
const App = ({ message }: AppProps) => <div>{ message }</div>
```

```typescript
const App: React.FC<{ message: string }> = ({ message }) => (
  <div>{ message }</div>
)
```

- The second implementation is more explicit, the differences are minimal
- Conditional rendering does not work well with the 1st implementation

# Class Components

```typescript
type myProps = {
  message: string;
}
type myState = {
  count: number;
}
class App extends React.Component<myProps, myState> {
  state: myState = {
    count: 0,
  }
  render(){
    return (
      ...
    )
  }
}
```

## Types/Interfaces

- Both are used for very similar things
- Always use `interface` for public API definitions
- Use `type` for props and state as it is more constrained
- Types are good for union types
- Interfaces are good for dictionary shapes and then using `implement` or `extend`



