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
- local brute-force

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

# MIT DP
- DP is recursion with memoization
- we write a constant amount of code to solve programs of arbitrary size
- we perform a DFS on a subproblem graph
    - origin of top down/bottom up

> What do I need to know to solve this problem?
> What choices do I make at each step?

# General Solution

## Top Down
```
def top_down(subprob, memo):
    # 1
    base case
    # 2
    if subprob in memo:
        return memo[subprob]
    # 3
    memo[subproblem] = recurse via relation
```

## Bottom Up
```
def b():
    # base B(n) = 0
    bn = 0
    # topological order
    for i = n, n-1, ..., 0:
        # relate
        b(i) = max{choice 1, choice 2}
    # original problem
    return b(0)
```

# SRTBOT
## Subproblems
- define subproblems
    - subproblems must be smaller than the original problem
## Relations
- create a recurrence relation
- define solving a problem in terms of solutions of subproblems
## Topological Order
- each choice forms a DAG
    - we can specify a topological order
> a -> b = b needs a
- a already computed
## Base Case
## Original Problem
- define in terms of subproblems
## Time
- big O

# Memoization
- reuse solutions
- maintain a dictionary mapping {subproblem -> solution}
1. recursive function returns stored solution else
2. compute and store
- we recurse down the left branch and the right is free 
    - we solve each subproblem at most once
    - therefore, ignore recurrence relation recursion time (it's free!)
## Time <= # subproblems * (relation time)
- ex. fibonacci, O(n) subproblems * O(1) addition

# Sequence problem - Bowling, LCS (multi)
## Good subproblems:
### prefixes
- x[:i]
- go from r -> l
- always look at the last letter
    - if we remove the last, we get a smaller prefix
### suffixes
- x[i:]
- go from l -> r
- always look at the 1st letter
    - if we remove the 1st, we get a smaller suffix

# Multi-Sequence - LCS
- cross product
- combine multiple inputs, 1 from each sequence

# Subproblem Constraints - LIS
## Bad Recurrence: L(i) = max{L(i+1), 1+L(i+1)}
- no constraints, are we increasing?
## Real Recurrence: L(i) = 1+max{L(j) | i<j<n, A[i] < A[j]}
- we request that LIS starts at i and the 2nd item in the LIS is j
    - we brute force j and choose the max of the choices
- 1 is because i is always in the answer
- i < j < n enforces that j is to the right of i
- A[i] < A[j] enforces an increasing subsequence

# Subproblem Expansion - Alternating Coins
## Subproblem: substrings
- x[i:j]
- we remove from left and right
