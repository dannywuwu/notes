# Chapter 1 - Intro

## Binary Search

- `log(n)` searching for sorted arrays
- Every iteration, we halve the search space
- Every time, we check the middle element
    - If the guess is too low, we update `low`
    - If the guess is too high, we update `high`

>  Suppose you have a sorted list of 128 names, and you’re searching through it using binary search. What’s the maximum number of steps it would take? 

- $\log_{2}128 = 7$ steps 

> Suppose you double the size of the list. What’s the maximum number of steps now?

- Doubling the size of the list increases the number of steps by 1

## Travelling Salesperson

- You have a salesperson
- The salesperson needs to go to `n` cities while traveling the minimum distance
    - Look at every possible order in which they should travel to the cities
- This ends up being `O(n!)` time 

# Chapter 2 - Arrays & Linked Lists

### Reading: Arrays

- Instant random access
- You must iterate through a full linked list to find elements

### Inserting/Deleting: Linked Lists > Arrays

- All you need to do is change pointers around
- For arrays you have to shift the other elements down

> People sign up for Facebook pretty often, too. Suppose you decided to use an array to store the list of users. What are the downsides of an array for inserts? In particular, suppose you’re using binary search to search for logins. What happens when you add new users to an array?

- Adding new users will shift the elements down, which costs `O(n)` time 

>  Let’s consider a hybrid data structure: an array of linked lists. You have an array with 26 slots. Each slot points to a linked list. For example, the first slot in the array points to a linked list containing all the usernames starting with a. The second slot points to a linked list containing all the usernames starting with b, and so on.
>  Compare this hybrid data structure to arrays and linked lists. Is it slower or faster than each for searching and inserting? 

- This hybrid data structure optimizes linked list insertion of usernames
    - Instead of searching through the linked list to find the correct letter to insert the usernames in, we can instantly access the letter
- `O(n) -> O(1)` insert

## Selection Sort

> Q: Sort an array from lowest to highest

- Go through each element of the array and find the lowest value
- Add the lowest value to a new array
- `O(n^2)` time, `O(n)` space

# Recursion

- When a function calls itself
- Every recursive function has 2 parts:

1. Base case
        - The function stops
        
1. Recursive case
        - The function calls itself

## The call stack

> What happens when you call a function?

- Your computer allocates a box of memory for that function call
- Every time we make a function call, your computer saves variable values in each call's respective memory boxes
- These boxes are placed on a **stack**
    - When the top function returns from its call, its box is popped off
- We use this to our advantage with recursion

**When you call a function from another function, the calling function is paused in a partially completed state**

- All variable values for that function are still stored in memory

**Every function has its own state**

However, saving function info takes memory

- We can use loops instead
- Or use *tail recursion*

# Divide and Conquer

A way to think about a problem recursively

1. Figure out a simple case as the base case
2. Figure out how to reduce the problem to get to the base case

ex. With an array, the base case is often an empty array/an array with one element


## Quicksort

- Uses divide & conquer

### Base Cases

- Already sorted: empty arrays, arrays with 1 element
- An array of 2 elements just needs a swap if they are out of order
- Using D&C, we want to break down arrays until they are at the base case

## Steps

1. Pick a pivot (random for now)
2. Find elements smaller than pivot and elements larger than pivot, and partition them into 2 subarrays
3. We now have:
    - A subarray of numbers less than pivot
    - The pivot
    - A sub-array of numbers greater than the pivot
4. Call quicksort on the subarrays
    - If the sub-arrays are sorted, we can simply combine everything for the sorted array
    - `qsort(left array) + pivot + qsort(right array)`

