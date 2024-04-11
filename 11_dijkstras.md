#dijkstra #sssp #shortest_path 

[[_main|<-- Back to main]]

# Basic Idea
- **Assumptions**
	- **No negative weights!**
- Initialise:
	- Put all vertices into a priority queue
	- Set all priorities to estimated distances as infinity
	- Set the starting vertex estimated distance as 0
- Repeat until the priority queue is empty
	- Extract the vertex v in the priority queue with the shortest estimated distance
	- Relax all the neighbours of v in the priority queue and update their estimated distance

# Priority Queue
#priority_queue
In this case, its a min heap
```cpp
void insert(Key k, Priority p);
Data extractMin();
void decreaseKey(Keyy k, Prioirity p);
bool contains(Key k);
bool isempty();
```

# Pseudo Code
#dijkstra 
```cpp
// O(E log V)
relax(Edge e) {
	int v = e.from();
	int w = e.to();
	double weight = e.weight();
	if (distTo[w] > distTo[v] + weight) {
	distTo[w] = distTo[v] + weight;
	parent[w] = v;
	queue.decreaseKey(w, distTo[w])
	}
}
```

# Performance

| PQ Implementation | insert | deleteMin | decreaseKey |     Total      |
| :---------------: | :----: | :-------: | :---------: | :------------: |
|       Array       |   1    |     V     |      1      |    O($V^2$)    |
|     AVL Tree      | log V  |   log V   |    log V    |   O(E log V)   |
|    d-way Heap     | dlogdV |  dlogdV   |    logdV    | O(Elog(E/V)V)  |
|  Fibonacci Heap   |   1    |   log V   |      1      | O(E + V log V) |
# Implementation
```cpp
#include "graph.h"
#include "shortest_path.h"
#include "heap.hpp"
#include "graph.cpp"

Path shortestPath(const Graph& g, int source, int dest) {
  // given graph g, Dijkstra's the paths to find shortestPath
  Heap<GraphEdge> heap;
  vector<int> dist_to; //from source to each of the dest
  vector<int> shortest_path; //from source to dest
  vector<int> result_path; //best way to from source to dest
  for (int i = 0; i < g.num_vertices(); i++) {
    dist_to.push_back(-999); //just a very (small)big number
    shortest_path.push_back(-1);
  }
  int current = source;
  forward_list<GraphEdge> neighbours;
  GraphEdge to_insert;
  int weight;
  int destination;
  while (current != dest) {
    neighbours = g.edges_from(current);
    while (!neighbours.empty()) {
      to_insert = neighbours.front();
      neighbours.pop_front();
      weight = -1 * to_insert.weight();
      destination = to_insert.dest();
      if (current == source) {
        dist_to[destination] = weight;
        shortest_path[destination] = current;
        heap.insert(GraphEdge(destination, -1*dist_to[destination]));
      }
      if (dist_to[destination] == -999) {
        heap.insert(GraphEdge(destination, -1*dist_to[destination]));
      }
      if (dist_to[destination] < dist_to[current] + weight) {
        dist_to[destination] = (dist_to[current] + weight);
        shortest_path[destination] = current;
        heap.changeKey(to_insert, GraphEdge(destination, -1*dist_to[destination]));
      }
    }
    current = heap.extractMax().dest();
  }
  current = dest;
  while (current!=source) {
    result_path.insert(result_path.begin(), current);
    current = shortest_path[current];
  }
  result_path.insert(result_path.begin(), current);
  return Path(-1*dist_to[dest], result_path);
}
```