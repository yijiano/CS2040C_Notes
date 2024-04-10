[[_main|<-- Back to main]]
# Terminology
#graphs #nodes #edges #diagraphs
**Graph G = <V, E>**

**V** is a set of nodes:
- At least one node: $|V| > 0$

**E** is a set of edges:
- E $\subseteq$ { (v, w): (v $\in$ V), (w $\in$ V) } 
- **Not reflexive (no self-loops):** e = (v ,w), for v $\neq$ w
	- Order matters for #directed_graphs
- **Only one edge for each pair of nodes:** For all $e_1$, $e_2$ $\subseteq$ E : $e_1 \neq e_2$

Connected
- Every pair of nodes is a connected by a path, only one components

Disconnected:
- Some pair of nodes is not connected by a path, multiple connected components

Degree of a **node**:
- Number of **adjacent** edges

Degree of a **graph**:
- Maximum number of **adjacent** edges
- #directed_graphs 
	- In-degree: number of incoming edges
	- Out-degree: number of outgoing edges

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
- Edges: **linked list** per node
	- only **out-going edges** for #directed_graphs

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

# Graph Search
#graphs #graph_search
## BFS (Queue)
#bfs #queue
- Add start node to queue
- Repeat until queue is empty
	- Remove node v from the front of the queue.
	- Visit v.
	- Explore all outgoing edges of v.
	- Add all unvisited neighbours of v to the queue.

## DFS (Stack)
#dfs #stack
- Add start node to stack
- Repeat until stack is empty
	- Pop node v from the front of the stack.
	- Visit v.
	- Explore all outgoing edges of v.
	- Push all unvisited neighbours of v on the top of the stack.

# Breadth-First Search
#bfs
## Characteristics
- Explore level by level
- **Frontier:** current level
- Initially: {s}
- Advance **frontier**, never backtrack
	- For #directed_graph follow outgoing, ignore incoming
- Calculate level (i) from level (i - 1)
- Skip already visited nodes
- BFS fails to visit every node in a disconnected graph (more than one component)

```cpp
// O(V + E) runtime
BFS(Node[] nodeList, int startId) {
	bool visited[numNode] = {0};
	int parent[numNode];
	for (int i = 0; i < numNode; i++) { // no parent yet
		parent[i] = -1; 
	}
	
	for (int start = 0; start < numNode; start++) {
		// to account for disconnected graphs
		if (!visited[start]) {
			Set<int> frontier = new Set<int>;
			frontier.insert(startId);
			visited[startId] = true;
			
			// main code
			while (!frontier.isEmpty()) {
				Set<int> nextFrontier = new Set<int>;
				while (!frontier.isEmpty()) {
					>>extract a vertex v from fontier<<
				for (w = every neighbour of v) {
						if (!visited[w]) {
							visited [w] = true;
							parent[w] = v;
							nextFrontier.add(w);
						}
					}
				}
				frontier = nextFrontier;
			}	
		}
	}
}
```
# Depth-First Search
#dfs
## Characteristics
- Follow path until stuck
	- For #directed_graphs follow outgoing edges
- Backtrack until reach unexplored neighbour
	- For #directed_graphs backtrack through incoming edges
- Recursively explore

```cpp
DFS-visit (Node[] nodeList, boolean[] visited, int startId) { 
	for every neighbor v of startId { 
		if (!visited[v]){ 
			visited[v] = true; 
			DFS-visit(nodeList, visited, v); 
		} 
	} 
}

DFS (Node[] nodeList) {
	boolean visited [numNode] = {0};
	
	for (start = 0; start<nodeList.length; start++) {
		if (!visited[start]) {
			visited[start] = true;
			DFS-visit(nodeList, visited, start);
		}
	}
}
```