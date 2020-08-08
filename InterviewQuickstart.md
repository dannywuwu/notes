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
{2}

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

- We have 2 indexes, a left window and right window index both starting at 0

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
- For binary trees, DFS is in the form of pre/in/post order traversal

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
        total += range_sum_bst(root.right, L, R)
    return total
```

- O(n) time, O(d) space (d is max depth)

### Check completeness of binary tree

A complete binary tree has every level except the last level completely full. If the last level is not full, all nodes are to the far left.

**Key: "level" -> level-order traversal -> BFS**

- Once we find a null, we know that the level is not complete

1. Start at the root node and place it into a queue
2. Pop it off and add its left and right children to the queue
3. Pop the next node off the queue (left in this case as it was added first, FIFO) and add its left and right children to the queue
4. Pop the next node off the queue (right in this case) and add its left and right children to the queue
5. Repeat until null is popped
6. Now check if the rest of the elements are null. If there is a non-null element, the binary tree is not complete

- O(n) time and space

### Questions

[Binary tree diameter](https://leetcode.com/problems/diameter-of-binary-tree/)

[Path sum 2](https://leetcode.com/problems/path-sum-ii/)

[Path sum 3](https://leetcode.com/problems/path-sum-iii/)

[Populate next pointers](https://leetcode.com/problems/populating-next-right-pointers-in-each-node/)

[Right side view](https://leetcode.com/problems/binary-tree-right-side-view/)

[Zigzag level traversal](https://leetcode.com/problems/binary-tree-zigzag-level-order-traversal/)

# Graphs

## DFS/BFS

- Can be used in almost all graph problems
- Can be used almost interchangeably
- BFS is good for shortest path
    - ex. Determine smallest # steps to reach end of maze:
    - DFS computes all possible paths
    - BFS expands 1 step at a time so the first time we hit the end, it uses the shortest path
- DFS is good for searching all paths in a graph from a node/exhaustive graph search
    - ex. Find best chess move, 

### Is graph bipartite - BFS

> Given a graph, return True iff it is bipartite

A graph is bipartite if we can split its nodes into 2 independent subsets A and B, such that every edge has one node A and another node B.

- Basically, no 2 neighbours can be of the same letter
- Our BFS algorithm will "colour" neighbours and make sure that they are not the same colour

1. Start at a node and colour it (I like yellow)
2. Colour the neighbours (I think purple is cool)
3. Traverse through the graph and colour more nodes!
4. If the neighbour is not coloured, colour it yellow, however if the current node is also yellow we must colour it purple
5. If the neighbour colour is the current node colour, we return False

- O(V + E) time where V represents vertices and E represents edges 
- O(V) space 

### Clone a graph - DFS

> Given a graph, return a deep copy of the graph

We want to clone every neighbour and add it recursively to our copy graph.

- We must keep track of which nodes are already cloned - hash maps
    - Set the keys as node values and the hash map values as references to the cloned node

1. Check through every node in the graph - if it is not in the hash map, add it to the clone and add it to the hash map
2. If the node is already in the hash map, add it as a neighbour to the current cloned node

- O(V + E) time where V represents vertices and E represents edges 
- O(V) space

### Questions

[Course schedule](https://leetcode.com/problems/course-schedule/)

[Find safe states](https://leetcode.com/problems/find-eventual-safe-states/)

[Max island area](https://leetcode.com/problems/max-area-of-island/)

[Water flow](https://leetcode.com/problems/pacific-atlantic-water-flow/)

[Surrounded regions](https://leetcode.com/problems/surrounded-regions/)

[Number of islands](https://leetcode.com/problems/number-of-islands/)

## Topological Sorting

- Take a directed graph and line up the nodes in a straight line (all pointers point in the same direction)
- Useful when problems involve resolving dependencies:
    - Course dependencies
    - Program build dependencies
    - Recipe steps

**Key: dependencies, prerequisites, ordered steps**

- Only applies to directed acyclic graphs (DAGs)
- DAGs can have many unique valid topological orderings
- 2 ways: 
    - DFS (simpler than BFS)
    - BFS (Kahn's algorithm)

### Course Schedule

> Given a directed graph representing courses and prerequisites, return an ordering of courses you can take to finish all the courses while satisfying all the prerequisites

> If no ordering exists, return an empty array

- Pick a node to start the DFS
- Whenever we have to backtrack from the DFS, we add a node to the beginning of the topological ordering and mark it as part of the topological ordering on the graph
    - We do not want to add the same node multiple times in the ordering
- Whenever we recurse in the DFS we add another prerequisite
- Hitting the end of a branch is basically saying: "We need to finish all the courses on the way in order to complete the end course"
- Keep performing DFS until all the nodes have been evaluated in the ordering
- In this question, if we hit a node that we have already encountered it means that there is a cycle and there are no valid topological orderings
    - Use a new hash set for each DFS
    - This is different from being marked as part of the topological ordering

- O(V + E) time
- O(V) space

### Questions

[Alien dictionary](https://www.lintcode.com/problem/alien-dictionary/description)

[Course schedule](https://leetcode.com/problems/course-schedule-ii/)

[Safe states](https://leetcode.com/problems/find-eventual-safe-states/)

[Sort respecting dependencies](https://leetcode.com/problems/sort-items-by-groups-respecting-dependencies/)


## Shortest Path Algorithms: Dijkstra's

### Dijkstra's

- Shortest path from one node to all others (main focus)

### Floyd-Warshall

- Slower than Dijkstra's but can handle negative edges

### Bellman-Ford

- Shortest paths from all nodes to all other nodes

### DFS/BFS 

- Less effective for weighted graphs
- They can still be used, but they are slower

### Network Delay Time

> A network is represented by a directed graph, where each node is a server, and each weighted edge is how many seconds a request takes to get from that server to its neighbour

> Find how long it takes for all servers in the network to receive a request from the given server; Return -1 if this is impossible.

**Dijkstra - one node to all other nodes**

- We are bounded by the server that takes the longest to receive the request
- Compute shortest path from starting node to all other servers
    - Find maximum value for these paths

1. Initialize hash map to keep track of shortest distance from start node to all other nodes (so far)
2. Also initialize a minimum heap to keep track of the shortest distances from the start node. To start, the start node has a distance of 0 and the other nodes have distances of infinity
3. Visit nodes until all are visited or the heap is emptied. Visiting a node is when we pop it off the min heap
4. The next unvisited node is the value we get when we pop off the min of the heap. Here, we start off with 0. Add the node value (shortest known distance) to the hash map by mapping it to its respective node
5. Check out the neighbours of the node we are visiting: Add the value of the current node (found in hash map) and add the weight of the edge to the neighbour and look it up in the heap
6. If this sum is smaller than the value in the heap, replace it
7. This sum represents the shortest path from the start node 
8. Pop off another value from the min heap and continue until we have visited all nodes/min heap is empty

```python
def dijkstras(graph, start_node):
    shortest_dists = {}
    shortest_path_heap = min_heap()
    shortest_path_heap.insert(0, start_node)
    
    # add nodes to heap
    for node in graph:
        if node != start_node:
            shortest_path_heap.insert(inf, node
    # end conditions        
    while (shortest_path_heap and not all_nodes_visited):
        val, node = shortest_path_heap.pop()
        visit(node, ...)
    # success - hash table full and min heap empty
    if (len(shortest_dists) == len(graph)):
        return max(shortest_dists.values())
    # the min heap is empty and the hash table is not full - there is an unreachable node from the start node
    return -1
       
        
def visit(node, val, graph, shortest_path_heap, shortest_dists):
    shortest_dists[node] = val
    for edge in graph[node]:
        new_dist = val + edge.weight
    # The find function would ideally use a hash table to look up the shortest distance for the current node
    heap_dist = find(edge.neighbor, shortest_path_heap)
    # If we find a new shortest distance, update the min heap of that node
    if new_dist < heap_dist:
        shortest_path_heap.update(edge.neighbor, new_dist)
```

- Simplified: O((V + E)logV) time
- Long answer: O(V + E + VlogV + ElogV)  time
    - Hash table: we visit each node and perform constant time lookups, but we also visit all of the node's neighbours 
    - Min heap: We pop off V nodes from the min heap which takes logV time 
        - Updating heap may occur E times
            - Heap bubbling is logV
            
- O(V) space - hash map + min heap

### Questions

[Cheapest flights](https://leetcode.com/problems/cheapest-flights-within-k-stops/)
