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

# Query attributes
- testing for user input recommended

## getByRole
- heading (ex. h1), button, etc

## getByLabelText
- forms

## getByPlaceholderText
## getByText
## getByTestId
- last resort

# Query Examples
- best practice to create __test__ folder in component folder
- name as Component.test.js

## `getByRole`

```js
const h1Element = screen.getByRole("heading", { name: /text between tags/i });
```

- looks for specific <tag>text in between</tag>

## `getByTestId`

```html
<h1 data-testid="header-1">100</h1>
```

```js
const h1Element = screen.getByTestId("header-1");
```

## `findBy`

```
it('find by example', async () => {
    render( <Header title="todo" />);
    const h1Element = await screen.findByText(/todo/i);
    expect(h1Element).toBeInTheDocument();
});
```

- `async` and `await` are required

## `queryBy`

```
it('query by example', () => {
    render( <Header title="todo" />);
    const h1Element = screen.queryByText(/no/i);
    expect(h1Element).not.toBeInTheDocument
});
```

## `getAllBy`

```
it('get all by example', () => {
    render( <Header title="todo" />);
    const h1Elements = screen.getAllByText(/anime/i);
    expect(h1Elements.length).toBe(9001);
});
```

# Testing components wrapped by Router

```
const MockTodoFooter = ({ numberOfIncompleteTasks }) => {
    return (
        <BrowserRouter>
          <TodoFooter 
            numberOfIncompleteTasks={numberOfIncompleteTasks}
          />
        </BrowserRouter>
    )
}

it('rendering a mock component wrapped with BrowserRouter', () => {
    render(<MockTodoFooter numberOfIncompleteTasks={5} />);
    const pElement = screen.getByText(/5 tasks left/i);
    expect(pElement).toBeInTheDocument();
});

```

# Cool Assertions

## `expect(element).toBeVisible()`
- expects element to be visible to the user
- the element can be in the document but not visible to user

## `expect(pElement).toContainHTML('p')`
- expects element to contain <p> tag

## `expect(pElement).toHaveTextContent('anime')`
- useful when getting by test id 

## `expect(pElement.textContent).toBe('manga')`
- assert values

### 1 assertion per test case
- if any assertion fails, the entire test case fails

# `not`
- negates `expect` logic
