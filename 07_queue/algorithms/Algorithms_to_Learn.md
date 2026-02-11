# Queue - Algorithms to Learn

## 1. Queue Implementation

### Problem
Implement queue using array and linked list.

### Algorithm (Linked List)
```python
class Node:
    def __init__(self, value):
        self.value = value
        self.next = None

class Queue:
    def __init__(self):
        self.front = None
        self.rear = None
        self._size = 0

    def enqueue(self, value):
        node = Node(value)
        if not self.rear:
            self.front = self.rear = node
        else:
            self.rear.next = node
            self.rear = node
        self._size += 1

    def dequeue(self):
        if not self.front:
            return None
        value = self.front.value
        self.front = self.front.next
        if not self.front:
            self.rear = None
        self._size -= 1
        return value

    def peek(self):
        return self.front.value if self.front else None

    def is_empty(self):
        return self._size == 0
```

### Complexity
- **Time:** O(1) for all operations
- **Space:** O(n)

---

## 2. Circular Queue Implementation

### Problem
Implement circular queue with fixed size.

### Algorithm
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

### Complexity
- **Time:** O(1) for all operations
- **Space:** O(k)

---

## 3. Implement Stack using Queues

### Problem
Implement stack using only queue operations.

### Algorithm
```python
from collections import deque

class MyStack:
    def __init__(self):
        self.queue = deque()

    def push(self, x):
        self.queue.append(x)
        # Rotate to make new element at front
        for _ in range(len(self.queue) - 1):
            self.queue.append(self.queue.popleft())

    def pop(self):
        return self.queue.popleft()

    def top(self):
        return self.queue[0]

    def empty(self):
        return len(self.queue) == 0
```

### Complexity
- **Time:** O(n) for push, O(1) for others
- **Space:** O(n)

---

## 4. Sliding Window Maximum (using Deque)

### Problem
Find maximum in each sliding window of size k.

### Algorithm
```python
from collections import deque

def max_sliding_window(nums, k):
    result = []
    dq = deque()  # Stores indices, decreasing order

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

### Complexity
- **Time:** O(n)
- **Space:** O(k)

---

## 5. Task Scheduler

### Problem
Given tasks and cooldown n, find minimum time to complete all.

### Algorithm
```python
import heapq
from collections import Counter, deque

def least_interval(tasks, n):
    # Count frequencies
    count = Counter(tasks)

    # Max heap (negative for max-heap)
    max_heap = [-c for c in count.values()]
    heapq.heapify(max_heap)

    # Queue for cooldown: (count, ready_time)
    queue = deque()

    time = 0
    while max_heap or queue:
        time += 1

        if max_heap:
            count = heapq.heappop(max_heap) + 1  # +1 because negative
            if count < 0:  # Still has more
                queue.append((count, time + n))

        # Check if any task is ready
        if queue and queue[0][1] == time:
            heapq.heappush(max_heap, queue.popleft()[0])

    return time
```

### Complexity
- **Time:** O(n × m) where m is unique tasks
- **Space:** O(m)

---

## 6. Design Circular Queue

### Problem
Design circular queue with front, rear, enqueue, dequeue operations.

### Algorithm
```python
class MyCircularQueue:
    def __init__(self, k):
        self.k = k
        self.queue = [None] * k
        self.front = -1
        self.rear = -1

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

### Complexity
- **Time:** O(1) for all operations
- **Space:** O(k)

---

## 7. Design Circular Deque

### Problem
Design circular deque with operations at both ends.

### Algorithm
```python
class MyCircularDeque:
    def __init__(self, k):
        self.k = k
        self.deque = [None] * k
        self.front = 0
        self.rear = k - 1
        self.size = 0

    def insertFront(self, value):
        if self.isFull():
            return False
        self.front = (self.front - 1 + self.k) % self.k
        self.deque[self.front] = value
        self.size += 1
        return True

    def insertLast(self, value):
        if self.isFull():
            return False
        self.rear = (self.rear + 1) % self.k
        self.deque[self.rear] = value
        self.size += 1
        return True

    def deleteFront(self):
        if self.isEmpty():
            return False
        self.front = (self.front + 1) % self.k
        self.size -= 1
        return True

    def deleteLast(self):
        if self.isEmpty():
            return False
        self.rear = (self.rear - 1 + self.k) % self.k
        self.size -= 1
        return True

    def getFront(self):
        return -1 if self.isEmpty() else self.deque[self.front]

    def getRear(self):
        return -1 if self.isEmpty() else self.deque[self.rear]

    def isEmpty(self):
        return self.size == 0

    def isFull(self):
        return self.size == self.k
```

### Complexity
- **Time:** O(1) for all operations
- **Space:** O(k)
