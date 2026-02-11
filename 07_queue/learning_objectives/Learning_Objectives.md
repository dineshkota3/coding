# Queue - Learning Objectives

## Overview
Queue is a First-In-First-Out (FIFO) data structure essential for BFS and scheduling problems.

## Learning Objectives

### 1. FIFO Property Understanding
- Understand First-In-First-Out behavior
- Learn when FIFO is the natural approach
- Master queue visualization and mental model
- Recognize problems requiring queue

### 2. Queue Operations Mastery
- Master enqueue, dequeue, peek, and isEmpty operations
- Understand time complexity O(1) for all operations
- Learn queue implementation using array and linked list
- Practice with Python collections.deque

### 3. Circular Queue Implementation
- Understand circular buffer concept
- Learn to implement circular queue with fixed size
- Master front and rear pointer management
- Handle wrap-around logic

### 4. Priority Queue and Deque
- Learn priority queue concept and applications
- Master Python heapq module
- Understand deque (double-ended queue)
- Practice sliding window with deque

## Python-Specific Notes
- Use `collections.deque` for efficient queue
- `deque.append()` for enqueue, `deque.popleft()` for dequeue
- `heapq` for priority queue (min-heap by default)
- For max-heap, negate values or use custom comparator

## Success Criteria
- [ ] Implement queue using array and linked list
- [ ] Implement circular queue with fixed size
- [ ] Use queue for BFS traversal
- [ ] Apply deque for sliding window maximum
- [ ] Implement priority queue using heap
