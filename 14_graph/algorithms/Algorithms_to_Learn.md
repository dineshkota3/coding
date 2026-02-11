# Graph - Algorithms to Learn

## 1. Breadth-First Search (BFS)

### Problem
Traverse graph level by level from start node.

### Algorithm
```python
from collections import deque

def bfs(graph, start):
    visited = set([start])
    queue = deque([start])
    result = []

    while queue:
        node = queue.popleft()
        result.append(node)

        for neighbor in graph.get(node, []):
            if neighbor not in visited:
                visited.add(neighbor)
                queue.append(neighbor)

    return result
```

### Complexity
- **Time:** O(V + E)
- **Space:** O(V)

---

## 2. Depth-First Search (DFS)

### Problem
Traverse graph by exploring as far as possible before backtracking.

### Algorithm
```python
def dfs(graph, node, visited=None):
    if visited is None:
        visited = set()

    visited.add(node)

    for neighbor in graph.get(node, []):
        if neighbor not in visited:
            dfs(graph, neighbor, visited)

    return visited
```

### Complexity
- **Time:** O(V + E)
- **Space:** O(V)

---

## 3. Detect Cycle in Undirected Graph

### Problem
Detect if undirected graph has cycle.

### Algorithm
```python
def has_cycle_undirected(graph):
    visited = set()

    def dfs(node, parent):
        visited.add(node)
        for neighbor in graph.get(node, []):
            if neighbor not in visited:
                if dfs(neighbor, node):
                    return True
            elif neighbor != parent:
                return True
        return False

    for node in graph:
        if node not in visited:
            if dfs(node, -1):
                return True
    return False
```

### Complexity
- **Time:** O(V + E)
- **Space:** O(V)

---

## 4. Detect Cycle in Directed Graph

### Problem
Detect if directed graph has cycle.

### Algorithm
```python
def has_cycle_directed(graph, n):
    visited = set()
    rec_stack = set()

    def dfs(node):
        visited.add(node)
        rec_stack.add(node)

        for neighbor in graph.get(node, []):
            if neighbor not in visited:
                if dfs(neighbor):
                    return True
            elif neighbor in rec_stack:
                return True

        rec_stack.remove(node)
        return False

    for i in range(n):
        if i not in visited:
            if dfs(i):
                return True
    return False
```

### Complexity
- **Time:** O(V + E)
- **Space:** O(V)

---

## 5. Topological Sort (Kahn's Algorithm)

### Problem
Order vertices so edges go from earlier to later.

### Algorithm
```python
from collections import deque, defaultdict

def topological_sort(n, edges):
    graph = defaultdict(list)
    in_degree = [0] * n

    for u, v in edges:
        graph[u].append(v)
        in_degree[v] += 1

    queue = deque([i for i in range(n) if in_degree[i] == 0])
    result = []

    while queue:
        node = queue.popleft()
        result.append(node)

        for neighbor in graph[node]:
            in_degree[neighbor] -= 1
            if in_degree[neighbor] == 0:
                queue.append(neighbor)

    return result if len(result) == n else []
```

### Complexity
- **Time:** O(V + E)
- **Space:** O(V)

---

## 6. Dijkstra's Algorithm

### Problem
Find shortest path from source to all nodes (non-negative weights).

### Algorithm
```python
import heapq

def dijkstra(graph, start, n):
    distances = [float('inf')] * n
    distances[start] = 0
    pq = [(0, start)]

    while pq:
        dist, node = heapq.heappop(pq)

        if dist > distances[node]:
            continue

        for neighbor, weight in graph.get(node, []):
            new_dist = dist + weight
            if new_dist < distances[neighbor]:
                distances[neighbor] = new_dist
                heapq.heappush(pq, (new_dist, neighbor))

    return distances
```

### Complexity
- **Time:** O((V + E) log V)
- **Space:** O(V)

---

## 7. Bellman-Ford Algorithm

### Problem
Find shortest path with negative weights (detect negative cycle).

### Algorithm
```python
def bellman_ford(n, edges, start):
    distances = [float('inf')] * n
    distances[start] = 0

    # Relax all edges n-1 times
    for _ in range(n - 1):
        for u, v, w in edges:
            if distances[u] != float('inf') and distances[u] + w < distances[v]:
                distances[v] = distances[u] + w

    # Check for negative cycle
    for u, v, w in edges:
        if distances[u] != float('inf') and distances[u] + w < distances[v]:
            return None  # Negative cycle detected

    return distances
```

### Complexity
- **Time:** O(V × E)
- **Space:** O(V)

---

## 8. Union-Find (Disjoint Set Union)

### Problem
Efficiently union sets and find set membership.

### Algorithm
```python
class UnionFind:
    def __init__(self, n):
        self.parent = list(range(n))
        self.rank = [0] * n

    def find(self, x):
        if self.parent[x] != x:
            self.parent[x] = self.find(self.parent[x])
        return self.parent[x]

    def union(self, x, y):
        px, py = self.find(x), self.find(y)
        if px == py:
            return False
        if self.rank[px] < self.rank[py]:
            px, py = py, px
        self.parent[py] = px
        if self.rank[px] == self.rank[py]:
            self.rank[px] += 1
        return True

    def connected(self, x, y):
        return self.find(x) == self.find(y)
```

### Complexity
- **Time:** O(α(n)) amortized per operation
- **Space:** O(n)

---

## 9. Kruskal's Algorithm (MST)

### Problem
Find minimum spanning tree using edge weights.

### Algorithm
```python
def kruskal(n, edges):
    # Sort edges by weight
    edges.sort(key=lambda x: x[2])

    uf = UnionFind(n)
    mst = []
    total_weight = 0

    for u, v, w in edges:
        if uf.union(u, v):
            mst.append((u, v, w))
            total_weight += w
            if len(mst) == n - 1:
                break

    return mst, total_weight
```

### Complexity
- **Time:** O(E log E)
- **Space:** O(V)

---

## 10. Prim's Algorithm (MST)

### Problem
Find minimum spanning tree by growing tree.

### Algorithm
```python
import heapq

def prim(graph, n):
    visited = [False] * n
    mst_weight = 0
    pq = [(0, 0)]  # (weight, node)

    while pq:
        weight, node = heapq.heappop(pq)

        if visited[node]:
            continue

        visited[node] = True
        mst_weight += weight

        for neighbor, w in graph.get(node, []):
            if not visited[neighbor]:
                heapq.heappush(pq, (w, neighbor))

    return mst_weight
```

### Complexity
- **Time:** O(E log V)
- **Space:** O(V)

---

## 11. Floyd-Warshall Algorithm

### Problem
Find shortest paths between all pairs of vertices.

### Algorithm
```python
def floyd_warshall(n, edges):
    # Initialize distance matrix
    dist = [[float('inf')] * n for _ in range(n)]

    # Distance to self is 0
    for i in range(n):
        dist[i][i] = 0

    # Set direct edge weights
    for u, v, w in edges:
        dist[u][v] = min(dist[u][v], w)
        # For undirected: dist[v][u] = min(dist[v][u], w)

    # Main algorithm
    for k in range(n):
        for i in range(n):
            for j in range(n):
                if dist[i][k] + dist[k][j] < dist[i][j]:
                    dist[i][j] = dist[i][k] + dist[k][j]

    return dist
```

### Complexity
- **Time:** O(V³)
- **Space:** O(V²)

---

## 12. Connected Components

### Problem
Find all connected components in an undirected graph.

### Algorithm
```python
def connected_components(graph, n):
    visited = [False] * n
    components = []

    def dfs(node, component):
        visited[node] = True
        component.append(node)
        for neighbor in graph.get(node, []):
            if not visited[neighbor]:
                dfs(neighbor, component)

    for node in range(n):
        if not visited[node]:
            component = []
            dfs(node, component)
            components.append(component)

    return components

# Using BFS
def connected_components_bfs(graph, n):
    from collections import deque

    visited = [False] * n
    components = []

    for start in range(n):
        if visited[start]:
            continue

        component = []
        queue = deque([start])
        visited[start] = True

        while queue:
            node = queue.popleft()
            component.append(node)

            for neighbor in graph.get(node, []):
                if not visited[neighbor]:
                    visited[neighbor] = True
                    queue.append(neighbor)

        components.append(component)

    return components
```

### Complexity
- **Time:** O(V + E)
- **Space:** O(V)

---

## 13. Number of Islands (2D Grid BFS/DFS)

### Problem
Count number of islands in a 2D grid where '1' is land and '0' is water.

### Algorithm
```python
def num_islands(grid):
    if not grid or not grid[0]:
        return 0

    rows, cols = len(grid), len(grid[0])
    count = 0

    def dfs(r, c):
        if r < 0 or r >= rows or c < 0 or c >= cols or grid[r][c] != '1':
            return

        grid[r][c] = '0'  # Mark as visited

        # Explore 4 directions
        dfs(r + 1, c)
        dfs(r - 1, c)
        dfs(r, c + 1)
        dfs(r, c - 1)

    for r in range(rows):
        for c in range(cols):
            if grid[r][c] == '1':
                count += 1
                dfs(r, c)

    return count

# BFS version
def num_islands_bfs(grid):
    from collections import deque

    if not grid or not grid[0]:
        return 0

    rows, cols = len(grid), len(grid[0])
    count = 0
    directions = [(1, 0), (-1, 0), (0, 1), (0, -1)]

    for r in range(rows):
        for c in range(cols):
            if grid[r][c] == '1':
                count += 1
                queue = deque([(r, c)])
                grid[r][c] = '0'

                while queue:
                    row, col = queue.popleft()
                    for dr, dc in directions:
                        nr, nc = row + dr, col + dc
                        if 0 <= nr < rows and 0 <= nc < cols and grid[nr][nc] == '1':
                            grid[nr][nc] = '0'
                            queue.append((nr, nc))

    return count
```

### Complexity
- **Time:** O(m × n)
- **Space:** O(m × n) worst case for recursion stack

---

## 14. Bipartite Graph Check

### Problem
Determine if a graph is bipartite (can be colored with 2 colors).

### Algorithm
```python
from collections import deque

def is_bipartite(graph, n):
    color = [-1] * n  # -1: uncolored, 0: color A, 1: color B

    for start in range(n):
        if color[start] != -1:
            continue

        queue = deque([start])
        color[start] = 0

        while queue:
            node = queue.popleft()

            for neighbor in graph.get(node, []):
                if color[neighbor] == -1:
                    color[neighbor] = 1 - color[node]
                    queue.append(neighbor)
                elif color[neighbor] == color[node]:
                    return False

    return True

# DFS version
def is_bipartite_dfs(graph, n):
    color = [-1] * n

    def dfs(node, c):
        color[node] = c
        for neighbor in graph.get(node, []):
            if color[neighbor] == -1:
                if not dfs(neighbor, 1 - c):
                    return False
            elif color[neighbor] == color[node]:
                return False
        return True

    for i in range(n):
        if color[i] == -1:
            if not dfs(i, 0):
                return False

    return True
```

### Complexity
- **Time:** O(V + E)
- **Space:** O(V)

---

## 15. Course Schedule (Cycle Detection)

### Problem
Determine if all courses can be finished given prerequisites.

### Algorithm
```python
from collections import defaultdict, deque

def can_finish(num_courses, prerequisites):
    # Build graph and in-degree
    graph = defaultdict(list)
    in_degree = [0] * num_courses

    for course, prereq in prerequisites:
        graph[prereq].append(course)
        in_degree[course] += 1

    # Start with courses having no prerequisites
    queue = deque([i for i in range(num_courses) if in_degree[i] == 0])
    completed = 0

    while queue:
        course = queue.popleft()
        completed += 1

        for next_course in graph[course]:
            in_degree[next_course] -= 1
            if in_degree[next_course] == 0:
                queue.append(next_course)

    return completed == num_courses

# DFS version with cycle detection
def can_finish_dfs(num_courses, prerequisites):
    graph = defaultdict(list)
    for course, prereq in prerequisites:
        graph[prereq].append(course)

    # 0: unvisited, 1: visiting, 2: visited
    state = [0] * num_courses

    def has_cycle(node):
        if state[node] == 1:
            return True  # Cycle detected
        if state[node] == 2:
            return False  # Already processed

        state[node] = 1

        for neighbor in graph[node]:
            if has_cycle(neighbor):
                return True

        state[node] = 2
        return False

    for i in range(num_courses):
        if state[i] == 0:
            if has_cycle(i):
                return False

    return True
```

### Complexity
- **Time:** O(V + E)
- **Space:** O(V)

---

## 16. Clone Graph

### Problem
Create a deep copy of a graph.

### Algorithm
```python
class Node:
    def __init__(self, val=0, neighbors=None):
        self.val = val
        self.neighbors = neighbors if neighbors else []

def clone_graph(node):
    if not node:
        return None

    visited = {}

    def dfs(node):
        if node in visited:
            return visited[node]

        clone = Node(node.val)
        visited[node] = clone

        for neighbor in node.neighbors:
            clone.neighbors.append(dfs(neighbor))

        return clone

    return dfs(node)

# BFS version
def clone_graph_bfs(node):
    if not node:
        return None

    from collections import deque

    visited = {node: Node(node.val)}
    queue = deque([node])

    while queue:
        current = queue.popleft()

        for neighbor in current.neighbors:
            if neighbor not in visited:
                visited[neighbor] = Node(neighbor.val)
                queue.append(neighbor)
            visited[current].neighbors.append(visited[neighbor])

    return visited[node]
```

### Complexity
- **Time:** O(V + E)
- **Space:** O(V)

---

## 17. Word Ladder (Shortest Path in Word Graph)

### Problem
Find shortest transformation from beginWord to endWord.

### Algorithm
```python
from collections import deque, defaultdict

def ladder_length(begin_word, end_word, word_list):
    if end_word not in word_list:
        return 0

    # Build pattern graph
    word_list.append(begin_word)
    pattern_map = defaultdict(list)

    for word in word_list:
        for i in range(len(word)):
            pattern = word[:i] + '*' + word[i+1:]
            pattern_map[pattern].append(word)

    # BFS
    visited = set([begin_word])
    queue = deque([(begin_word, 1)])

    while queue:
        word, length = queue.popleft()

        if word == end_word:
            return length

        for i in range(len(word)):
            pattern = word[:i] + '*' + word[i+1:]
            for neighbor in pattern_map[pattern]:
                if neighbor not in visited:
                    visited.add(neighbor)
                    queue.append((neighbor, length + 1))

    return 0
```

### Complexity
- **Time:** O(M² × N) where M = word length, N = number of words
- **Space:** O(M² × N)

---

## 18. Surrounded Regions

### Problem
Capture surrounded 'O's by flipping them to 'X'.

### Algorithm
```python
def solve_surrounded_regions(board):
    if not board or not board[0]:
        return

    rows, cols = len(board), len(board[0])

    def dfs(r, c):
        if r < 0 or r >= rows or c < 0 or c >= cols or board[r][c] != 'O':
            return
        board[r][c] = 'T'  # Temporarily mark
        dfs(r + 1, c)
        dfs(r - 1, c)
        dfs(r, c + 1)
        dfs(r, c - 1)

    # Mark border 'O's and their connected regions
    for r in range(rows):
        for c in [0, cols - 1]:
            if board[r][c] == 'O':
                dfs(r, c)

    for c in range(cols):
        for r in [0, rows - 1]:
            if board[r][c] == 'O':
                dfs(r, c)

    # Flip: 'O' -> 'X' (surrounded), 'T' -> 'O' (not surrounded)
    for r in range(rows):
        for c in range(cols):
            if board[r][c] == 'O':
                board[r][c] = 'X'
            elif board[r][c] == 'T':
                board[r][c] = 'O'
```

### Complexity
- **Time:** O(m × n)
- **Space:** O(m × n) for recursion

---

## 19. Rotting Oranges (Multi-source BFS)

### Problem
Find minimum time for all oranges to rot.

### Algorithm
```python
from collections import deque

def oranges_rotting(grid):
    rows, cols = len(grid), len(grid[0])
    queue = deque()
    fresh = 0

    # Find all rotten oranges
    for r in range(rows):
        for c in range(cols):
            if grid[r][c] == 2:
                queue.append((r, c, 0))
            elif grid[r][c] == 1:
                fresh += 1

    directions = [(1, 0), (-1, 0), (0, 1), (0, -1)]
    max_time = 0

    while queue:
        r, c, time = queue.popleft()
        max_time = max(max_time, time)

        for dr, dc in directions:
            nr, nc = r + dr, c + dc
            if 0 <= nr < rows and 0 <= nc < cols and grid[nr][nc] == 1:
                grid[nr][nc] = 2
                fresh -= 1
                queue.append((nr, nc, time + 1))

    return max_time if fresh == 0 else -1
```

### Complexity
- **Time:** O(m × n)
- **Space:** O(m × n)

---

## 20. Pacific Atlantic Water Flow

### Problem
Find cells where water can flow to both oceans.

### Algorithm
```python
def pacific_atlantic(heights):
    if not heights or not heights[0]:
        return []

    rows, cols = len(heights), len(heights[0])
    pacific_reachable = set()
    atlantic_reachable = set()

    def dfs(r, c, visited, prev_height):
        if (r, c) in visited or r < 0 or r >= rows or c < 0 or c >= cols:
            return
        if heights[r][c] < prev_height:
            return

        visited.add((r, c))

        for dr, dc in [(1, 0), (-1, 0), (0, 1), (0, -1)]:
            dfs(r + dr, c + dc, visited, heights[r][c])

    # Start from Pacific (top and left edges)
    for r in range(rows):
        dfs(r, 0, pacific_reachable, 0)
    for c in range(cols):
        dfs(0, c, pacific_reachable, 0)

    # Start from Atlantic (bottom and right edges)
    for r in range(rows):
        dfs(r, cols - 1, atlantic_reachable, 0)
    for c in range(cols):
        dfs(rows - 1, c, atlantic_reachable, 0)

    return list(pacific_reachable & atlantic_reachable)
```

### Complexity
- **Time:** O(m × n)
- **Space:** O(m × n)

---

## 21. Longest Increasing Path in Matrix

### Problem
Find longest increasing path in matrix.

### Algorithm
```python
def longest_increasing_path(matrix):
    if not matrix or not matrix[0]:
        return 0

    rows, cols = len(matrix), len(matrix[0])
    memo = [[0] * cols for _ in range(rows)]

    def dfs(r, c):
        if memo[r][c] != 0:
            return memo[r][c]

        max_path = 1
        for dr, dc in [(1, 0), (-1, 0), (0, 1), (0, -1)]:
            nr, nc = r + dr, c + dc
            if 0 <= nr < rows and 0 <= nc < cols and matrix[nr][nc] > matrix[r][c]:
                max_path = max(max_path, 1 + dfs(nr, nc))

        memo[r][c] = max_path
        return max_path

    result = 0
    for r in range(rows):
        for c in range(cols):
            result = max(result, dfs(r, c))

    return result
```

### Complexity
- **Time:** O(m × n)
- **Space:** O(m × n)

---

## 22. Cheapest Flights Within K Stops

### Problem
Find cheapest flight price with at most K stops.

### Algorithm
```python
def find_cheapest_price(n, flights, src, dst, k):
    # Build graph
    graph = defaultdict(list)
    for from_city, to_city, price in flights:
        graph[from_city].append((to_city, price))

    # Dijkstra with stops constraint
    # (price, city, stops)
    heap = [(0, src, 0)]
    min_stops = [float('inf')] * n

    while heap:
        price, city, stops = heapq.heappop(heap)

        if city == dst:
            return price

        if stops > k or stops >= min_stops[city]:
            continue

        min_stops[city] = stops

        for next_city, next_price in graph[city]:
            heapq.heappush(heap, (price + next_price, next_city, stops + 1))

    return -1

# Bellman-Ford approach
def find_cheapest_price_bf(n, flights, src, dst, k):
    prices = [float('inf')] * n
    prices[src] = 0

    for _ in range(k + 1):
        temp_prices = prices[:]

        for from_city, to_city, price in flights:
            if prices[from_city] == float('inf'):
                continue
            temp_prices[to_city] = min(temp_prices[to_city], prices[from_city] + price)

        prices = temp_prices

    return prices[dst] if prices[dst] != float('inf') else -1
```

### Complexity
- **Dijkstra:** O(E log E)
- **Bellman-Ford:** O(K × E)

---

## 23. Network Delay Time

### Problem
Find time for signal to reach all nodes.

### Algorithm
```python
import heapq

def network_delay_time(times, n, k):
    # Build graph
    graph = defaultdict(list)
    for u, v, w in times:
        graph[u].append((v, w))

    # Dijkstra
    distances = {i: float('inf') for i in range(1, n + 1)}
    distances[k] = 0
    heap = [(0, k)]
    visited = set()

    while heap:
        dist, node = heapq.heappop(heap)

        if node in visited:
            continue
        visited.add(node)

        for neighbor, weight in graph[node]:
            new_dist = dist + weight
            if new_dist < distances[neighbor]:
                distances[neighbor] = new_dist
                heapq.heappush(heap, (new_dist, neighbor))

    max_time = max(distances.values())
    return max_time if max_time != float('inf') else -1
```

### Complexity
- **Time:** O(E log V)
- **Space:** O(V + E)

---

## 24. Accounts Merge (Union-Find Application)

### Problem
Merge accounts with common emails.

### Algorithm
```python
def accounts_merge(accounts):
    uf = {}
    email_to_name = {}

    def find(x):
        if x not in uf:
            uf[x] = x
        if uf[x] != x:
            uf[x] = find(uf[x])
        return uf[x]

    def union(x, y):
        uf[find(x)] = find(y)

    # Build union-find structure
    for account in accounts:
        name = account[0]
        first_email = account[1]

        for email in account[1:]:
            email_to_name[email] = name
            union(first_email, email)

    # Group emails by root
    root_to_emails = defaultdict(list)
    for email in email_to_name:
        root_to_emails[find(email)].append(email)

    # Build result
    result = []
    for root, emails in root_to_emails.items():
        result.append([email_to_name[root]] + sorted(emails))

    return result
```

### Complexity
- **Time:** O(N × α(N)) where N = total emails
- **Space:** O(N)
