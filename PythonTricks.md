## Alphanumeric elements only

```python
import re

re.sub(r'\W+', '', string)
```

- Sub all non-alphanumeric elements `\W` with `''`

## Find most common element in list
```python
import statistics 
from statistics import mode 

List = [2, 1, 2, 2, 1, 3] 
print(mode(List))

# 2 
```

## Convert String to List

```python
list(string)
```

##  Iterate through 2 lists at once

```python
a = [1, 3, 5]
b = [2, 4, 6]

for num1, num2 in zip(a, b):
    print(num1),
    print(num2)
# 1 2 3 4 5 6
```

# Stacks

### `.append()`

- Add new elements to the top of the stack

### `.pop()`

- Remove elements in LIFO order

## List implementation

- Speed issues once large
- `lists` are stored to provide fast access to random elements
- Elements stored next to each other (Python knows exactly where to look in memory to find it)
- Amortized constant time - if the stack grows bigger than the block of memory, Python does memory allocations

##  Deque implementation

```python
From collections import deque

theStack = deque()
```

- Implemented with Double Linked Lists
- Constant time addition + removal of entries
- Random indexing is slower, but that is not what we use a stack for

### Peeking a deque

```python
q = deque()
q.append(1)
q.append(2)
q.append(3)

q[0] # 1
q[-1] # 3
```

- Just like an array

# Slice Notation

```python
a[start:stop]  # items start through stop-1
a[start:]      # items start through the rest of the array
a[:stop]       # items from the beginning through stop-1
a[:]           # a copy of the whole array
```

```python
a[start:stop:step] # start through not past stop, by step
a[slice(start, stop, step)] # equivalent slice code
```

- `:stop` is not inclusive!

```python
a[-1]    # last item in the array
a[-2:]   # last two items in the array
a[:-2]   # everything except the last two items
```

```python
a[::-1]    # all items in the array, reversed
a[1::-1]   # the first two items, reversed
a[:-3:-1]  # the last two items, reversed
a[-3::-1]  # everything except the last two items, reversed
```

- These values can also be negative

