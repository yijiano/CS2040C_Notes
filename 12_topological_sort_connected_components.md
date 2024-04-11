[[_main|<-- Back to main]]
# Properties
#topological_sort
- Sequential total ordering of all nodes
- Edges only point forward
- Essentially its Post-Order Processing of #DFS
- Time complexity: DFS: O(V + E)
# Implementation
```cpp
DFS-visit (Node[] nodeList, boolean[] visited, int startId) { 
	for every neighbor v of startId { 
		if (!visited[v]){ 
			visited[v] = true; 
			DFS-visit(nodeList, visited, v); 
			schedule.prepend(V);
		} 
	} 
}

DFS (Node[] nodeList) {
	boolean visited [numNode] = {0};
	
	for (start = 0; start<nodeList.length; start++) {
		if (!visited[start]) {
			visited[start] = true;
			DFS-visit(nodeList, visited, start);
			schedule.prepend(V);
		}
	}
}
```