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