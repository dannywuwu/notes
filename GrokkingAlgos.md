# Binary Search

- `log(n)` searching for sorted arrays
- Every iteration, we halve the search space
- Every time, we check the middle element
    - If the guess is too low, we update `low`
    - If the guess is too high, we update `high`

>  Suppose you have a sorted list of 128 names, and you’re searching through it using binary search. What’s the maximum number of steps it would take? 

- $\log_{2}128 = 7$ steps 

> Suppose you double the size of the list. What’s the maximum number of steps now?

- Doubling the size of the list increases the number of steps by 1

# Travelling Salesperson

- You have a salesperson
- The salesperson needs to go to `n` cities while traveling the minimum distance
    - Look at every possible order in which they should travel to the cities
- This ends up being `O(n!)` time 

