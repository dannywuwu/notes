- A data structure where nodes/vertices are connected through edges
- No rules for connections (compared to a tree) 
- Any tree is a graph

> A graph $G$ is an ordered air of a set $V$ of vertices and a set $E$ of edges

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
