## `is` and `==`

- `is` compares equality

- `==` compares identity

- ex. 2 cats: cat `==` cat, however using `is` they are "different cats"

## `len`

```python
len("Hello") #5
len([1, 2, 6, 3, 4]) #5
sorted([5, 4, 3, 2, 1]) #[1, 2, 3, 4, 5]
sorted(["C", "B", "a", str(3), str(1)]) #['1', '3', 'B', 'C', 'a']
```

## `pass`

- Write a function implementation in the future; Avoid compilation errors
- Ignore `if` implementation


# Functions

- `snake_case`

```python
def function_a(str1 = "hello"):
    print(str1)
    print("there")

function_a("hi") #hi\nthere
function_a() #hello\nthere

def print_name(first, last):
    print("First:", first, "Last:", last)

print_name(last = "w", first = "d") #First: d Last: w 
```
```python
# * denotes a list/array
def print_people(*people):
    for person in people:
        print("Name:", person)
  
print_people('a', 'b', 'c', 'd') # Name: 'a' / Name: 'b'...
```

# Classes

```python
class Pokemon
    
    def __init__(self, health, atk):
        self.hp = health
        self.atk = atk
    
    def getStats:
        print(self.hp)
        print(self.atk)
        
Pokemon pikachu(100, 50)
pikachu.getStats() # 100 / 50
```

# File IO

```python
# 'w+' is for writing to file
newfile = open("test.txt", "w+")

string = "The quick brown fox jumps over the lazy dog"

newfile.write(string)
```

- Writing to a file

# Parsing JSON

```python
import json
import os

# if file exists and file is not empty
if os.path.isfile("./test.json") and os.stat("./test.json").st_size != 0:
# open file to read
file_text = open("./test.json", "r+")
data = json.loads(file_text.read()) # returns a Python Dictionary
```

### `json.loads()`

- Returns a dictionary object from a JSON file

### `json.dumps()`

- Returns a JSON string from a dictionary object


# Requests

- `pip install requests`

```python
import requests

r = requests.get("url")

'''
r.url - url
r.text - html
r.status_code - http code
'''
```

# Advanced Topics

## Iterators

An iterator object must implement `__iter__()` and `__next__()`

- These 2 functions can be called through `iter(obj)` and `next(obj)`
- `iter(obj)` returns an iterator from the passed in `obj`
- `next(obj)` is used to manually iterate through all items of an iterator
    - Reaching the end raises the `StopIteration` exception
    - For loops on iterators are actually infinite while loops of `next()` calls until `StopIteration` is raised
    - Accepts an optional 2nd argument ex. `next(obj, 1)` which in this example returns `1` upon `StopIteration`

## Generators

Generators are functions that return iterator objects 

- To create a generator, define a normal function with a `yield` statement instead of a `return` statement
- `yield` pauses the function and saves its state, continuing on successive calls

[Examples](https://www.programiz.com/python-programming/generator)

**Usage**

- Memory friendly implementation of sequences - produces one item at a time
    - Good for infinite streams

## Decorators

Decorators takes a function and adds some functionality

```python
def make_pretty(func):
    def inner():
        print("I got decorated")
        func()
    return inner

def ordinary():
    print("I am ordinary")
    
pretty = make_pretty(ordinary)
pretty()
# I got decorated
# I am ordinary
```

```python
@make_pretty
def ordinary():
    print("I am ordinary")
# Equivalent statements  
def ordinary():
    print("I am ordinary")
ordinary = make_pretty(ordinary)
```

- `@` syntactic sugar