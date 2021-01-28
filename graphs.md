- A data structure where nodes/vertices are connected through edges
- No rules for connections (compared to a tree) 
- Any tree is a graph

> A graph $G$ is an ordered pair of a set $V$ of vertices and a set $E$ of edges

$$$
G = (V, E)
$$$

## Edges

- Identified by 2 endpoints as a pair
- 2 types: directed/undirected

## Directed/Undirected graphs

- 2 types of graphs

**Directed**

- Edges are uni-directional/ordered pairs

**Undirected**

- Edges are bi-directional/unordered pairs

> ex. xy and yx are the same edge, hence they only appear once in E

> So if E = {xy, wz, yx}, it is actually just {xy, wz} and the graph only has 2 edges

## Weights

- Can assign "weights" to different paths which prioritize connections over others 
- Unweighted graphs have all edges with the same weight

## Examples

- Graphs can represent any collection of objects having some kind of pairwise relationship

### Social network

- Undirected graph
    - Friendship is a mutual relationship (2 way)
- Users are nodes and friendship is an edge connecting them

### Webpages

- Directed graph
    - Webpages are nodes, links to another page are edges

# Graph implementations

1. Adjacency matrix
2. Adjacency list

## Adjacency Matrix

- A `V x V ` square matrix (2D array)
- `V` is the number of vertices of the graph
- If `mat[i][j] = 1`, there is an edge between the `i` and `j` vertices
- For weighted graphs, `mat[i][j] = weight`
- O(n^2) space, O(1) time to find if an edge exists between 2 vertices

> How many vertices are adjacent to some vertex V?

## Adjacency List

- An array of lists
- Let `A` represent a graph
    - `A[i]` is a list with all vertices adjacent to `i`
- O(V + E) space, O(V) time to find if an edge exists between 2 vertices

> Find all vertices adjacent to V

- Any algorithm where you need to always operate on every neighbour of a vertex on a graph, an adjacency list may be better


### Time: Matrix > List

### Space: List > Matrix

# [BFS/DFS](https://www.youtube.com/watch?v=TIbUeeksXcI)

- We search **RELATIONSHIPS**

## DFS (Deep)

- Stack, whether our own or the call stack with recursion (LIFO)
- Uses: backtracking, complete search, exhausting possible paths

1. Pull a node
2. Process the node
3. Add the node's children

```python
from collections import deque

def dfs_print(start):
    stack = deque()
    seen = set()
    # add start to search
    stack.append(start)
    
    while !stack.empty():
        # pull node
        cur_node = stack.pop()
        # process if not seen
        if cur_node not in seen:
            seen.add(cur_node)
            print(cur_node)
        # add unseen children
        for adjacent in cur_node.adjacents:
            if adjacent not in seen:
                stack.append(adjacent)
```

- O(|V| + |E|) time, O(|V|) size

## BFS (Wide)

- Iterative with queue (FIFO)
- Uses: Check if path exists between nodes, distance out, levels
- Goes layer by layer 

The implementation is exactly the same as DFS, but uses a queue

```python
from collections import deque

def dfs_print(start):
    queue = deque()
    seen = set()
    
    queue.append(start)
    while !queue.empty:
        # pull node
        cur_node = queue.popleft()
        # process node
        if cur_node not in seen:
            seen.add(cur_node)
            print(cur_node)
        # add node's children
        for adjacent in cur_node.adjacents:
            if adjacent not in seen:
                queue.add(adjacent)
```

- O(|V| + |E|) time, O(|V|) size

# Topological Sort

- Linearly sort nodes in graph in the order the edges point

### Prerequisites

- The graph must be acyclic
- The graph must be directed

#  [Dijkstra Algorithm ](https://www.youtube.com/watch?v=XB4MIexjvY0)

- Single source shortest path (minimization problem)
- Greedy method

If a weighted graph is given, then we have to find the shortest path from some starting vertex to all of the vertices.

- The Dijkstra algorithm provides a procedure for getting an optimal solution that is the minimum result (shortest path)
- Works on directed/non-directed graphs

## Relaxation

- Say we have 2 points, `u` and `v`
- If the distance of `u` + the cost of `u` and `v` is smaller than the distance of `v`, replace the distance of `v` with the expression above

```python
if d[u] + c(u, v) < d[v]:
    d[v] = d[u] + c(u, v)
```

## Procedure

1. Setup: Choose a starting node, and label distances to other direct vertices (vertices touching the starting node) - the distance is the weight of the direction. Any indirect vertices are given a distance of infinity
2. Repeating steps: Select the shortest path and perform edge relaxation on the node's neighbours
3. With relaxation, we want to replace the larger distances with their proper values (`d[u] + c(u, v)`)

### Analysis

`n = |V| `

- `n` is the number of vertices
- O(n^2) time (we inspect every vertex, and in the worst case all vertices are connected and we perform n operations for every vertex)

## Drawbacks

- Dijkstra's algorithm can give the wrong answer when dealing with negative weightings

