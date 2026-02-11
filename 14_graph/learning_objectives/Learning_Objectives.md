# Graph - Learning Objectives

## Overview
Graphs are versatile data structures for modeling relationships. Mastering graph algorithms is essential for many real-world problems.

## Learning Objectives

### 1. Graph Representation
- Learn adjacency list representation
- Understand adjacency matrix representation
- Master when to use each representation
- Practice building graphs from edge lists

### 2. Graph Types and Properties
- Understand directed vs undirected graphs
- Learn weighted vs unweighted graphs
- Master connected components concept
- Understand cycle detection

### 3. Graph Traversal
- Master BFS (Breadth-First Search)
- Master DFS (Depth-First Search)
- Understand when to use BFS vs DFS
- Practice traversal applications

### 4. Shortest Path Algorithms
- Learn Dijkstra's algorithm
- Understand Bellman-Ford algorithm
- Master Floyd-Warshall algorithm
- Know when to use each algorithm

### 5. Advanced Graph Algorithms
- Learn topological sort
- Master Union-Find (Disjoint Set Union)
- Understand Minimum Spanning Tree
- Practice Kruskal's and Prim's algorithms

## Python-Specific Notes
- Use dictionary for adjacency list: `{node: [neighbors]}`
- Use set for visited tracking
- Use deque for BFS
- heapq for priority queue in Dijkstra

## Success Criteria
- [ ] Implement BFS and DFS from scratch
- [ ] Detect cycles in directed and undirected graphs
- [ ] Find shortest path using Dijkstra
- [ ] Implement topological sort
- [ ] Apply Union-Find for connected components
