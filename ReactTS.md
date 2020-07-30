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

### Type Assertion

```typescript
<Text message={message as SpecialMessageType}>{ message }</Text>
```

- Assert yourself against the compiler - you definitely know that `message` can be used as a `SpecialMessageType`
- Not the same as casting; this is a method to assert dominance

## Intersection types

```typescript
export interface Props {
  label: string;
}
export const PrimaryButton = (
  props: Props & React.HTMLProps<HTMLButtonElement> // adding my Props together with the @types/react button provided props
) => <Button {...props} />;
```

- This example is dual typing - both our custom button and a native HTML button

## Inferred Types

```typescript
const [state, setState] = useState({
  hp: 100,
  mp: 50,
}); // state's type inferred to be {hp: number, mp: number}

const method = (obj: typeof state) => {
  // grabbing the type of state even though it was inferred
  setState(obj); // this works
};
```

- `typeof` is cool