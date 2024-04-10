[[_main|<-- Back to main]]
# Shortest Path
#shortest_path 
- Cannot use #BFS as it finds the minimum number of HOPS, not distance.
- $\delta$(u, v) = distance from $u$ to $v$
- Maintain estimate for each distance
	- Init distance to every node as infinity
	- Reduce the estimate with every search (through relaxing each edge)
		- assert(estimate $\geq$ actual shortest distance)
# Bellman-Ford
#bellman-ford

Basic Idea:
- Repeat |V| times: relax every edge
- Stop when "converges"
- O(VE) time.

Special Cases: 
- Negative weight cycles (impossible to proceed)
	- To detect, run Bellman-Ford for |V| + 1 iterations.
	- If an estimate changes in the last iteration then negative weight cycle.
- All edges have the same weight -> use regular #bfs 

>[!DEFINITION]
>**Edge relaxation** means that during traversing our graph and finding our shortest path, **we update the paths we have for already known nodes as soon as we find a shorter path to reach it.**

```cpp
for (int i = 0; i < numNode; i++) {
	// Terminate early when there is no more improvement
	for (every edge e in graph) {
		relax(e);
	}
}
```





