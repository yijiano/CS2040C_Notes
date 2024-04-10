[[_main|<-- Back to main]]

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