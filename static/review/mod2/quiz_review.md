Module 2 Quiz Review
------

## Graph basics
### Graph definition
- A set of vertices $V$
- A set of edges $E$
    - Each edge takes the form $(a, b)$ if $G$ is directed
    - ...or $\{a, b\}$ if $G$ is nondirected

### Graph representation
- Adjacency list:
    - Maintain a list of vertices; each vertex's list maintains a list of out-neighbors
- Adjacency matrix:
    - Maintain 2-d V x V array of vertices
    - Each entry in the vertex corresponds to a weight (if weighted) or just a binary "edge", "no edge" between vertices a and b. I.e., $M[a][b] \neq 0 \iff (a, b) \in E$ 

### Graph terms
- Vertex (pl. vertices) or node
- Edge
    - An vertex is "incident" to an edge if it is one of the vertices connected by that edge
- Dense graph
    - One with many edges
    - A *maximally dense* undirected graph has $\frac{1}{2}v(v-1)$ edges.
    - Maximally dense directed graph: $v(v-1)$ edges.
- Path
    - Sequence of vertices each reachable from the last
    - *Simple path*: a path that has no repeat vertices
- Connectedness
    - Undirected setting: every node is reachable from every other node
    - Directed setting:
        - Weakly connected: every pair of vertices is connected by some edges, even if we have to traverse in the wrong direction
        - Strongly connected: $\forall (u, v) \in V^2 \text{ s.t. } u \neq v : v \text{ reachable from } u$

## BFS
- One algorithm for graph **traversal:** an algorithm that visits each vertex in some organized fashion while following edges

### BFS strategy
- Pick a starting vertex $s$, set distance $s.d = 0$.
- Put $s$ on a queue.
- While queue is nonempty:
    - Pop $v$ off the queue.
    - Mark $v$ as visited.
    - For each $n$ of $v$'s (out)neighbors:
        - Put $n$ on the queue.
        - Set $n.d = v.d + 1$

BFS constructs a breadth-first-search tree of vertices while it operates. 

- The root of the tree is the start node, and each child is $d$ steps farther from $s$ on the shortest path. ($d$ is our dist value, but also the depth of the node in the tree.)

### BFS complexity
Time complexity: $\Theta(V+E)$ (graph linear time)

Space complexity: $\Theta(V)$ (needs to allocate structure for each vertex to store distance and potentially parent node)

## Kruskal's and Prim's MST algorithms
A minimum spanning tree of $G$ is the subgraph of $G$ that:
- Has the minimum sum of edge weights
- Is a tree (i.e., has no cycles)

Spanning trees are not necessarily unique

### Kruskal's strategy
Start with a forest of single-node trees, and...

**Idea:** repeatedly find the smallest-weight edge that joins two distinct trees 

In practice:
- Create a find-union data structure. Each node is its own tree.
- Toss all of the edges into a priority queue (minheap).
- While priority queue is nonempty: 
    - Pop an edge $e$ off the queue.
    - If $e$ joins two distinct trees in the forest, then we include it in the MST.
        - Update the vertices it joins to become part of the same tree. (This is accomplished by the Find-Union data structure.)

To process the edges by ascending weight, we can use a priority queue or simply sort the edges before starting.

#### Optimizing with Find-Union
Naively, `find` and `union` are both linear.

##### Union-by-rank
- One optimization for Find-Union data structure
- Stores "rank," an upper-bound for the height of that tree
    - Height defines how many traversals we'll have to do, so always pointing to the higher-rank tree ensures we won't accidentally increase the height of the tree, except when we have to 

##### Path compression
- Whenever we do a `find` operation, store the set label we eventually ended up finding, and make the pointer direct.
    - Means that the complexity of find becomes $O(1)$ amortized.

### Updated runtime
Union-by-rank and path compression take us from linear `find` and `union` to approximately constant `find` and `union`. 

Our overall runtime:
$$
    \Theta(ElogE + E * (1)) = \Theta(ElogE) = \Theta(ElogV)
$$
