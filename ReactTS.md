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