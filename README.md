# Shortest-paths
- No weights? => BFS
- No negative weights && greedy is okay? => Dijkstra
- Negative weights || detecting negative cycles? => Bellman-Ford
- (Google Maps || Pacman) && we need heuristic? => A*

---
**Relaxation:** Initialize the path cost of all of the nodes to Infinity. Then whenever we reach a node, we take the minimum of (older cost, path cost of predecessor + cost between predecessor and this node). [Dijkstra, Bellman-Ford]

**Heuristic:** A measure of how close a node is to the target. Used to check that we are actually building a path in the right direction towards that target, unlike the greedy approach. [A*]

## Dijkstra: O(E+VlogV)

[codepen](https://codepen.io/ALawliet/pen/XeBQBW)
- Shortest path from ONE node to ALL other nodes (SSSP)
- Greedy
    - If this were Google Maps, we would always choose the lowest weight so far. Even though this may be the "fastest" road or the road least congested by traffic, it may be going in the wrong direction, and we would continue going in that direction until a shorter path is found.
```
function dijkstra()
  dist = {}
  prev = {}

  for (each vertex)
    if (start vertex)
      dist[start vertex] = 0
    else
      dist[other vertex] = +INF

  Q = [all vertices]  // ideally fibonacci heap for optimal running time

  while (Q not empty)
    u = remove vertex with lowest dist from Q (extract min)  // greedy

    for (each edge(u: [v, weight]))
      if (dist[v] > dist[u] + weight)
        dist[v] = dist[u] + weight
        prev[v] = u

  return dist
````

## Bellman-Ford: O(VE)

[codepen](https://codepen.io/ALawliet/pen/RLBeyq)
- Shortest path from ONE node to ALL other nodes (SSSP)
- DP
- Works with negative edge weights
- Can also detect negative cycles
    - If we just wanted to know if graph has a cycle, we can use DAG topological sort instead
```
function bellmanFord()
  dist = {}
  prev = {}
  
  for (each vertex)
    if (start vertex)
      dist[start vertex] = 0
    else
      dist[other vertex] = +INF
  
  loop (|V|-1)  // this is main difference from Dijkstra
    for (each edge(u: [v, weight]))
      dist[v] = Math.min(dist[v], dist[u] + weight)  // update every edge
      prev[v] = u

  return dist
```

## A*: O(E) = O(b^d)

[codepen](https://codepen.io/ALawliet/pen/JrZVMR)
- Shortest path from ONE node to SINGLE TARGET node (STSP)
- Heuristic instead of greedy
    - Manhattan distance = # cells horizontal + # cells vertical to target (incl. obstacles)
```
function aStar()
  open = []
  closed = []

  add start to open
  
  while (open not empty)
    current = node with lowest F in open

    drop current from open and add it to closed

    if (current is target)
      return  // draw path from target.parent to start

    for (each neighbor)
      if (neighbor not traversible or neighbor in closed)
        continue
    
      if ((neighbor.F < current.F) or neighbor not in open)
        neighbor.parent = current
        neighbor.H = # cells horizontal + # cells vertical to target (incl. obstacles)
        neighbor.G = neighbor is diagonal ? 14 : 10
        neighbor.F = neighbor.G + neighbor.H
        if (neighbor not in open)
          add neighbor to open
 ```

## Floyd-Warshall: O(V^3)

- Shortest path from ALL PAIRS of nodes (APSP)