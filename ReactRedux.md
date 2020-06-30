### `npm install redux react-redux`

![Redux Diagram](https://miro.medium.com/max/4210/1*q0zyAUFV5LMNdM42pNJGkw.png)

- Have central storage for data 
- Passing around props is bad

1. Define central store with redux 
2. A component subscribes to changes in data; Redux passes data using props

### To make a change:

1. Dispatch action
2. Actions describe changes with data payload
3. Action passed to Reducer
4. Reducer updates data store

## Store 

- Holds all data/state for the application
- Globalized state

```js
import { createStore } from 'redux';

const store = createStore(rootReducer);
```

## Dispatch

- Execute the action to the reducer

```js
const dispatch = useDispatch();

<Button title="+" onPress={() => dispatch(() => plus(5)}></Button>
```

## Action

- Describe what we want to do

```js
export const plus = (num) => {
    return {
        type: 'INCREMENT',
        payload: num 
    }
}
```

- In this example, `num` is 5

## Reducer

- Describe how actions transform state
- Based on the action, we modify the store

```js
const countReducer = (state = 0, action){
  switch(action.type){
    case: 'INCREMENT':
        return state + action.payload;
    case 'DECREMENT':
        return state - action.payload;
  }
}
```

- `state = 0` describes initial state

## `useSelector()`

- Extract data from Redux state using a selector function

```js
// if using a rootReducer
const countReducer = useSelector(state => state.count);
```

- In this example, we accessed the state (root reducer) and retrieved the count reducer from it where `count: countReducer`
