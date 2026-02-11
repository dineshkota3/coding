# Queue - Practice Problems

## Easy Problems

### 1. Design Circular Queue
**LeetCode:** #622

**Description:**
Design your implementation of the circular queue with fixed size k.

**Example:**
```
myCircularQueue = MyCircularQueue(3)
myCircularQueue.enQueue(1) -> true
myCircularQueue.enQueue(2) -> true
myCircularQueue.enQueue(3) -> true
myCircularQueue.enQueue(4) -> false (full)
myCircularQueue.Rear() -> 3
```

**Approach Hint:** Use array with front/rear pointers and modulo for wrap-around.

---

### 2. Design Circular Deque
**LeetCode:** #641

**Description:**
Design circular deque that supports insert/delete at both front and rear.

**Example:**
```
myCircularDeque = MyCircularDeque(3)
myCircularDeque.insertLast(1) -> true
myCircularDeque.insertLast(2) -> true
myCircularDeque.insertFront(3) -> true
myCircularDeque.insertFront(4) -> false (full)
```

**Approach Hint:** Extend circular queue with front operations.

---

### 3. Implement Stack using Queues
**LeetCode:** #225

**Description:**
Implement a stack using only queue operations.

**Example:**
```
myStack.push(1)
myStack.push(2)
myStack.top() -> 2
myStack.pop() -> 2
myStack.empty() -> false
```

**Approach Hint:** Rotate queue after each push to keep newest at front.

---

### 4. Moving Average from Data Stream
**LeetCode:** #346

**Description:**
Given a stream of integers and window size, calculate moving average.

**Example:**
```
m = MovingAverage(3)
m.next(1) = 1
m.next(10) = (1 + 10) / 2
m.next(3) = (1 + 10 + 3) / 3
m.next(5) = (10 + 3 + 5) / 3
```

**Approach Hint:** Use deque or circular buffer with running sum.

---

## Medium Problems

### 5. Sliding Window Maximum
**LeetCode:** #239

**Description:**
Find the maximum in each sliding window of size k.

**Example:**
```
Input: nums = [1, 3, -1, -3, 5, 3, 6, 7], k = 3
Output: [3, 3, 5, 5, 6, 7]
```

**Approach Hint:** Use deque to maintain decreasing order of elements.

---

### 6. Design Bounded Blocking Queue
**LeetCode:** #1188

**Description:**
Implement a thread-safe bounded blocking queue.

**Example:**
```
queue = BoundedBlockingQueue(2)
queue.enqueue(1)
queue.enqueue(2)
queue.dequeue() -> 1
```

**Approach Hint:** Use locks and condition variables for thread safety.

---

### 7. Design Hit Counter
**LeetCode:** #362

**Description:**
Design a hit counter that counts hits in the past 5 minutes (300 seconds).

**Example:**
```
hitCounter.hit(1)
hitCounter.hit(2)
hitCounter.hit(3)
hitCounter.getHits(4) -> 3
hitCounter.getHits(301) -> 2 (hit at 1 is older than 300s)
```

**Approach Hint:** Use deque to store timestamps, remove old hits.

---

### 8. Task Scheduler
**LeetCode:** #621

**Description:**
Given tasks A-Z and cooldown n, find minimum time to complete all.

**Example:**
```
Input: tasks = ["A","A","A","B","B","B"], n = 2
Output: 8
Explanation: A -> B -> idle -> A -> B -> idle -> A -> B
```

**Approach Hint:** Use max-heap for most frequent tasks + queue for cooldown.

---

### 9. Number of Islands (BFS approach)
**LeetCode:** #200

**Description:**
Count the number of islands in a 2D grid. Use BFS approach.

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

**Approach Hint:** Use queue for BFS, mark visited cells.

---

## Hard Problems

### 10. Serialize and Deserialize Binary Tree
**LeetCode:** #297

**Description:**
Design algorithm to serialize/deserialize binary tree. Use level-order (BFS).

**Example:**
```
Input: root = [1,2,3,null,null,4,5]
Serialized: "1,2,3,null,null,4,5,null,null,null,null"
```

**Approach Hint:** Use queue for level-order traversal, handle nulls.

---

## Additional Practice

### Walls and Gates (Medium) - #286
Fill each room with distance to nearest gate using BFS.

### Open the Lock (Medium) - #752
Find minimum turns to open lock using BFS.

### Perfect Squares (Medium) - #279
Find minimum perfect squares that sum to n using BFS.

### Course Schedule II (Medium) - #210
Find order of courses using topological sort (BFS).

### Cut Off Trees for Golf Event (Hard) - #675
Use BFS to find shortest path between trees.

### Word Ladder (Hard) - #127
Find shortest transformation using BFS.

---

## Problem-Solving Tips

1. **When to use queue:**
   - BFS traversal (tree, graph)
   - Level-order processing
   - Scheduling with fairness
   - Buffer between producer-consumer

2. **Queue types:**
   - Simple queue: Basic FIFO
   - Circular queue: Fixed-size buffer
   - Deque: Operations at both ends
   - Priority queue: Order by priority

3. **BFS patterns:**
   - Level-by-level: Process all at current level
   - Shortest path: Unweighted graph
   - Multi-source: Start from multiple points

4. **Sliding window with deque:**
   - Maintain monotonic property
   - Front has max/min
   - Remove elements outside window
