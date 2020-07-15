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