# Graph - Practice Problems

## Easy Problems

### 1. Number of Islands
**LeetCode:** #200

**Description:**
Given a 2D grid of '1's (land) and '0's (water), count the number of islands.

**Example:**
```
Input: grid = [
  ["1","1","0","0","0"],
  ["1","1","0","0","0"],
  ["0","0","1","0","0"],
  ["0","0","0","1","1"]
]
Output: 3
```

**Approach Hint:** DFS or BFS to mark connected components.

---

### 2. Graph Valid Tree
**LeetCode:** #261

**Description:**
Given n nodes and edges, determine if they form a valid tree.

**Example:**
```
Input: n = 5, edges = [[0,1],[0,2],[0,3],[1,4]]
Output: true
```

**Approach Hint:** Tree has n-1 edges and is connected. Use Union-Find or DFS.

---

### 3. Clone Graph
**LeetCode:** #133

**Description:**
Clone a graph (deep copy).

**Example:**
```
Input: adjList = [[2,4],[1,3],[2,4],[1,3]]
Output: Deep copy of the graph
```

**Approach Hint:** DFS/BFS with hash map for original -> clone mapping.

---

## Medium Problems

### 4. Course Schedule
**LeetCode:** #207

**Description:**
Determine if you can finish all courses given prerequisites.

**Example:**
```
Input: numCourses = 2, prerequisites = [[1,0]]
Output: true (take course 0 then course 1)
```

**Approach Hint:** Detect cycle in directed graph using DFS or topological sort.

---

### 5. Course Schedule II
**LeetCode:** #210

**Description:**
Return ordering of courses to finish all courses.

**Example:**
```
Input: numCourses = 4, prerequisites = [[1,0],[2,0],[3,1],[3,2]]
Output: [0,2,1,3] or [0,1,2,3]
```

**Approach Hint:** Topological sort using Kahn's algorithm or DFS.

---

### 6. Pacific Atlantic Water Flow
**LeetCode:** #417

**Description:**
Find cells where water can flow to both Pacific and Atlantic oceans.

**Example:**
```
Input: heights = [[1,2,2,3,5],[3,2,3,4,4],[2,4,5,3,1],[6,7,1,4,5],[5,1,1,2,4]]
Output: [[0,4],[1,3],[1,4],[2,2],[3,0],[3,1],[4,0]]
```

**Approach Hint:** BFS/DFS from both oceans, find intersection.

---

### 7. Surrounded Regions
**LeetCode:** #130

**Description:**
Capture surrounded regions: flip 'O' to 'X' if surrounded by 'X'.

**Example:**
```
Input: board = [["X","X","X","X"],["X","O","O","X"],["X","X","O","X"],["X","O","X","X"]]
Output: [["X","X","X","X"],["X","X","X","X"],["X","X","X","X"],["X","O","X","X"]]
```

**Approach Hint:** Mark 'O's connected to border, flip rest.

---

### 8. Rotting Oranges
**LeetCode:** #994

**Description:**
Find minimum minutes until no fresh oranges. Fresh adjacent to rotten becomes rotten each minute.

**Example:**
```
Input: grid = [[2,1,1],[1,1,0],[0,1,1]]
Output: 4
```

**Approach Hint:** Multi-source BFS from all rotten oranges.

---

### 9. Word Ladder
**LeetCode:** #127

**Description:**
Find shortest transformation from beginWord to endWord, changing one letter at a time.

**Example:**
```
Input: beginWord = "hit", endWord = "cog", wordList = ["hot","dot","dog","lot","log","cog"]
Output: 5 (hit -> hot -> dot -> dog -> cog)
```

**Approach Hint:** BFS with word patterns as graph nodes.

---

### 10. Minimum Spanning Tree
**Various platforms**

**Description:**
Find minimum cost to connect all nodes.

**Example:**
```
Input: n = 3, edges = [[0,1,1],[1,2,2],[0,2,3]]
Output: 3 (use edges [0,1,1] and [1,2,2])
```

**Approach Hint:** Kruskal's (sort edges) or Prim's (grow tree).

---

## Hard Problems

### 11. Alien Dictionary
**LeetCode:** #269

**Description:**
Given sorted words in alien language, determine character order.

**Example:**
```
Input: words = ["wrt","wrf","er","ett","rftt"]
Output: "wertf"
```

**Approach Hint:** Build graph from adjacent words, topological sort.

---

## Additional Practice

### Find if Path Exists (Easy) - #1971
Check if path exists between two nodes.

### Keys and Rooms (Easy) - #841
Check if all rooms can be visited.

### Find the Town Judge (Easy) - #997
Find the town judge.

### Reconstruct Itinerary (Medium) - #332
Reconstruct itinerary using all tickets.

### Cheapest Flights Within K Stops (Medium) - #787
Bellman-Ford with stop limit.

### Network Delay Time (Medium) - #743
Dijkstra to find max time to all nodes.

### Redundant Connection (Medium) - #684
Find edge to remove using Union-Find.

### Accounts Merge (Medium) - #721
Merge accounts using Union-Find.

### Longest Increasing Path in Matrix (Hard) - #329
DFS with memoization.

### Word Ladder II (Hard) - #126
BFS to find all shortest paths.

---

## Problem-Solving Tips

1. **Graph construction:**
   - Choose adjacency list vs matrix
   - Handle directed vs undirected
   - Consider weighted edges

2. **BFS vs DFS:**
   - BFS: shortest path, level order
   - DFS: cycle detection, connectivity

3. **Common patterns:**
   - Grid as graph: 4-directional neighbors
   - Build graph first, then traverse
   - Multi-source BFS for spread problems

4. **Union-Find applications:**
   - Connected components
   - Cycle detection
   - MST (Kruskal's)

5. **Edge cases:**
   - Empty graph
   - Single node
   - Disconnected components
   - Self-loops
