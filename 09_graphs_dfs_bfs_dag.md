[[_main|<-- Back to main]]
# Terminology
#graphs #nodes #edges
**Graph G = <V, E>**

**V** is a set of nodes:
- At least one node: $|V| > 0$

**E** is a set of edges:
- E $\subseteq$ { (v, w): (v $\in$ V), (w $\in$ V) } 
- **Not reflexive (no self-loops):** e = (v ,w), for v $\neq$ w
- **Only one edge for each pair of nodes:** For all $e_1$, $e_2$ $\subseteq$ E : $e_1 \neq e_2$

Connected
- Every pair of nodes is a connected by a path

Degree of a **node**:
- Number of **adjacent** edges

Degree of a **graph**:
- Maximum number of **adjacent** edges

Diameter:
- Maximum distance between two nodes, following the **shortest** path

Special Graphs:

|   Type    |                     Description                     |    Diameter     | Degree |
| :-------: | :-------------------------------------------------: | :-------------: | :----: |
|   Star    | One central node, all edges connect center to edges |        2        | n - 1  |
|  Clique   |            All pairs connected by edges             |        1        | n - 1  |
| Line/Path |                  Straight up line                   |      n - 1      |   2    |
|   Cycle   |                        Cycle                        | n / 2 OR n/2 -1 |   2    |
# Representing a Graph
#graphs #nodes #edges #array #linked_list

Graph consists of:
- Nodes: stored in an **array**
- Edges: **linked list** per nod

Key questions to ask:
- Space usage: is graph dense or sparse?
- Queries: what type of queries do I need?
	- Enumerate neighbours?
	- Query relationship?

Trade-offs
- Adjacency Matrix:
	- Fast query: Are v and w neighbours?
	- Slow query: Find me any neighbour of v.
	- Slow query: Enumerate all neighbours
- Adjacency List:
	- Slower query: Are v and w neighbours?
	- Fast query: Find me any neighbour of v.
	- Fast query: Enumerate all neighbours

If graph is dense (|E| = O($V^2$) then use an adjacency matrix; else use an adjacency list.
## Adjacency List
#adjacency_list
Memory usage for graph G = (V, E):
- array size of |V|
- linked lists of size |E|
- Total: O(V + E)
- For a cycle: E = O(V)

```cpp
class Node {
	int key;
	LinkedList<int>;
}

class Graph {
	Node nodeList[MAXNODE];
}
```
## Adjacency Matrix
#adjacency_matrix
Memory usage for graph G = (V, E):
- array size of |V| * |V|
- Total: O($V^2$)
- For a cycle: E = O($V^2$)

|       | **a** | **b** | **c** | **d** | **e** | **f** |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| **a** |   0   |   0   |   0   |   0   | **1** | **1** |
| **b** |   0   |   0   | **1** | **1** | **1** |   0   |
| **c** |   0   | **1** |   0   |   0   |   0   |   0   |
| **d** |   0   | **1** |   0   |   0   |   0   |   0   |
| **e** | **1** | **1** |   0   |   0   |   0   |   0   |
| **f** | **1** |   0   |   0   |   0   |   0   |   0   |
Graph is represented as **A(v)(w) = 1 iff (v, w) $\subseteq$ E**

Neat property: $A^2$ = length 2 paths

To find out if c and d are 2-hop neighbours:
- Let $B = A^2$
- B[c, d] = A[c, .] $\cdot$ A[., d] > 0 ? 1 : 0
- B[c, d] = 1 iff A[c, x] == A[x, d] for some x.

```cpp
class Graph {
	bool[][] m_adjMatrix;
}

class Graph {
	Node[][] m_adjMatrix;
}
```

# Breadth-First Search
