# Shortest-paths
- No weights? => BFS
- No negative weights && greedy is okay? => Dijkstra
- Negative weights || detecting negative cycles? => Bellman-Ford
- (Google Maps || Pacman) && we need heuristic? => A*

---
**Relaxation:** Initialize the path cost of all of the nodes to Infinity. Then whenever we reach a node, we take the minimum of (older cost, path cost of predecessor + cost between predecessor and this node). [Dijkstra, Bellman-Ford]

**Heuristic:** A measure of how close a node is to the target. Used to check that we are actually building a path in the right direction towards that target, unlike the greedy approach. [A*]

## Dijkstra: O(|E|+|V|log|V|)

[codepen](https://codepen.io/ALawliet/pen/XeBQBW)
- Shortest path from ONE node to ALL other nodes (SSSP)
- Greedy
    - If this were Google Maps, we would always choose the lowest weight so far. Even though this may be the "fastest" road or the road least congested by traffic, it may be going in the wrong direction, and we would continue going in that direction until a shorter path is found.

## A*: O(|E|) = O(b^d)

[codepen](https://codepen.io/ALawliet/pen/JrZVMR)
- Shortest path from S to T
- Heuristic instead of greedy
    - Manhattan distance = # cells horizontal + # cells vertical (including obstacles)

## Bellman-Ford: O(|V|*|E|)

[codepen](https://codepen.io/ALawliet/pen/RLBeyq)
- Shortest path from ONE node to ALL other nodes (SSSP)
- DP
- Works with negative edge weights
- Can also detect negative cycles
    - If we just wanted to know if graph has a cycle, we can use DAG topological sort instead

## Floyd-Warshall: O(|V|^3)

- Shortest path from ALL PAIRS of nodes (APSP)