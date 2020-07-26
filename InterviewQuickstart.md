Notes from the [Interview Quickstart](https://interviewquickstart.dev/) course


#  Arrays

## 2 pointers

- 2 pointers iterate through an array at the same time
- Useful for searching for pairs in a **sorted** array

### Example: Squares of a Sorted Array

> Given an array of integers sorted in non-decreasing order, return an array of the squares of each number (also sorted in non-decreasing order)

`[-4, -1, 0, 3, 10] -> [0, 1, 9, 16, 100]`

**Answer**
 
1. Have both pointers start on the absolute lowest number (in this case 0)
2. Move 1 pointer to the left, 1 pointer to the right
3. Compare both pointed values, appending the smaller squared one to the result
4. Move the pointer pointing to the lower value once again in the direction it was going in 
5. Compare once more
6. Repeat 3-5 until finished

```markdown
      *     *
[-4, -1, 0, 3, 10] -> []

  *         *
[-4, -1, 0, 3, 10] -> [1]

 *             *
[-4, -1, 0, 3, 10] -> [1, 9]

...
```

- Iterate over array once: O(n) time and O(1) space (no extra data structures)

### Questions

[Merge sorted array](https://leetcode.com/problems/merge-sorted-array/)

[2Sum 2](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/)

[3Sum](https://leetcode.com/problems/3sum/)

[Container with most water](https://leetcode.com/problems/container-with-most-water/)

[Trapping rainwater](https://leetcode.com/problems/trapping-rain-water/)

## Hash Maps

- O(1) insert/get/delete 
- Detect duplicates and count occurrences of array elements
- Reduce time complexity 

**Duplicate, Unique, # Occurences -> Hashmaps**

### Example: Two Sum

> Given an array of integers, return True if there are 2 numbers that add up to a specified target number

`[2, 7, 9] -> 16`

**Answer: Hash Set**

1. Hash the current element by `target - element`
2. If the hash exists in the set, return True
3. Else, move on to the next element

```markdown
2: is 14 in the hash set? No
{2, }

7: is  9 in the hash set? No
{2, 7}

9: is 7 in the hash set? Yes
True
```

- O(n) runtime and O(n) space

### Questions

[First unique character](https://leetcode.com/problems/first-unique-character-in-a-string/)

[Isomorphic strings](https://leetcode.com/problems/isomorphic-strings/)

[Insert/delete/random](https://leetcode.com/problems/insert-delete-getrandom-o1/)

# Strings

## Sliding Window

- Sliding window is a sub-array that slides over the main array
- Used when looking for a substring with certain properties
- The window always contains a **partial solution** to the problem
- **Consecutive**

### Example: Longest substring without repeating characters

> Given a string, find the length of the longest substring without repeating characters

- We have 2 indexes, a left window and right window index

1. Start `right_i` at the first element and add the element to a hash set
2. Increment `right_i` by 1 and add the new element to the hash set
3. `longest_len = max(longest_len, len(chars_in_window))`
4. Repeat until finding a value that is already in the hash set
5. While the repeated value is in still in the hash set, keep removing elements based on the `left_i` and increment `left_i` by 1 for each removal

```python
while string[right_i] in chars_in_window:
            chars_in_window.remove(string[left_i])
            left_i += 1
```

- Brute force takes O(n^3)
- Sliding window is O(n) runtime and O(n) space (hashmap)

### Questions

[Find all anagrams](https://leetcode.com/problems/find-all-anagrams-in-a-string/)

[Max consecutive ones](https://leetcode.com/problems/max-consecutive-ones-iii/)

[Sliding window maximum](https://leetcode.com/problems/sliding-window-maximum/)

[Minimum window substring](https://leetcode.com/problems/minimum-window-substring/)

# Linked Lists

- Recursive data structure

> If the rest of the linked list is solved, how can I use that on the current node?

### Merge 2 sorted linked lists

> Given two sorted linked lists, merge them together and return a new sorted list

```python
# Recursive solution
def merge_two_lists(l1: ListNode, l2: ListNode) -> ListNode:

    # Base case if one list is null
    if l1 is None:
        return l2
    elif l2 is None:
        return l1
    # Current node should be whichever is smaller
    if l1.val < l2.val:
        merged_list = merge_two_lists(l1.next, l2)
    else:
        merged_list = merge_two_lists(l1, l2.next)
    return merged_list
    
```

- O(m + n) time & space (new list) where m, n are the number of elements in both sorted linked lists

### Questions

[Binary to integer](https://leetcode.com/problems/convert-binary-number-in-a-linked-list-to-integer/)

[Reverse linked list](https://leetcode.com/problems/reverse-linked-list/)

[Palindrome](https://leetcode.com/problems/palindrome-linked-list/)

[Next greater node](https://leetcode.com/problems/next-greater-node-in-linked-list/)

[Add 2 numbers](https://leetcode.com/problems/add-two-numbers-ii/)

[Odd even](https://leetcode.com/problems/odd-even-linked-list/)

[Reverse nodes in k group](https://leetcode.com/problems/reverse-nodes-in-k-group/)

## Tortoise & Hare pointers

- Used to detect cycles in linked lists and graphs
- Start from the beginning, move a pointer 1 node at a time (tortoise)
- Also move a pointer 2 nodes at a time (hare)
- If the pointers meet there is a cycle

### Proof

- Let $m$ be the number of moves from the head to the cycle start
- Let $L$ be the number of nodes in the cycle
- Let $k$ be the number of nodes from cycle start

$$$
m + hL + k = 2(m + tL + k)
$$$


- Here, $t$ is the number of tortoise moves and $h$ is the number of hare moves (the hare is double the speed of the tortoise)
- There exists some value $t$, $h$, $k$ which makes the above equation true

$t = 0$, $h = m$, and $k = mL - m$

- O($L + m$) runtime, O(1) space
- Tell interviewer you've seen this before; no way you're figuring out the proof in the middle of an interview

# Binary Trees

- Recursive data structure
- Iterative solutions often involve stacks/queues

### Max depth of binary tree

> Find the number of nodes along the longest path from the root node to the farthest leaf node

Hint: Assume you have the maximum depth of the left and right subtree

``` python
def max_depth(root: Node) -> int:
    if root is None:
        return 0
    left_max_depth = max_depth(root.left)
    right_max_depth = max_depth(root.right)
    return max(left_max_depth, right_max_depth) + 1
```

- Simply take the maximum of the left/right subtrees and add 1 to account for the root node
- Base case: hitting a leaf node; max depth is 1
    - `return max(0, 0) + 1`
- O(n) runtime, visit every node once
- O(d) space, d = max depth of tree

### Validate binary search tree

> Determine if a binary tree is a valid binary search tree
- We must keep track of additional information and pass them through function calls

```python
def is_valid_bst_h(root: Node, min: int, max: int) -> bool:
    if root is None:
        return True
    # The value of all nodes in the left subtree have to be less than this node's value.
    # They also have to be greater than the current minimum from higher up in the tree.
    left_valid = is_valid_bst_h(root.left, min, root.val)
      
    # Similarly, the value of all nodes in the right subtree have to be greater than this node's value.
    # They also have to be less than the current maximum from higher up in the tree.
    right_valid = is_valid_bst_h(root.right, root.val, max)
    
    return min < root.val < max and left_valid and right_valid
    
def is_valid_bst(root: Node) -> bool:
    return is_valid_bst_h(root, -float('inf'), float('inf'))
```

- O(n) runtime, visit every node once
- O(d) space, d = max depth of tree
- Another method is to use in-order traversal and add every node value to an array
    - If the array is sorted, the BST is valid

### Questions

[Invert tree](https://leetcode.com/problems/invert-binary-tree/)

[Merge 2 trees](https://leetcode.com/problems/merge-two-binary-trees/)

[Same tree](https://leetcode.com/problems/same-tree/)

[Symmetric tree](https://leetcode.com/problems/symmetric-tree/)

[Balanced tree](https://leetcode.com/problems/balanced-binary-tree/)

[Trim tree](https://leetcode.com/problems/trim-a-binary-search-tree/)

[Lowest common ancestor](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/)

[Unique BST](https://leetcode.com/problems/unique-binary-search-trees-ii/)

[BST maximum path sum](https://leetcode.com/problems/binary-tree-maximum-path-sum/)

## DFS/BFS

- The most common binary tree algorithm

### DFS

- Searches from the root to the leaf node, 1 path at a time
- Find values that fit criteria
- Recursion

### BFS

- Level order traversal
- Uses queue/stack

### Range sum of BST

> Given a BST + min/max values, return the sum of all tree nodes with values in between min/max (inclusive)

**DFS**

- Note that we can slightly optimize where we use BST properties to know when to stop searching
    - ex. If min = 10, and we have a node of value 9, we do not need to search any nodes on the left as they will all be smaller than 9

```python
def range_sum_bst(root: Node, L: int, R: int) -> int:
    if root is None:
        return 0
    total = 0
    if L <= root.val <= R:
        total += root.val
    if L < root.val:
        total += range_sum_bst(root.left, L, R)
    if root.val < R:
        total += range_sum_bst(root.left, L, R)
    return total
```

- O(n) time, O(d) space (d is max depth)



