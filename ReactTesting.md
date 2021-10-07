[Net Ninja React Testing Tutorial](https://github.com/harblaith7/React-Testing-Library-Net-Ninja)

# Test Structure

```jsx
import { render, screen } from '@testing-library/react';
import App from './App';

test('describes what is being tested (name of test)', () => {
  // render component to test
  render(<App />);
  // find elements to interact with
  // `screen` looks into DOM
  const linkElement = screen.getByText(/learn react/i);
  // assert with `expect` (part of Jest testing library)
  expect(linkElement).toBeInTheDocument();
});
```

- `it` is an alias of the `test` function

# Query Methods

## getBy, findBy, queryBy
- only returns 1 element
- error on multiple matches

### getBy
- general use

### findBy
- used with async await

### queryBy
- does not error on no match, returns null
- used for finding lack of existence of elements

## getAllBy, findAllBy, queryAllBy
- returns list of elements

