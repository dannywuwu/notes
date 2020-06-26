### `create-react-app [appname] --typescript`

# React Types

### `React.FC` - Functional component

```ts
export const Component: React.FC<{ text: string }> = () => {
}
```

- Destructure props

```ts
interface Props {
  text: string
}

Component: React.FC<Props> = () => {
}
```

- Or use an interface