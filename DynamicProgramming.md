#  Intro

- Like the greedy method, dynamic programming is used to solve optimization problems
- With the greedy method, we make whatever choice seems best at the moment in hope that it will lead to the most optimal solution
- With dynamic programming, we try to find all possible solutions and then pick out the best solution

1. Recursion
2. Store (Memoization)
3. Bottom-up (tabular iterative solution)
 

## Fibonacci example

```python
def fib(n):
    if n <= 1:
        return 1
    return fib(n - 2) + fib(n - 1)
```

- O(2^n) time complexity
- To optimize this function, store previous function calls to avoid calling them multiple times

### Optimization

- Whenever we call a function, store its value as its index in the array (ex. fib(3) = 2, arr[3] = 2)
- Now in the fibonacci function, do not recurse if the value is already in the array (we can already have the answer)
- O(n) time complexity

### Bottom-up approach

- Using the information we have gleaned using memoization, we can write the function iteratively

```python
def fib(n):
    if n <= 1:
        return 1
    # fib numbers
    F = [0, 1]
    for i, num in enumerate(range(n + 1)):
        F[i] = F[i - 2] + F[i - 1]
    return F[n]
```

- O(n) time, O(n) space