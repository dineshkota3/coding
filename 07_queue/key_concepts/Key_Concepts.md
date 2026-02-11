# Queue - Key Concepts to Master

## 1. Queue Operations

### Basic Operations using deque
```python
from collections import deque

queue = deque()

# Enqueue
queue.append(1)
queue.append(2)

# Dequeue
front = queue.popleft()  # Returns 1

# Peek
front = queue[0]  # Returns 2

# Check empty
is_empty = len(queue) == 0

# Size
size = len(queue)
```

### Time Complexity
| Operation | Time |
|-----------|------|
| Enqueue | O(1) |
| Dequeue | O(1) |
| Peek | O(1) |
| isEmpty | O(1) |

## 2. Queue Implementation

### Using Array (with front/rear pointers)
```python
class Queue:
    def __init__(self, capacity):
        self.capacity = capacity
        self.queue = [None] * capacity
        self.front = 0
        self.rear = -1
        self.size = 0

    def enqueue(self, item):
        if self.size == self.capacity:
            raise Exception("Queue is full")
        self.rear = (self.rear + 1) % self.capacity
        self.queue[self.rear] = item
        self.size += 1

    def dequeue(self):
        if self.size == 0:
            raise Exception("Queue is empty")
        item = self.queue[self.front]
        self.front = (self.front + 1) % self.capacity
        self.size -= 1
        return item

    def peek(self):
        if self.size == 0:
            raise Exception("Queue is empty")
        return self.queue[self.front]

    def is_empty(self):
        return self.size == 0
```

### Using Linked List
```python
class Node:
    def __init__(self, value):
        self.value = value
        self.next = None

class QueueLinkedList:
    def __init__(self):
        self.front = None
        self.rear = None

    def enqueue(self, item):
        node = Node(item)
        if not self.rear:
            self.front = self.rear = node
        else:
            self.rear.next = node
            self.rear = node

    def dequeue(self):
        if not self.front:
            raise Exception("Queue is empty")
        item = self.front.value
        self.front = self.front.next
        if not self.front:
            self.rear = None
        return item
```

## 3. Circular Queue

### Fixed Size Circular Buffer
```python
class CircularQueue:
    def __init__(self, k):
        self.k = k
        self.queue = [None] * k
        self.front = self.rear = -1

    def enQueue(self, value):
        if self.isFull():
            return False
        if self.isEmpty():
            self.front = 0
        self.rear = (self.rear + 1) % self.k
        self.queue[self.rear] = value
        return True

    def deQueue(self):
        if self.isEmpty():
            return False
        if self.front == self.rear:
            self.front = self.rear = -1
        else:
            self.front = (self.front + 1) % self.k
        return True

    def Front(self):
        return -1 if self.isEmpty() else self.queue[self.front]

    def Rear(self):
        return -1 if self.isEmpty() else self.queue[self.rear]

    def isEmpty(self):
        return self.front == -1

    def isFull(self):
        return (self.rear + 1) % self.k == self.front
```

## 4. Priority Queue

### Using heapq
```python
import heapq

# Min-heap (default)
pq = []
heapq.heappush(pq, 3)
heapq.heappush(pq, 1)
heapq.heappush(pq, 2)
heapq.heappop(pq)  # Returns 1

# Max-heap (negate values)
max_pq = []
heapq.heappush(max_pq, -3)
heapq.heappush(max_pq, -1)
heapq.heappush(max_pq, -2)
heapq.heappop(max_pq)  # Returns -3, which is -(-3) = 3

# Custom priority (priority, item)
pq = []
heapq.heappush(pq, (2, 'task2'))
heapq.heappush(pq, (1, 'task1'))
heapq.heappop(pq)  # Returns (1, 'task1')
```

## 5. Deque (Double-Ended Queue)

### Operations
```python
from collections import deque

dq = deque()

# Add to ends
dq.append(1)       # Add to right
dq.appendleft(0)   # Add to left

# Remove from ends
dq.pop()           # Remove from right
dq.popleft()       # Remove from left

# Access
dq[0]              # Leftmost
dq[-1]             # Rightmost
```

### Sliding Window Maximum with Deque
```python
from collections import deque

def max_sliding_window(nums, k):
    result = []
    dq = deque()  # Stores indices

    for i, num in enumerate(nums):
        # Remove indices outside window
        while dq and dq[0] < i - k + 1:
            dq.popleft()

        # Remove smaller elements
        while dq and nums[dq[-1]] < num:
            dq.pop()

        dq.append(i)

        if i >= k - 1:
            result.append(nums[dq[0]])

    return result
```

## 6. BFS Using Queue

### Tree Level Order Traversal
```python
from collections import deque

def level_order(root):
    if not root:
        return []

    result = []
    queue = deque([root])

    while queue:
        level = []
        for _ in range(len(queue)):
            node = queue.popleft()
            level.append(node.val)
            if node.left:
                queue.append(node.left)
            if node.right:
                queue.append(node.right)
        result.append(level)

    return result
```

### Graph BFS
```python
def bfs(graph, start):
    visited = set()
    queue = deque([start])

    while queue:
        node = queue.popleft()
        if node not in visited:
            visited.add(node)
            for neighbor in graph[node]:
                if neighbor not in visited:
                    queue.append(neighbor)

    return visited
```

## When to Use Queue

| Scenario | Queue Type |
|----------|------------|
| BFS traversal | Simple Queue |
| Level order | Simple Queue |
| Scheduling tasks | Priority Queue |
| Sliding window | Deque |
| Circular buffer | Circular Queue |
| Task scheduling | Priority Queue |
