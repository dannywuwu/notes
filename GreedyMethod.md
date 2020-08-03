- If a problem requires a minimum/maximum result, it is an optimization problem
- Feasible solutions to the problem are solutions which satisfy a constraint
- The optimal solution satisfies the objective of the problem
- There is only one optimal solution, however there may be multiple feasible solutions

The greedy method is used to solve optimization problems 

- The method says that problems should be solved in stages
- Each stage, we consider an input for a given problem and that input is feasible, we can include it in the solution

ex. general method:

```
for n in arr:
    if Feasible(n):
        solution += n
```

The greedy approach is where you have your own method of selection, and based on that selection method you get a result which is the "best" result
