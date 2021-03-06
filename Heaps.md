# Heap

- Keeps quantities in gradual increasing/decreasing order
    - Starting from the bottom, a min heap's elements decrease as you go up; a max heap's elements increase as you go up
- A data structure that implements the Priority Queue ADT
    - An ADT (Abstract Data Type) is defined by its behaviour (its methods)

### A PQ implements:
    
- `isEmpty()`
- `insertWithPriority()`
- `pullHighestPriorityElement()`
- `peek()` (which is basically `findMax()` or` findMin()`)

Min heap: a min element can be peeked in O(1) time
Max heap: a max element can be peeked in O(1) time

- A binary heap is a complete binary tree with the root holding the min/max value
    - The heap can be implemented with nodes or with an array

```python
arr[(i - 1)//2] # Access parent node
arr[2*i + 1] # Access left child
arr[2*i + 2] # Access right child
```

**In the examples below, we are using a min heap**

## Insertion - Heapify Upwards

1. Insert at the end of the tree to satisfy complete property and "bubble" the node upwards to its correct spot
2. Compare the inserted node to its parent - if the node is smaller than its parent, swap them
3. Repeat comparisons until the inserted node is in its correct position

## Removal - Heapify Downwards

1. Remove the root and replace it with the bottom-right node
2. Since we have a min heap, we bubble down through the root child's smaller element (swap replaced root with smaller child)
3. Bubble downwards, swapping the replacement node with its smaller child until the node is in its correct position

### Note: If the left node does not exist, by definition of complete binary tree we know the right node does not exist either

## The farthest we can swap downwards/upwards is the height of the tree - If a tree has `2^n` nodes, its height is `logn`

### `O(1)` peek, `O(logn)` insertion/removal

# Python `heapq` module

- Implements heap operations on lists as a **min heap**
    - If we need a max heap, we can reverse the order (ex. use negative numbers)

```python
>>> import heapq
>>> a = [3, 5, 1, 2, 6, 8, 7]
>>> heapq.heapify(a)
>>> a
[1, 2, 3, 5, 6, 8, 7]

```

### `.heappop()`, `.heappush()`

```python
>>> a = [2, 5, 3, 7, 6, 8]
>>> heapq.heappush(a, 4)
>>> a
[2, 5, 3, 7, 6, 8, 4]
>>> heapq.heappop(a)
2
>>> heapq.heappop(a)
3
>>> heapq.heappop(a)
4
```

- Insertion/removal while preserving the heap property

### `.heapreplace()`: equivalent to `heappop()` followed by `heappush()`

### `.merge()`: merges sorted input iterables 

- Returns an iterator, not a list

### `.nsmallest(n, iterable, key)`

- `n` indicates how many elements to return.
- `iterable` identifies the elements or dataset to compare.
- `key` is a callable function that determines how elements are compared.

  