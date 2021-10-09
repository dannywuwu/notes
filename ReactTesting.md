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
    const element = screen.getByText(/5 tasks left/i);
    expect(element).toBeInTheDocument();
});

```

# Cool Assertions

## `expect(element).toBeVisible()`
- expects element to be visible to the user
- the element can be in the document but not visible to user

## `expect(element).toContainHTML('p')`
- expects element to contain <p> tag

## `expect(element).toHaveTextContent('anime')`
- useful when getting by test id 

## `expect(element.textContent).toBe('manga')`
- assert values

### 1 assertion per test case
- if any assertion fails, the entire test case fails

# `not`
- negates `expect` logic

# Describe Blocks
- group common tests
- can nest blocks

```
describe('cool tests only', () => {
    if('cool test 1', () => {
        ...
    }

    if('cool test 2', () => {
        ...
    }
})
```

# Mock Functions
- used when a component is passed a function as a prop

```
const mockedSetTodo = jest.fn();

it('mock function test', () => {
    render(<AddInput fruitList={[]} setFruits={fruits} />);
});
```

# Testing Events

## input

```
it('fire input test', () => {
    render(<AddInput fruitList={[]} setFruits={fruits} />);
    const inputElement = screen.getByPlaceholderText(/Add a new fruit here.../i);
    fireEvent.click(inputElement)
    fireEvent.change(inputElement, { target: { value: "Orange" } })
    expect(inputElement.value).toBe("Orange");
});
```

## click

```
it('button click test', () => {
    ...
    const buttonElement = screen.getByRole("button", { name: /Add/i});
    fireEvent.click(buttonElement)
});
```

# Integration Tests
- testing multiple components
- we test the parent component

```
const addTask = (tasks) => {
    const inputElement = screen.getByPlaceholderText(/Add a new task here.../i);
    const buttonElement = screen.getByRole("button", { name: /Add/i} );
    tasks.forEach((task) => {
        fireEvent.change(inputElement, { target: { value: task } });
        fireEvent.click(buttonElement);
    })
}
```

- bundle repetitive test code into functions

```
it('should render multiple items', () => {
    render( <MockTodo />);
    addTask(["task 1", "task 2", "task 3"])
    const divElements = screen.getAllByTestId("task-container");
    expect(divElements.length).toBe(3)
});
```

- can have multiple elements with same test id

# [Mocking Requests](https://jestjs.io/docs/manual-mocks)
- found in the __mocks__/ directory directly adjacent to node_modules/
- naming and location is important

### `screen.debug`

## ex. mocking axios
- src/__mocks__/axios.js

```
const mockResponse = {
    data: {
        results: [
            {
                name: {
                    first: "Shinichi",
                    last: "Akiyama"
                },
                login: {
                    username: "kanzakinao"
                }
            }
        ]
    }
}


export default {
    get: jest.fn().mockResolvedValue(mockResponse)
}
```
